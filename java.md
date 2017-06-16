// AtomicLong原子量,java6中的新东西。有兴趣研究线程的时候在学。这里用它了自增一个id
private final AtomicLong counter = new AtomicLong();
counter.incrementAndGet()
