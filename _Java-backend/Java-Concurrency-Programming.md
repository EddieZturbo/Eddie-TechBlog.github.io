---
title: "Java-Concurrency-Programming"
collection: Java-backend
permalink: /Java-backend/Java-Concurrency-Programming
excerpt: 'Java-Concurrency-Programming'
date: 2023-02-05
venue: 'February 5'
---
# Java Concurrency Programming

## 理论基础

### 上下文切换：

> 上下文切换：
>
> 多线程编程中一般线程的个数都大于 CPU 核心的个数，而一个 CPU 核心在任意时刻只能被一个线程使用，为了让这些线程都能得到有效执行，CPU 采取的策略是为每个线程**分配时间片**并**轮转**的形式。当一个线程的时间片用完的时候就会重新处于就绪状态让给其他线程使用，这个过程就属于一次上下文切换。概括来说就是：当前任务在执行完 CPU 时间片切换到另一个任务之前会先保存自己的状态，以便下次再切换回这个任务时，可以再加载这个任务的状态。
>
> **任务从保存到再加载的过程就是一次上下文切换**。
>
> **挂起线程**和**恢复线程**的操作**都需要转入内核态中完成**，这些操作对系统的并发性能带来了很大的压力
>
> 上下文切换通常是计算密集型的。也就是说，它需要相当可观的处理器时间，在每秒几十上百次的切换中，每次切换都需要纳秒量级的时间。所以，上下文切换对系统来说意味着消耗大量的 CPU 时间，事实上，可能是操作系统中时间消耗最大的操作。
>
> Linux 相比与其他操作系统（包括其他类 Unix 系统）有很多的优点，其中有一项就是，其上下文切换和模式切换的时间消耗非常少。

## 线程基础

## Java并发机制的底层实现原理

### Java Object Memory Layout

![image-20221024174142826](C:\Users\ZJH20\AppData\Roaming\Typora\typora-user-images\image-20221024174142826.png)

In Hotspot VM, the object layout in the heap can be divided into three parts,

1. Header
2. Instance Data
3. Padding

#### Header:eyes:

It saves two types of information.

1. Save the object self's runtime information, the officials call it `Mark Word`, such as HashCode, GC generation age, lock states, the lock that the thread holds, biased thread id, biased timestamp.
2. Save the type pointer, that's the pointer to the meta-type, Java VM used it  to determine which type of this object is, this is an optional  implementation in the VM.
   If the object is an array, there is a data in the header to save the array's length

##### Mark Word:eye:

![image-20230210154448670](/images/image-20230210154448670.png)

```
一个对象创建时：
如果开启了偏向锁（默认开启），那么对象创建后，markword 值为 0x05 即最后 3 位为 101，这时它的 thread、epoch、age 都为 0
偏向锁是默认是延迟的，不会在程序启动时立即生效，如果想避免延迟，可以加 VM 参数 
-
XX:BiasedLockingStartupDelay=0 来禁用延迟
如果没有开启偏向锁，那么对象创建后，markword 值为 0x01 即最后 3 位为 001，这时它的 hashcode、age 都为 0，第一次用到 hashcode 时才会赋值

轻量锁和重量锁一个会把hashcode放在栈帧的锁记录，一个会放到monitor中（解锁的时候会还原回来）
而偏向锁没有额外的储存空间 当获取了hashcode则会弃用偏向锁（消除偏向状态） 重写markword

谨记偏向是指类偏向，而不是对象实例偏向；一个类只能有一个偏向
```

![image-20230210154116888](/images/image-20230210154116888.png)

![image-20230210145412031](/images/image-20230210145412031.png)



The 32 bit and 64 bit VM are different.

- 32-bit word

| Object              | Format                                                    |
| ------------------- | --------------------------------------------------------- |
| normal object       | hash: 25, age: 4, biased_lock: 1, lock: 2                 |
| biased object       | JavaThread*: 23, epoch: 2 age: 4, biased_lock: 1, lock: 2 |
| CMS free block      | 32 bits                                                   |
| CMS promoted object | PromotedObject*: 29, promo_bits: 3                        |

- 64-bit word

| Object                       | Format                                                       |
| ---------------------------- | ------------------------------------------------------------ |
| normal object                | unused: 25, hash: 31, unused: 1, age: 4, biased_lock: 1, lock: 2 |
| biased object                | JavaThread*: 54, epoch: 2, unused: 1, age: 4, biased_lock: 1, lock: 2 |
| CMS promoted object          | PromotedObject*: 61, promo_bits: 3                           |
| CMS free block               | 64 bits                                                      |
| COOPs && normal object       | unused: 25, hash: 31, cms_free: 1, age: 4, biased_lock: 1, lock: 2 |
| COOPs && biased object       | JavaThread*: 54, epoch: 2, cms_free: 1, age: 4, biased_lock: 1, lock: 2 |
| COOPs && CMS promoted object | narrowOop: 32, unused: 24, cms_free: 1, unused: 4, promo_bits: 3 |
| COOPs && CMS free block      | unused: 21, size: 35, cms_free: 1, unused: 7                 |

##### Class Metadata Address

指向该对象的所属类型



##### Is Array ? Array Length : nothing

#### Instance Data

The instance data saves the variables defined in the class, including the  variable defined in the parent class. The store sequence will be  impacted by the JVM argument `-XX:FieldsAllocationStyle` and the sequence defined in the class.

> The Hotspot's default allocation sequence is that,
>
> - longs/doubles
> - ints
> - shorts/chars
> - bytes/booleans
> - oops(Ordinary Object Pointers, OOP)

Also, if JVM argument `-XX:CompactFields` is true(default value), the thinner variable in the child class will be inserted into the gap of parent variables.

#### Padding

The HotSpot VM's auto memory management system requires the starting  address of the object must be 8-byte event digits, which means any  object's size muse be 8-byte event digits. So, if an object's instance  data doesn't align, it needs padding.



