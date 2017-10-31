                                            JDK 源码个人学习
	JDK中有很多类是学习java的基础，是基础类，比如Runtime类；每一个基础类必须学好才能更好的理解java，现在就来对java.lang.Runtime进行学习。
	Runtime类封装了运行时环境，每一个java应用程序都有一个Runtime实例，把运行环境和程序连接起来。
	查看java API可以知道，Runtime类没有构造方法，也就是不能直接创建一个Runtime的实例，而是通过其方法getRuntime获得Runtime的实例，通过这个引用就可以使用方法获得java虚拟机的状态和行为。
	1）API一些方法解释
	addShutdownHook(Thread hook) 
      注册新的虚拟机来关闭挂钩
	availableProcessors() 
      向 Java 虚拟机返回可用处理器的数目。 
    exec(String command) 
      在单独的进程中执行指定的字符串命令。 
    exec(String[] cmdarray) 
      在单独的进程中执行指定命令和变量。 
    exec(String[] cmdarray, String[] envp) 
      在指定环境的独立进程中执行指定命令和变量。 
    exec(String[] cmdarray, String[] envp, File dir) 
      在指定环境和工作目录的独立进程中执行指定的命令和变量。 
    exec(String command, String[] envp) 
      在指定环境的单独进程中执行指定的字符串命令。 
    exec(String command, String[] envp, File dir) 
      在有指定环境和工作目录的独立进程中执行指定的字符串命令。 
    exit(int status) 
      通过启动虚拟机的关闭序列，终止当前正在运行的 Java 虚拟机。 
    freeMemory() 
      返回 Java 虚拟机中的空闲内存量。 
    gc() 
      运行垃圾回收器。 
    InputStream getLocalizedInputStream(InputStream in) 
      已过时。 从 JDK 1.1 开始，将本地编码字节流转换为 Unicode 字符流的首选方法是使用 InputStreamReader 和 BufferedReader 类。 
    OutputStream getLocalizedOutputStream(OutputStream out) 
      已过时。 从 JDK 1.1 开始，将 Unicode 字符流转换为本地编码字节流的首选方法是使用 OutputStreamWriter、BufferedWriter 和 PrintWriter 类。 
    getRuntime() 
      返回与当前 Java 应用程序相关的运行时对象。 
    halt(int status) 
      强行终止目前正在运行的 Java 虚拟机。 
    load(String filename) 
      加载作为动态库的指定文件名。 
    loadLibrary(String libname) 
      加载具有指定库名的动态库。 
    maxMemory() 
      返回 Java 虚拟机试图使用的最大内存量。 
    removeShutdownHook(Thread hook) 
      取消注册某个先前已注册的虚拟机关闭挂钩。 
    runFinalization() 
      运行挂起 finalization 的所有对象的终止方法。 
    runFinalizersOnExit(value) 
      已过时。 此方法本身具有不安全性。它可能对正在使用的对象调用终结方法，而其他线程正在操作这些对象，从而导致不正确的行为或死锁。 
    totalMemory() 
      返回 Java 虚拟机中的内存总量。 
    traceInstructions(on) 
      启用／禁用指令跟踪。 
    traceMethodCalls(on) 
      启用／禁用方法调用跟踪
	2）常见应用--内存管理
	java提供了无用单元收集机制，通过方法totalMemory()和freeMemory()分别获得java虚拟机堆内存总量和空闲内存量，
	java会周期性的回收垃圾对象，释放内存空间；
	3）常见应用--执行其它程序
	通过如上的exec()方法执行，参数不一样；就像前面介绍的，该方法将应用程序和当前环境连接起来，exec方法的本质依赖当前环境，windows环境和linux环境命令不一样，
	//windows执行运行记事本
	Runtime.getRuntime().exec("notepad");
	//linux环境执行创建文件夹,对所有人开放
	Runtime.getRuntime().exec("chmod -R 777"+文件绝对路劲)
	从API中可以看出其中的很多方法都是返回Process对象，它位于java.lang中，可以参考API查看方法 