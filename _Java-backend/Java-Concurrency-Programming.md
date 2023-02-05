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

## 线程基础

## JUC(Java Util Concurrency)

### Java 线程池

**池化技术的思想**主要是为了**减少每次获取资源的消耗**，**提高对资源的利用率**

- **降低资源消耗**。通过重复利用已创建的线程降低线程创建和销毁造成的消耗。

- **提高响应速度**。当任务到达时，任务可以不需要等到线程创建就能立即执行。

- **提高线程的可管理性**。线程是稀缺资源，如果无限制的创建，不仅会消耗系统资源，还会降低系统的稳定性，使用线程池可以进行统一的分配，调优和监控。

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



### CompletableFuture异步编程

 Java 8 才被引入的一个非常有用的用于**异步编程的类**

```java
public class CompletableFuture<T> implements Future<T>, CompletionStage<T> {...}
```

#### **Future接口**

![image-20230204223419774](/images/image-20230204223419774.png)

- boolean `cancel(boolean mayInterruptIfRunning)` ：尝试取消执行任务。

- boolean `isCancelled()` ：判断任务是否被取消。

- boolean `isDone()` ： 判断任务是否已经被执行完成。

- `get()` ：等待任务执行完成并获取运算结果。

- `get(long timeout, TimeUnit unit)` ：多了一个超时时间。

#### CompletionStage接口

![image-20230204223644600](/images/image-20230204223644600.png)

`CompletionStage<T>` 接口中的方法比较多，`CompletableFuture` 的函数式能力就是这个接口赋予的。

**大量使用了 Java8 引入的函数式编程**



#### 创建 CompletableFuture

**一，通过 new 关键字。**

通过 new 关键字创建 `CompletableFuture` 对象这种使用方式可以看作是将 `CompletableFuture` 当做 `Future` 来使用。





**二，基于 `CompletableFuture` 自带的静态工厂方法：`runAsync()` 、`supplyAsync()` 。**