### Monitor

> **Each object and its class are associated with a monitor.**



> Java's monitor supports two kinds of thread synchronization: ==*mutual exclusion*== and ==*cooperation*==. 
>
> 
>
> ==*mutual exclusion*==, which is supported in the Java virtual machine via  object locks, enables multiple threads to **independently work on shared  data without interfering with each other**;**only one thread can "own" at any one time.**
>
> :lock:每个 Java 对象都可以关联一个 Monitor 对象，如果使用 synchronized 给对象上锁（重量级）之后，该对象头的Mark Word 中就被设置指向 Monitor 对象的指针
>
> 
>
> ==*cooperation*==, which is supported in the Java virtual machine via the ==wait== and ==notify== methods of class `Object`, **enables threads to work together towards a common goal.**
>
> | Method                                 | Description                                                  |
> | -------------------------------------- | ------------------------------------------------------------ |
> | `void wait();`                         | Enter a monitor's wait set until notified by another thread<br />This method should **only be called by** a thread that is the **owner of this object's monitor.** |
> | `void wait(long timeout); `            | Enter a monitor's wait set until notified by another thread or `timeout` milliseconds elapses |
> | `void wait(long timeout, int nanos); ` | Enter a monitor's wait set until notified by another thread or `timeout` milliseconds plus `nanos` nanoseconds elapses<br />**timeout** – the maximum time to wait in milliseconds.<br/>**nanos** – additional time, in nanoseconds range 0-999999. |
> | `void notify();`                       | Wake up one thread waiting in the monitor's wait set. (If no threads are waiting, do nothing.) |
> | `void notifyAll();`                    | Wake up all threads waiting in the monitor's wait set. (If no threads are waiting, do nothing.) |





![image-20230210133418542](/images/image-20230210133418542.png)

![image-20230210133507494](/images/image-20230210133507494.png)

### synchronized

#### synchronized底层实现

> **当一个线程试图访问synchronized同步代码块或方法时**，它首先**必须得到锁**;
>
> **退出或抛出异常时必须释放锁**
>
> 
>
> JVM基于进入和退出Monitor对象来实现方法同步和代码块同步
>
> 
>
> **代码块级别**的 JVM中==monitorenter==和==monitorexit==字节码指令依赖于底层的操作系统的**Mutex Lock**来实现的
>
> **方法级别**的 synchronized 不会在字节码指令中有所体现

```java
synchronized (this) {//--------monitorenter
	//critical section
}//----------------------------monitorexit
```

#### synchronized应用

> ==对象锁==
>
> In the Java virtual machine, **every object and class is logically associated with a ==monitor==.**
>
> 
>
> ==类锁==
>
> Class locks are actually implemented as object locks. As mentioned in earlier chapters, when the Java virtual machine loads a class file, it creates an instance of `class java.lang.Class.` When you lock a class, you are actually locking that class's Class object.



==应用于方法上==

```java
public synchronized void test2(String s) {//对象锁 默认为this对象
	...
}

public static synchronized void test3(String s) {//类锁 默认的锁就是当前所在的Class类
    /*Class locks are actually implemented as object locks. As mentioned in earlier chapters, when the Java virtual machine loads a class file, it creates an instance of class java.lang.Class. When you lock a class, you are actually locking that class's Class object. */
	...
}
```

==应用于代码块==

可以指定任意对象作为锁

```java
synchronized (this) {//对象锁
	...
}

synchronized (Person.class) {//类锁
    /*Class locks are actually implemented as object locks. As mentioned in earlier chapters, when the Java virtual machine loads a class file, it creates an instance of class java.lang.Class. When you lock a class, you are actually locking that class's Class object. */
	...
}
```

#### synchronized锁的升级

> Java SE 1.6里Synchronied同步锁，一共有四种状态：`无锁`、`偏向锁`、`轻量级锁`、`重量级锁`，它会**随着竞争**情况**逐渐升级**。锁可以升级但是**不可以降级**，
>
> 目的是为了**提高获取锁和释放锁的效率**。
>
> 可以通过-XX:-UseBiasedLocking=false来禁用偏向锁。
>
> 锁膨胀方向： 无锁 → 偏向锁 → 轻量级锁 → 重量级锁 (此过程是不可逆的)



## JUC(Java Util Concurrency)

### Java 线程池

**池化技术的思想**主要是为了**减少每次获取资源的消耗**，**提高对资源的利用率**

- ==**降低资源消耗**==。通过重复利用已创建的线程降低线程创建和销毁造成的消耗。

- ==**提高响应速度**==。当任务到达时，任务可以不需要等到线程创建就能立即执行。

- ==**提高线程的可管理性**==。线程是稀缺资源，如果无限制的创建，不仅会消耗系统资源，还会降低系统的稳定性，使用线程池可以进行统一的分配，调优和监控。

### 线程池原理分析

![image-20230204232022514](/images/image-20230204232022514.png)

**线程池主要处理流程**

![image-20230204231928198](/images/image-20230204231928198.png)

```
1）如果当前运行的线程少于corePoolSize，则创建新线程来执行任务（注意，执行这一步骤
需要获取全局锁）。
2）如果运行的线程等于或多于corePoolSize，则将任务加入BlockingQueue。
3）如果无法将任务加入BlockingQueue（队列已满），则创建新的线程来处理任务（注意，执
行这一步骤需要获取全局锁）。
4）如果创建新线程将使当前运行的线程超出maximumPoolSize，任务将被拒绝，并调用
RejectedExecutionHandler.rejectedExecution()方法。
```

![image-20230204232431709](/images/image-20230204232431709.png)

