# ThreadPoolExecutor源码分析

```java
private static final int COUNT_BITS = Integer.SIZE - 3;
private static final int CAPACITY   = (1 << COUNT_BITS) - 1;

// runState is stored in the high-order bits
private static final int RUNNING    = -1 << COUNT_BITS;
private static final int SHUTDOWN   =  0 << COUNT_BITS;
private static final int STOP       =  1 << COUNT_BITS;
private static final int TIDYING    =  2 << COUNT_BITS;
private static final int TERMINATED =  3 << COUNT_BITS;
```

`runState`因为有5个状态 所以需要使用3个bit位来表示（1个bit位可以代表2个状态 所以需要3个bit位才能表示) 使用`int`的高3位来表示线程池的状态 这是一个好的设计思想
只有`RUNING`状态为负数 所以要判断线程池的状态时，只要为负数就表示当前处于运行中的状态
