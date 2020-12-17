---

layout: post

title:  "ERROR: Unable to find the resource: /META-INF/BenchmarkList"

date:   2020-12-17 14:00:00 +0800

categories: gradle、jmh

---

<br>

##### 我是想着用 benchmark 测试项目的。使用的是 jmh，gradle 做为构建工具。在 run 的时候，报出以下错误

```
4:22:37 下午: Executing task 'QuickStart.main()'...


> Configure project :
Hello Jmh-Demo.
> Task :compileJava NO-SOURCE
> Task :processResources NO-SOURCE
> Task :classes UP-TO-DATE
> Task :compileTestJava
> Task :processTestResources NO-SOURCE
> Task :testClasses

> Task :QuickStart.main() FAILED
net.yisasin.jmh.QuickStart

Deprecated Gradle features were used in this build, making it incompatible with Gradle 7.0.
Use '--warning-mode all' to show the individual deprecation warnings.
See https://docs.gradle.org/6.4.1/userguide/command_line_interface.html#sec:command_line_warnings
2 actionable tasks: 2 executed
Exception in thread "main" java.lang.RuntimeException: ERROR: Unable to find the resource: /META-INF/BenchmarkList
	at org.openjdk.jmh.runner.AbstractResourceReader.getReaders(AbstractResourceReader.java:98)
	at org.openjdk.jmh.runner.BenchmarkList.find(BenchmarkList.java:122)
	at org.openjdk.jmh.runner.Runner.internalRun(Runner.java:263)
	at org.openjdk.jmh.runner.Runner.run(Runner.java:209)
	at net.yisasin.jmh.QuickStart.main(QuickStart.java:51)

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':QuickStart.main()'.
> Process 'command '/Library/Java/JavaVirtualMachines/jdk1.8.0_241.jdk/Contents/Home/bin/java'' finished with non-zero exit value 1

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 287ms
4:22:37 下午: Task execution finished 'QuickStart.main()'.
```

##### 解决方法

在 `build.gradle` 脚本中添加依赖
``
testAnnotationProcessor "org.openjdk.jmh:jmh-generator-annprocess:1.21"
```

---

参考

- [https://stackoverflow.com/questions/47708578/error-unable-to-find-the-resource-meta-inf-benchmarklist-when-running-jmh-wit](https://stackoverflow.com/questions/47708578/error-unable-to-find-the-resource-meta-inf-benchmarklist-when-running-jmh-wit)