```java
   // 存放线程池的运行状态 (runState) 和线程池内有效线程的数量 (workerCount)
   private final AtomicInteger ctl = new AtomicInteger(ctlOf(RUNNING, 0));

    private static int workerCountOf(int c) {
        return c & CAPACITY;
    }
    //任务队列
    private final BlockingQueue<Runnable> workQueue;

    public void execute(Runnable command) {
        // 如果任务为null，则抛出异常。
        if (command == null)
            throw new NullPointerException();
        // ctl 中保存的线程池当前的一些状态信息
        int c = ctl.get();

        //  下面会涉及到 3 步 操作
        // 1.首先判断当前线程池中执行的任务数量是否小于 corePoolSize
        // 如果小于的话，通过addWorker(command, true)新建一个线程，并将任务(command)添加到该线程中；然后，启动该线程从而执行任务。
        if (workerCountOf(c) < corePoolSize) {
            if (addWorker(command, true))
                return;
            c = ctl.get();
        }
        // 2.如果当前执行的任务数量大于等于 corePoolSize 的时候就会走到这里
        // 通过 isRunning 方法判断线程池状态，线程池处于 RUNNING 状态并且队列可以加入任务，该任务才会被加入进去
        if (isRunning(c) && workQueue.offer(command)) {
            int recheck = ctl.get();
            // 再次获取线程池状态，如果线程池状态不是 RUNNING 状态就需要从任务队列中移除任务，并尝试判断线程是否全部执行完毕。同时执行拒绝策略。
            if (!isRunning(recheck) && remove(command))
                reject(command);
                // 如果当前线程池为空就新创建一个线程并执行。
            else if (workerCountOf(recheck) == 0)
                addWorker(null, false);
        }
        //3. 通过addWorker(command, false)新建一个线程，并将任务(command)添加到该线程中；然后，启动该线程从而执行任务。
        //如果addWorker(command, false)执行失败，则通过reject()执行相应的拒绝策略的内容。
        else if (!addWorker(command, false))
            reject(command);
    }
```

### Executor 框架

`Executor` 框架是 Java5 之后引进的，在 Java 5 之后，通过 `Executor` 来启动线程比使用 `Thread` 的 `start` 方法更好，除了更易管理，效率更好（用线程池实现，节约开销）外，还有关键的一点：有助于避免 this 逃逸问题。

> 补充：this 逃逸是指在构造函数返回之前其他线程就持有该对象的引用. 调用尚未构造完全的对象的方法可能引发令人疑惑的错误。

`Executor` 框架不仅包括了线程池的管理，还提供了线程工厂、队列以及拒绝策略等，`Executor` 框架让并发编程变得更加简单。

#### Executor 框架结构(三大部分组成)

![image-20230205000128358](/images/image-20230205000128358.png)

- 任务(`Runnable` /`Callable`)
- 任务的执行(`Executor`)
- 异步计算的结果(`Future`)

1. **主线程首先要创建实现 `Runnable` 或者 `Callable` 接口的任务对象。**
2. **把创建完成的实现 `Runnable`/`Callable`接口的 对象直接交给 `ExecutorService` 执行**: `ExecutorService.execute（Runnable command）`）或者也可以把 `Runnable` 对象或`Callable` 对象提交给 `ExecutorService` 执行（`ExecutorService.submit（Runnable task）`或 `ExecutorService.submit（Callable <T> task）`）。
3. **如果执行 `ExecutorService.submit（…）`，`ExecutorService` 将返回一个实现`Future`接口的对象**（我们刚刚也提到过了执行 `execute()`方法和 `submit()`方法的区别，`submit()`会返回一个 `FutureTask 对象）。由于 FutureTask` 实现了 `Runnable`，我们也可以创建 `FutureTask`，然后直接交给 `ExecutorService` 执行。
4. **最后，主线程可以执行 `FutureTask.get()`方法来等待任务执行完成。主线程也可以执行 `FutureTask.cancel（boolean mayInterruptIfRunning）`来取消此任务的执行。**

##### 任务(`Runnable` /`Callable`)

执行任务需要实现的 **`Runnable` 接口** 或 **`Callable`接口**。**`Runnable` 接口**或 **`Callable` 接口** 实现类都可以被 **`ThreadPoolExecutor`** 或 **`ScheduledThreadPoolExecutor`** 执行。

##### 任务的执行(`Executor`)

任务执行机制的核心接口 **`Executor`** ，以及继承自 `Executor` 接口的 **`ExecutorService` 接口。**

**`ThreadPoolExecutor`** 和 

**`ScheduledThreadPoolExecutor`** 

这两个关键类实现了 **ExecutorService 接口**。

![image-20230205000754985](/images/image-20230205000754985.png)

##### 异步计算的结果(`Future`)

**`Future`** 接口以及 `Future` 接口的实现类 **`FutureTask`** 类都可以代表异步计算的结果。

当我们把 **`Runnable`接口** 或 **`Callable` 接口** 的实现类提交给 **`ThreadPoolExecutor`** 或 **`ScheduledThreadPoolExecutor`** 执行。（调用 `submit()` 方法时会返回一个 **`FutureTask`** 对象）

#### Executors工具类

> 使用线程池的好处是减少在创建和销毁线程上所消耗的时间以及系统资源开销，解决资源不足的问题。如果不使用线程池，有可能会造成系统创建大量同类线程而导致消耗完内存或者“过度切换”的问题。

另外，《阿里巴巴 Java 开发手册》中**强制**线程池**不允许使用** `Executors` 去创建，而是通过 `ThreadPoolExecutor` 构造函数的方式，这样的处理方式让写的同学更加明确线程池的运行规则，规避资源耗尽的风险



**通过 `Executor` 框架的工具类 `Executors` 来实现** 我们可以创建三种类型的 `ThreadPoolExecutor`：

- `FixedThreadPool`
- `SingleThreadExecutor`
- `CachedThreadPool`

### ThreadPoolExecutor★

**线程池实现类 `ThreadPoolExecutor` 是 `Executor` 框架最核心的类**

**推荐使用 `ThreadPoolExecutor` 构造函数创建线程池**



