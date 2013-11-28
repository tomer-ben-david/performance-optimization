Profiling & Performance analysis


Introduction

Having performance issues? Here is a set of tips which hopefully get the performance issues and you farther away, and you and performance optimization much closer.  I have gathered this set of tips while profiling a java server, researching and resolving the performance bottlenecks.

Once you get to a performance optimization scenario you may ask yourself whether you should have done early performance optimization, and whether if you have done them you would not reach a state where you need to optimize yours server, however, there is the notion that premature optimizations should be avoided, while I tend to agree with it there is a limit to it; the limit is that your design should not prevent or at least make it easy for the tweaks when needed plus the design should take into account scalability and performance beforehand.  ie. Using plain json as a communication protocol between servers may be very human readable and easy to debug, but may have a large impact on performance if not done correctly, a solution to that can be mutl protocol communciation layer, be it json, protobuf, toggle to plain json for debugging and for protobuf for perofrmance.

Here we will investigate a case where our code already has some performance issues and we want to fix them. 

With that process I leanred some tips and best practices which I would like to share with you.  In this post I will gather some tips and best practices for performance analysis and load tests on a server on linux platform.
https://docs.google.com/a/liveperson.com/presentation/d/1Uzm-P0MGNk4YzR82yzX_5Bs06FcBhitV2vdI6q6UgPg/edit#slide=id.ge5438e7a_280
Content
User CPU / System CPU, CPU load average
Network kb load
top, sar, network sniffing (tcpflow/dump), 
req/sec tomcat
Apache Bench, JMeter (client,server,graph)
jstack, jmap, hprof
Metrics, Java Melody
JProfiler, YJP, VisualVM
CPU
http://nurkiewicz.blogspot.co.il/2012/08/which-java-thread-consumes-my-cpu.html

When you profile a server in a search of high cpu consumption areas you should first understand which cpu consumption are you looking at.  Using the tools shown below note that its possible to check out the user cpu and system cpu.  Its important to understand the differences between the two.  The user cpu is the cpu as directly consumed by apps running on linux, some of the app calls would be directed into the kernel for kernel services and operations.  The cpu used by the kernel is called system cpu.

lets start by running sar command to check out the cpu on a linux machine.  (I will describe further in more details the sar command, for now, flow with me..)

I'm going to use the following servlet app on tomcat7 for tests:

https://github.com/spray/spray/tree/master/examples/spray-servlet




