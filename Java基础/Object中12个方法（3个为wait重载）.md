1. clone方法:保护方法，实现对象的浅复制，只有实现了Cloneable接口才可以调用该方法，否则抛出CloneNotSupportedException异常。
2. toString方法:通常，toString 方法会返回一个“以文本方式表示”此对象的字符串。结果应是一个简明但易于读懂。建议所有子类都重写此方法。Object 类的 toString 方法返回一个字符串，该字符串由类名（对象是该类的一个实例）、at 标记符“@”和此对象哈希码的无符号十六进制表示组成。换句话说，该方法返回一个字符串，它的值等于：getClass().getName() + '@' + Integer.toHexString(hashCode())
3. getClass方法:final方法:获得运行时类型。该 Class 对象是由所表示类的 static synchronized 方法锁定的对象。返回：表示该对象的运行时类的 java.lang.Class 对象。此结果属于类型 Class<? extends X>，其中 X 表示清除表达式中的静态类型，该表达式调用 getClass。
4. finalize方法:该方法用于释放资源。因为无法确定该方法什么时候被调用，很少使用。
5. equals方法:该方法是非常重要的一个方法。一般equals和==是不一样的，但是在Object中两者是一样的。子类一般都要重写这个方法。
6. hashCode方法:支持该方法是为哈希表提供一些优点, 用于哈希查找，重写了equals方法一般都要重写hashCode方法。这个方法在一些具有哈希功能的Collection中用到。一般必须满足obj1.equals(obj2)==true。可以推出obj1.hash- Code()==obj2.hashCode()，但是hashCode相等不一定就满足equals。不过为了提高效率，应该尽量使上面两个条件接近等价。

7. wait方法:
- wait(long timeout)在其他线程调用此对象的 notify() 方法或 notifyAll() 方法，或者超过指定的时间量前，导致当前线程等待。
- wait(long timeout, int nanos) 在其他线程调用此对象的 notify() 方法或 notifyAll() 方法，或者其他某个线程中断当前线程，或者已超过某个实际时间量前，导致当前线程等待。
- wait()用于让当前线程失去操作权限，当前线程进入等待序列

    wait方法就是使当前线程等待该对象的锁，当前线程必须是该对象的拥有者，也就是具有该对象的锁。wait()方法一直等待，直到获得锁或者被中断。wait(long       timeout)设定一个超时间隔，如果在规定时间内没有获得锁就返回。
    调用该方法后当前线程进入睡眠状态，直到以下事件发生。
（1）其他线程调用了该对象的notify方法。
（2）其他线程调用了该对象的notifyAll方法。
（3）其他线程调用了interrupt中断该线程。
（4）时间间隔到了。
此时该线程就可以被调度了，如果是被中断的话就抛出一个InterruptedException异常。

8. notify方法:该方法唤醒在该对象上等待的某个线程。

9. notifyAll方法:该方法唤醒在该对象上等待的所有线程。

10.  registerNatives()
私有方法, 通常情况下，为了使JVM发现您的本机功能，他们被一定的方式命名