**`ThreadPoolExecutor` 3 个最重要的参数：**

- **`corePoolSize`** : 核心线程数线程数定义了最小可以同时运行的线程数量。
- **`maximumPoolSize` :** 当队列中存放的任务达到队列容量的时候，当前可以同时运行的线程数量变为最大线程数。
- **`workQueue`:** 当新任务来的时候会先判断当前运行的线程数量是否达到核心线程数，如果达到的话，新任务就会被存放在队列中。**阻塞队列**
  - `ArrayBlockingQueue`：是一个基于数组结构的有界阻塞队列，此队列按FIFO（先进先出）原则对元素进行排序
  - `LinkedBlockingQueue`：一个基于链表结构的阻塞队列，此队列按FIFO排序元素，**吞吐量通常要高于ArrayBlockingQueue**。静态工厂方法Executors.newFixedThreadPool()使用了这个队列。
  - `SynchronousQueue`：一个不存储元素的阻塞队列。每个插入操作必须等到另一个线程调用移除操作，否则插入操作一直处于阻塞状态，**吞吐量通常要高于Linked-BlockingQueue**，静态工厂方法Executors.newCachedThreadPool使用了这个队列。
  - `PriorityBlockingQueue`：一个具**有优先级的无限阻塞队列**。

`ThreadPoolExecutor`其他常见参数 :

1. **`keepAliveTime`**:当线程池中的线程数量大于 `corePoolSize` 的时候，如果这时没有新的任务提交，线程池中且核心线程外的线程不会立即销毁，而是会等待，直到等待的时间超过了 `keepAliveTime`才会被回收销毁；(**线程池中且核心线程外的线程空闲后，保持存活的时间**)

2. **`unit`** : `keepAliveTime` 参数的时间单位。

3. **`threadFactory`** :executor 创建新线程的时候会用到。

4. **`handler`** :饱和(拒绝)策略。关于饱和策略下面单独介绍一下。**`ThreadPoolExecutor` 饱和策略定义:**

   如果当前同时运行的线程数量达到最大线程数量并且队列也已经被放满了任务时，`ThreadPoolTaskExecutor` 定义一些策略:

   - `ThreadPoolExecutor.AbortPolicy` ：抛出 `RejectedExecutionException`来拒绝新任务的处理。(抛异常)
   - `ThreadPoolExecutor.CallerRunsPolicy` ：**只用调用者所在线程来运行任务(直接执行run方法不启动新线程)**;调用执行自己的线程运行任务，也就是直接在调用`execute`方法的线程中运行(`run`)被拒绝的任务，如果执行程序已关闭，则会丢弃该任务。因此这种策略会降低对于新任务提交速度，影响程序的整体性能。如果您的应用程序可以承受此延迟并且你要求任何一个任务请求都要被执行的话，你可以选择这个策略。
   - `ThreadPoolExecutor.DiscardPolicy` ：不处理新任务，直接丢弃掉。(丢弃新任务)
   - `ThreadPoolExecutor.DiscardOldestPolicy` ： 此策略将丢弃最早的未处理的任务请求。（丢弃老任务）

```java
/**
     * 用给定的初始参数创建一个新的ThreadPoolExecutor。
     */
    public ThreadPoolExecutor(int corePoolSize,//线程池的核心线程数量
                              int maximumPoolSize,//线程池的最大线程数
                              long keepAliveTime,//当线程数大于核心线程数时，多余的空闲线程存活的最长时间
                              TimeUnit unit,//时间单位
                              BlockingQueue<Runnable> workQueue,//任务队列，用来储存等待执行任务的队列
                              ThreadFactory threadFactory,//线程工厂，用来创建线程，一般默认即可
                              RejectedExecutionHandler handler//拒绝策略，当提交的任务过多而不能及时处理时，我们可以定制策略来处理任务
                               ) {
        if (corePoolSize < 0 ||
            maximumPoolSize <= 0 ||
            maximumPoolSize < corePoolSize ||
            keepAliveTime < 0)
            throw new IllegalArgumentException();
        if (workQueue == null || threadFactory == null || handler == null)
            throw new NullPointerException();
        this.corePoolSize = corePoolSize;
        this.maximumPoolSize = maximumPoolSize;
        this.workQueue = workQueue;
        this.keepAliveTime = unit.toNanos(keepAliveTime);
        this.threadFactory = threadFactory;
        this.handler = handler;
    }
```

![image-20230204232022514](/images/image-20230204232022514.png)

#### 创建线程池

##### **方式一：通过`ThreadPoolExecutor`构造函数实现（推荐）**

```java
/**
 @author EddieZhang
 @create 2023-02-05 12:36 AM
 */
public class ThreadPoolExecutorTest {
    private static final int CORE_POOL_SIZE = 5;//核心线程数
    private static final int MAX_POOL_SIZE = 10;//线程池中最大线程数
    private static final int QUEUE_CAPACITY = 100;//阻塞队列的最大容量
    private static final Long KEEP_ALIVE_TIME = 1L;//线程池中非核心空闲线程的存活时间
    public static void main(String[] args) {
        /**
         * (
         *  int corePoolSize,//核心线程数
         *  int maximumPoolSize,//线程池中最大线程数
         *  long keepAliveTime,//线程池中非核心空闲线程的存活时间
         *  TimeUnit unit,//存活时间单位
         *  BlockingQueue<Runnable> workQueue,//阻塞队列
         *  ThreadFactory threadFactory,//线程工厂
         *  RejectedExecutionHandler handler//拒接策略
         *  )
         */
        //通过ThreadPoolExecutor构造函数自定义参数创建
        ThreadPoolExecutor threadPoolExecutor;
        threadPoolExecutor = new ThreadPoolExecutor(
                CORE_POOL_SIZE,
                MAX_POOL_SIZE,
                5,
                TimeUnit.SECONDS,
                new ArrayBlockingQueue<>(QUEUE_CAPACITY),
                new ThreadPoolExecutor.CallerRunsPolicy());
        for (int i = 0; i < 10; i++) {
            Runnable thread = new Thread(() -> {
                System.out.println("这里是通过实现Runnable接口启动的新线程:" + Thread.currentThread().getName());
            });
            threadPoolExecutor.execute(thread);
        }
        //关闭线程池
        threadPoolExecutor.shutdown();
        //未将线程池关闭则死循环直至线程池关闭成功
        while (!threadPoolExecutor.isTerminated()) {
        }
        System.out.println("Finished all threads");
    }
}
```

##### **方式二：通过 `Executor` 框架的工具类 `Executors` 来实现** 我们可以创建三种类型的 `ThreadPoolExecutor`（**不推荐**；存在资源耗尽的风险）

#### 向线程池中提交任务

可以使用两个方法向线程池提交任务，分别为`execute()`和`submit()`方法。



`execute()`方法**用于提交不需要返回值的任务**，所以**无法判断任务是否被线程池执行成功**。

```java
public void execute(Runnable command) {
        if (command == null)
            throw new NullPointerException();
}
```



`submit()`方法用于**提交需要返回值的任务**。线程池**会返回一个`future`类型的对象**，通过这个future对象可以判断任务是否执行成功，并且**可以通过future的get()方法来获取返回值**，**`get()`方法会阻塞当前线程直到任务完成**，而使用get（long timeout，TimeUnit unit）方法则会阻塞当前线程一段时间后立即返回，这时候有可能任务没有执行完。

```java
Future<?> submit(Runnable task);
```

#### 关闭线程池

可以通过调用线程池的`shutdown()`或`shutdownNow()`方法来关闭线程池

- **`shutdown（）`** :关闭线程池，线程池的状态变为 `SHUTDOWN`。线程池不再接受新任务了，但是队列里的任务得执行完毕。

- **`shutdownNow（）`** :关闭线程池，线程的状态变为 `STOP`。线程池会终止当前正在运行的任务，并停止处理排队的任务并返回正在等待执行的 List。

```java
public List<Runnable> shutdownNow() {...}//线程池会终止当前正在运行的任务，并停止处理排队的任务并返回正在等待执行的 List。

public void shutdown() {...}//线程池不再接受新任务了，但是队列里的任务得执行完毕。
```

它们的**原理**是**遍历线程池中的工作线程**，然后**逐个调用线程的interrupt方法来中断线程**，所以**无法响应中断的任务可能永远无法终止**。

只要调用了这两个关闭方法中的任意一个，`isShutdown()`方法就会**返回true**。

当**所有的任务都已关闭后**，才表示**线程池关闭成功**，这时调用`isTerminaed()`方法会**返回true**。

```java
		//关闭线程池
        threadPoolExecutor.shutdown();
        //未将线程池关闭则死循环直至线程池关闭成功
        while (!threadPoolExecutor.isTerminated()) {
        }
        System.out.println("Finished all threads");
```

#### 几种常见的线程池

##### FixedThreadPool

`FixedThreadPool` 被称为**可重用固定线程数**的线程池。



源码可以看出新创建的 `FixedThreadPool` 的 `corePoolSize` 和 `maximumPoolSize` 都被设置为 **nThreads**，这个 nThreads 参数是我们使用的时候自己传递的。

```java
	/**
     * 创建一个可重用固定数量线程的线程池
     */
    public static ExecutorService newFixedThreadPool(int nThreads, ThreadFactory threadFactory) {
        return new ThreadPoolExecutor(nThreads, nThreads,
                                      0L, TimeUnit.MILLISECONDS,
                                      new LinkedBlockingQueue<Runnable>(),
                                      threadFactory);
    }
```

- 如果当前运行的线程数小于 corePoolSize， 如果再来新任务的话，就创建新的线程来执行任务；

- 当前运行的线程数等于 corePoolSize 后， 如果再来新任务的话，会将任务加入 `LinkedBlockingQueue`；

- 线程池中的线程执行完 手头的任务后，会在循环中反复从 `LinkedBlockingQueue` 中获取任务来执行；



![image-20230205144649029](/images/image-20230205144649029.png)



**为什么不推荐使用`FixedThreadPool`？**



**`FixedThreadPool` 使用无界队列 `LinkedBlockingQueue`（队列的容量为 Integer.MAX_VALUE）作为线程池的工作队列会对线程池带来如下影响 ：**

1. 当线程池中的线程数达到 `corePoolSize` 后，新任务将在无界队列中等待，因此线程池中的线程数不会超过 corePoolSize；
2. 由于使用无界队列时 `maximumPoolSize` 将是一个无效参数，因为不可能存在任务队列满的情况。所以，通过创建 `FixedThreadPool`的源码可以看出创建的 `FixedThreadPool` 的 `corePoolSize` 和 `maximumPoolSize` 被设置为同一个值。
3. 由于 1 和 2，使用无界队列时 `keepAliveTime` 将是一个无效参数；
4. 运行中的 `FixedThreadPool`（未执行 `shutdown()`或 `shutdownNow()`）不会拒绝任务，在任务比较多的时候**会导致 OOM（内存溢出）**。

##### SingleThreadExecutor 

`SingleThreadExecutor` 是**只有一个线程的线程池**

源代码可以看出新创建的 `SingleThreadExecutor` 的 `corePoolSize` 和 `maximumPoolSize` **都被设置为 1**.其他参数和 `FixedThreadPool` 相同

```java
	/**
     *返回只有一个线程的线程池
     */
    public static ExecutorService newSingleThreadExecutor(ThreadFactory threadFactory) {
        return new FinalizableDelegatedExecutorService
            (new ThreadPoolExecutor(1, 1,
                                    0L, TimeUnit.MILLISECONDS,
                                    new LinkedBlockingQueue<Runnable>(),
                                    threadFactory));
    }
```

- 如果当前运行的线程数少于 `corePoolSize`，则创建一个新的线程执行任务；

- 当前线程池中有一个运行的线程后，将任务加入 `LinkedBlockingQueue`

- 线程执行完当前的任务后，会在循环中反复从`LinkedBlockingQueue` 中获取任务来执行



![image-20230205144906373](/images/image-20230205144906373.png)

**为什么不推荐使用`SingleThreadExecutor`？**



`SingleThreadExecutor` **使用无界队列** `LinkedBlockingQueue` 作为线程池的工作队列（队列的容量为 Intger.MAX_VALUE）。`SingleThreadExecutor` 使用无界队列作为线程池的工作队列会对线程池带来的影响与 `FixedThreadPool` 相同。说简单点就是**可能会导致 OOM**，



##### CachedThreadPool

 `CachedThreadPool` 是一个会根**据需要创建新线程**的线程池



`CachedThreadPool` 的`corePoolSize` 被设置为空（0），`maximumPoolSize`被设置为 `Integer.MAX.VALUE`，即**最大线程数是无界**的，这也就意味着如果主线程提交任务的速度高于 `maximumPool` 中线程处理任务的速度时，`CachedThreadPool` 会不断创建新的线程。极端情况下，这样会导致耗尽 cpu 和内存资源



```java
	/**
     * 创建一个线程池，根据需要创建新线程，但会在先前构建的线程可用时重用它。
     */
    public static ExecutorService newCachedThreadPool(ThreadFactory threadFactory) {
        return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
                                      60L, TimeUnit.SECONDS,
                                      new SynchronousQueue<Runnable>(),
                                      threadFactory);
    }
```

1. 首先执行 `SynchronousQueue.offer(Runnable task)` 提交任务到任务队列。如果当前 `maximumPool` 中有闲线程正在执行 `SynchronousQueue.poll(keepAliveTime,TimeUnit.NANOSECONDS)`，那么主线程执行 offer 操作与空闲线程执行的 `poll` 操作配对成功，主线程把任务交给空闲线程执行，`execute()`方法执行完成，否则执行下面的步骤 2；
2. 当初始 `maximumPool` 为空，或者 `maximumPool` 中没有空闲线程时，将没有线程执行 `SynchronousQueue.poll(keepAliveTime,TimeUnit.NANOSECONDS)`。这种情况下，步骤 1 将失败，此时 `CachedThreadPool` 会创建新线程执行任务，execute 方法执行完成；

![image-20230205145227932](/images/image-20230205145227932.png)

 **为什么不推荐使用`CachedThreadPool`？**



`CachedThreadPool`允许创建的线程数量为 `Integer.MAX_VALUE` ，**可能会创建大量线程**，从而**导致 OOM**



##### ScheduledThreadPoolExecutor

**`ScheduledThreadPoolExecutor` 主要用来在给定的延迟后运行任务，或者定期执行任务。** 这个在实际项目中基本不会被用到，**也不推荐使用**，大家只需要简单了解一下它的思想即可



#### 合理地配置线程池

要想合理地配置线程池，就必须首先分析任务特性，可以从以下几个角度来分析。

- 任务的性质：**CPU密集型任务**、**IO密集型任务**和混合型任务。
- 任务的优先级：高、中和低。
- 任务的执行时间：长、中和短。
- 任务的依赖性：是否依赖其他系统资源，如数据库连接。



有一个简单并且适用面比较广的**经验之谈**：

- **CPU 密集型任务(N+1)：** 这种任务消耗的主要是 CPU 资源，可以将线程数设置为 N（CPU 核心数）+1，比 CPU 核心数多出来的一个线程是为了防止线程偶发的缺页中断，或者其它原因导致的任务暂停而带来的影响。一旦任务暂停，CPU 就会处于空闲状态，而在这种情况下多出来的一个线程就可以充分利用 CPU 的空闲时间。
- **I/O 密集型任务(2N)：** 这种任务应用起来，系统会用大部分的时间来处理 I/O 交互，而线程在处理 I/O 的时间段内不会占用 CPU 来处理，这时就可以将 CPU 交出给其它线程使用。因此在 I/O 密集型任务的应用中，我们可以多配置一些线程，具体的计算方法是 2N。

**如何判断是 CPU 密集任务还是 IO 密集任务？**

CPU 密集型简单理解就是利用 CPU 计算能力的任务比如你在内存中对大量数据进行排序。但凡涉及到网络读取，文件读取这类都是 IO 密集型，这类任务的特点是 CPU 计算耗费时间相比于等待 IO 操作完成的时间来说很少，大部分时间都花在了等待 IO 操作完成上。

#### 线程池的监控

监控线程池的时候可以使用以下属性。



- `taskCount`：线程池需要执行的任务数量。
- `completedTaskCount`：线程池在运行过程中已完成的任务数量，小于或等于taskCount。
- `largestPoolSize`：线程池里曾经创建过的最大线程数量。通过这个数据可以知道线程池是否曾经满过。如该数值等于线程池的最大大小，则表示线程池曾经满过。
- `getPoolSize`：线程池的线程数量。如果线程池不销毁的话，线程池里的线程不会自动销毁，所以这个大小只增不减。
- `getActiveCount`：获取活动的线程数。



通过扩展线程池进行监控。可以通过**继承线程池来自定义线程池**，**重写线程池**的`beforeExecute`、`afterExecute`和`terminated`方法，也可以在任务执行前、执行后和线程池关闭前执行一些代码来进行监控。例如，监控任务的平均执行时间、最大执行时间和最小执行时间等。这几个方法在线程池里是空方法。



### CompletableFuture异步编程

 Java 8 才被引入的一个非常有用的用于**异步编程的类**

```java
public class CompletableFuture<T> implements Future<T>, CompletionStage<T> {...}
```

**Future接口**

![image-20230204223419774](/images/image-20230204223419774.png)

- boolean `cancel(boolean mayInterruptIfRunning)` ：尝试取消执行任务。

- boolean `isCancelled()` ：判断任务是否被取消。

- boolean `isDone()` ： 判断任务是否已经被执行完成。

- `get()` ：等待任务执行完成并获取运算结果。会阻塞主线程

- `get(long timeout, TimeUnit unit)` ：多了一个超时时间。

**CompletionStage接口**

![image-20230204223644600](/images/image-20230204223644600.png)

`CompletionStage<T>` 接口中的方法比较多，`CompletableFuture` 的函数式能力就是这个接口赋予的。

**大量使用了 Java8 引入的函数式编程**



#### 创建 CompletableFuture

##### **一，通过 new 关键字。**

通过 new 关键字创建 `CompletableFuture` 对象这种使用方式可以看作是将 `CompletableFuture` 当做 `Future` 来使用。



```java
CompletableFuture completableFuture = new CompletableFuture();
```

##### **二，** 静态工厂方法

**基于 `CompletableFuture` 自带的静态工厂方法：`runAsync()` 、`supplyAsync()` 。**

###### `runAsync()` 无返回结果

```java
public static CompletableFuture<Void> runAsync(Runnable runnable,
                                                   Executor executor) {
    return asyncRunStage(screenExecutor(executor), runnable);
}
```

```java
public static ExecutorService threadPool = Executors.newFixedThreadPool(20);//指定线程池
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture.runAsync(()->{
            System.out.println("这里是通过CompletableFuture的静态方法runAsync启动的线程:" + Thread.currentThread().getName());
        },threadPool);
        
        threadPool.shutdown();
        while (!threadPool.isTerminated()){}//循环等待指导线程池关闭完成
        System.out.println("Finished all threads");
    }
```

###### `supplyAsync()` 有返回结果

```java
public static <U> CompletableFuture<U> supplyAsync(Supplier<U> supplier,
                                                       Executor executor) {
     return asyncSupplyStage(screenExecutor(executor), supplier);
}

public interface Supplier<T> {//有返回值的

    /**
     * Gets a result.
     *
     * @return a result
     */
    T get();
}
```

```java
public static ExecutorService threadPool = Executors.newFixedThreadPool(20);//指定线程池
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<String> supplyAsync = CompletableFuture.supplyAsync(() -> {
            return "Hello World";//有返回值
        }, threadPool);

        String result = supplyAsync.get();//获取线程执行后的返回值

        CompletableFuture.runAsync(()->{
            System.out.println(result);
        },threadPool);

        threadPool.shutdown();
        while (!threadPool.isTerminated()){}//循环等待指导线程池关闭完成
        System.out.println("Finished all threads");
    }
```

#### 处理异步结算的结果

- `thenApply()`进一步处理异步完成后的结果并返回处理结果
- `thenAccept()`进一步处理异步完成后的结果 无返回结果
- `thenRun()`进一步操作 无法获取异步完成后的结果 无返回结果
- `whenComplete()`进一步处理异步完成后的结果
  无法处理结果数据能够感知异常（`exceptionally()`可以感知到异常并对异常进行处理【当出现异常设置默认返回值】）并返回处理结果

```java
- `thenApply()`进一步处理异步完成后的结果并返回处理结果
- `thenAccept()`进一步处理异步完成后的结果 无返回结果
- `thenRun()`进一步操作 无法获取异步完成后的结果 无返回结果
    
public static ExecutorService threadPool = Executors.newFixedThreadPool(20);//指定线程池
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<String> supplyAsync = CompletableFuture.supplyAsync(() -> {
            return "Hello ";
        }, threadPool);
        supplyAsync.thenApply((result)->{return result + "World";})//进一步处理异步完成后的结果并返回处理结果
                .thenApply((result)->{return result + "--Eddie";})//进一步处理异步完成后的结果并返回处理结果
                
                .thenAccept(System.out::println)//进一步处理异步完成后的结果 无返回结果
                
                .thenRun(()->{//进一步操作 无法获取异步完成后的结果 无返回结果
                    System.out.println("我感知不到异步任务执行的任何结果");
                });

        threadPool.shutdown();
        while (!threadPool.isTerminated()){}//循环等待指导线程池关闭完成
        System.out.println("Finished all threads");
    }
```

```java
- `whenComplete()`进一步处理异步完成后的结果
无法处理结果数据能够感知异常（`exceptionally()`可以感知到异常并对异常进行处理【当出现异常设置默认返回值】）并返回处理结果
    
public static ExecutorService threadPool = Executors.newFixedThreadPool(20);//指定线程池
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        CompletableFuture<String> supplyAsync = CompletableFuture.supplyAsync(() -> {
            int num = 10 / 0;//模拟出现异常
            return "Hello ";
        }, threadPool);
        supplyAsync.whenComplete((result,exception)->{//当异步任务完成后
            System.out.println("上一步异步执行的结果是:" + result + "\t" + "上异步出现的异常是" + exception);
            //上一步异步执行的结果是:null	上异步出现的异常是java.util.concurrent.CompletionException: java.lang.ArithmeticException: / by zero
        }).exceptionally(throwable -> {//若异步任务完成时出现了异常
            System.out.println("出现的异常是" + throwable);
            //出现的异常是java.util.concurrent.CompletionException: java.lang.ArithmeticException: / by zero
            return "如果出现异常的话 这里返回一个默认值";
        }).thenAccept((result)->{
            System.out.println(result);//如果出现异常的话 这里返回一个默认值
        });

        threadPool.shutdown();
        while (!threadPool.isTerminated()){}//循环等待指导线程池关闭完成
        System.out.println("Finished all threads");
    }
```

#### 异步线程串行化

- `thenRunAsync`启动一个新的异步线程 串行上一个异步线程 无感知上个线程的结果 无返回结果
- `thenAcceptAsync`启动一个新的异步线程 串行并处理上个异步线程完成后的结果 无返回结果
- `thenApplyAsync`启动一个新的异步线程 串行并处理上个异步线程完成后的结果并返回处理结果

```java
一：`thenApplyAsync()`启动一个新的异步线程 串行并处理上个异步线程完成后的结果并返回处理结果
public <U> CompletionStage<U> thenApplyAsync
        (Function<? super T,? extends U> fn,
         Executor executor);
         
二：`thenAcceptAsync()`启动一个新的异步线程 串行并处理上个异步线程完成后的结果 无返回结果
public CompletionStage<Void> thenAcceptAsync(Consumer<? super T> action,
                                                 Executor executor);
    
三：`thenRunAsync()`启动一个新的异步线程 串行上一个异步线程 无感知上个线程的结果 无返回结果
public CompletionStage<Void> thenRunAsync(Runnable action,
                                              Executor executor);                                                 
```



#### 异常处理

- `handle()`处理任务执行过程中可能出现的抛出异常的情况
- `exceptionally()`可以感知到异常并对异常进行处理【当出现异常设置默认返回值】）并返回处理结果
- `completeExceptionally()`让结果就是异常

```java
一：`handle()`处理任务执行过程中可能出现的抛出异常的情况
    可以感知到异常并对异常进行处理【当出现异常设置默认返回值】）并返回处理结果
    
CompletableFuture<String> future
        = CompletableFuture.supplyAsync(() -> {
    if (true) {
        throw new RuntimeException("Computation error!");
    }
    return "hello!";
}).handle((res, ex) -> {
    // res 代表返回的结果
    // ex 的类型为 Throwable ，代表抛出的异常
    return res != null ? res : "world!";//若未出现异常则 返回正常返回结果 反之指定异常后返回的默认值
});

二：`exceptionally()`可以感知到异常并对异常进行处理【当出现异常设置默认返回值】）并返回处理结果
    
CompletableFuture<String> supplyAsync = CompletableFuture.supplyAsync(() -> {
            int num = 10 / 0;//模拟出现异常
            return "Hello ";
        }, threadPool);
        supplyAsync.whenComplete((result,exception)->{//当异步任务完成后
            System.out.println("上一步异步执行的结果是:" + result + "\t" + "上异步出现的异常是" + exception);
            //上一步异步执行的结果是:null	上异步出现的异常是java.util.concurrent.CompletionException: java.lang.ArithmeticException: / by zero
        }).exceptionally(throwable -> {//若异步任务完成时出现了异常
            System.out.println("出现的异常是" + throwable);
            //出现的异常是java.util.concurrent.CompletionException: java.lang.ArithmeticException: / by zero
            return "如果出现异常的话 这里返回一个默认值";
        }).thenAccept((result)->{
            System.out.println(result);//如果出现异常的话 这里返回一个默认值
        });

三：`completeExceptionally()`让结果就是异常
    
CompletableFuture<String> completableFuture = new CompletableFuture<>();
// ...
completableFuture.completeExceptionally(
  new RuntimeException("Calculation failed!"));
// ...
completableFuture.get(); // ExecutionException

```

#### 组合两个CompletableFuture

- `thenComposeAsync`**按顺序链接**两个 `CompletableFuture` 对象;**将前一个任务的返回结果作为下一个任务的参数**，它们之间存在着先后顺序
- `thenCombineAsync`会**在两个任务都执行完成后**，把**两个任务的结果处理后返回一个结果**。两个任务是并行执行的，它们之间并**没有先后依赖顺序**

**两个都完成**

- `runAfterBothAsync`两个异步线程都执行完后进行一些操作处理 **无法感知**两个线程的**执行结果** **无返回值**
- `thenAcceptBothAsync`两个异步线程都执行完后进行一些操作处理 **能够感知**两个线程的**执行结果** **无返回值**

**任一完成**

- `applyToEitherAsync`任意一个异步线程执行完成后进行一些操作处理 **能够感知**两个线程的**执行结果** **返回一个结果**
- `acceptEitherAsync`任意一个异步线程执行完成后进行一些操作处理 **能够感知**两个线程的**执行结果** **无返回值**
- `runAfterEitherAsync`任意一个异步线程执行完成后进行一些操作处理 **无法感知**两个线程的**执行结果** **无返回值**

#### 并行运行多个 CompletableFuture

可以通过 `CompletableFuture` 的 `allOf()`/`anyOf()`静态方法来并行运行多个 `CompletableFuture`

- `allOf()`**等到所有的 `CompletableFuture` 都运行完成之后再返回**
- 若线程A和B调用 `join()` 可以让程序等A和B线程 都运行完了之后再继续执行
- `anyOf()`**不会等待所有的 `CompletableFuture` 都运行完成之后再返回，只要有一个执行完成即可！**

```java
- 调用 `allOf()`**等到所有的 `CompletableFuture` 都运行完成之后再返回**
CompletableFuture<Void> task1 =
  CompletableFuture.supplyAsync(()->{
    //自定义业务操作
  });
......
CompletableFuture<Void> task6 =
  CompletableFuture.supplyAsync(()->{
    //自定义业务操作
  });
......
 CompletableFuture<Void> headerFuture=CompletableFuture.allOf(task1,.....,task6);//指定多个异步线程

  try {
    headerFuture.join();
  } catch (Exception ex) {
    ......
  }
System.out.println("all done. ");

- 调用 `join()` 可以让程序等`future1` 和 `future2` 都运行完了之后再继续执行
    
CompletableFuture<Void> completableFuture = CompletableFuture.allOf(future1, future2);
completableFuture.join();
assertTrue(completableFuture.isDone());
System.out.println("all futures done...");

- 调用 `anyOf()`**不会等待所有的 `CompletableFuture` 都运行完成之后再返回，只要有一个执行完成即可！**
CompletableFuture<Object> f = CompletableFuture.anyOf(future1, future2);
System.out.println(f.get());
```


