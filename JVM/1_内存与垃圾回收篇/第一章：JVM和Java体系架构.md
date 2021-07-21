### 文章目录

- [1.jvm前言](https://blog.csdn.net/sj15814963053/article/details/109767096#1jvm_6)
- [2.开发人员的病态](https://blog.csdn.net/sj15814963053/article/details/109767096#2_19)
- [3.架构师在想什么](https://blog.csdn.net/sj15814963053/article/details/109767096#3_29)
- [4.为什么学习jvm](https://blog.csdn.net/sj15814963053/article/details/109767096#4jvm_48)
- [5.Java VS C++](https://blog.csdn.net/sj15814963053/article/details/109767096#5Java_VS_C_56)
- [6.TIOBE 排行榜](https://blog.csdn.net/sj15814963053/article/details/109767096#6TIOBE__65)
- [7.Java 生态圈](https://blog.csdn.net/sj15814963053/article/details/109767096#7Java__73)
- [8.Java的跨平台性](https://blog.csdn.net/sj15814963053/article/details/109767096#8Java_86)
- [9.字节码](https://blog.csdn.net/sj15814963053/article/details/109767096#9_96)
- [10.多语言混合编程](https://blog.csdn.net/sj15814963053/article/details/109767096#10_106)
- [11.自己写个jvm](https://blog.csdn.net/sj15814963053/article/details/109767096#11jvm_114)
- [12.Java的重大事件](https://blog.csdn.net/sj15814963053/article/details/109767096#12Java_124)
- [13.虚拟机介绍](https://blog.csdn.net/sj15814963053/article/details/109767096#13_151)
- - [13.1 虚拟机概念](https://blog.csdn.net/sj15814963053/article/details/109767096#131__153)
  - [13.2 Java虚拟机](https://blog.csdn.net/sj15814963053/article/details/109767096#132_Java_163)
- [14.jvm的位置](https://blog.csdn.net/sj15814963053/article/details/109767096#14jvm_178)
- [15.jvm的整体结构](https://blog.csdn.net/sj15814963053/article/details/109767096#15jvm_190)
- [16.Java代码执行流程](https://blog.csdn.net/sj15814963053/article/details/109767096#16Java_201)
- [17.JVM架构模型](https://blog.csdn.net/sj15814963053/article/details/109767096#17JVM_207)
- - [17.1 两种架构的举例](https://blog.csdn.net/sj15814963053/article/details/109767096#171__225)
  - [17.2 反编译字节码文件](https://blog.csdn.net/sj15814963053/article/details/109767096#172__251)
  - [17.3 总结](https://blog.csdn.net/sj15814963053/article/details/109767096#173__306)
- [18.jvm生命周期](https://blog.csdn.net/sj15814963053/article/details/109767096#18jvm_316)
- 20.相关jvm介绍



------

# 1.jvm前言

> 作为Java工程师的你曾被伤害过吗？你是否也遇到过这些问题？

- 运行着的线上系统突然卡死，系统无法访问，甚至直接OOM！
- 想解决线上JVM GC问题，但却无从下手。
- 新项目上线，对各种JVM参数设置一脸茫然，直接默认吧然后就GG了
- 每次面试之前都要重新背一遍JVM的一些原理概念性的东西，然而面试官却经常问你在实际项目中如何调优VM参数，如何解决GC、OOM等问题，一脸懵逼。

![image-20200727120903847](https://img-blog.csdnimg.cn/img_convert/feeab72bc683a4d5f8aca0356517facb.png)

# 2.开发人员的病态

- 大部分Java开发人员，除了会在项目中使用到与Java平台相关的各种高精尖技术，对于Java技术的核心Java虚拟机了解甚少。
- 一些有一定工作经验的开发人员，打心眼儿里觉得SSM、微服务等上层技术才是重点，基础技术并不重要，这其实是一种本末倒置的“病态”。如果我们把核心类库的API比做数学公式的话，那么Java虚拟机的知识就好比公式的推导过程。
- 计算机系统体系对我们来说越来越远，在不了解底层实现方式的前提下，通过高级语言很容易编写程序代码。但事实上计算机并不认识高级语言

![image-20200727120922348](https://img-blog.csdnimg.cn/img_convert/35446ef9b0c85159e0c7bae9cc94add8.png)

# 3.架构师在想什么

> 架构师每天都在思考什么？

1. 应该如何让我的系统更快？
2. 如何避免系统出现瓶颈？

> 知乎上有条帖子：应该如何看招聘信息，直通年薪50万+？

- 参与现有系统的性能优化，重构，保证平台性能和稳定性
- 根据业务场景和需求，决定技术方向，做技术选型
- 能够独立架构和设计海量数据下高并发分布式解决方案，满足功能和非功能需求
- 解决各类潜在系统风险，核心功能的架构与代码编写
- 分析系统瓶颈，解决各种疑难杂症，性能调优等

# 4.为什么学习jvm

1. 面试的需要（BATJ、TMD，PKQ等面试都爱问）
2. 中高级程序员必备技能：项目管理、调优的需求
3. 追求极客的精神，比如：垃圾回收算法、JIT（即时编译器）、底层原理

# 5.Java VS C++

- 垃圾收集机制为我们打理了很多繁琐的工作，大大提高了开发的效率，但是，垃圾收集也不是万能的，懂得JVM内部的内存结构、工作机制，是设计高扩展性应用和诊断运行时问题的基础，也是Java工程师进阶的必备能力。
- C语言需要自己来分配内存和回收内存，Java全部交给JVM进行分配和回收。

![image-20200727121203443](https://img-blog.csdnimg.cn/img_convert/9f427cf534a30187ca8d212587d2c42c.png)

# 6.TIOBE 排行榜

**TIOBE 排行榜**：https://www.tiobe.com/tiobe-index/

![image-20201117235942570](https://img-blog.csdnimg.cn/img_convert/facedd2997fe925cf071f2ee2fe084c4.png)

# 7.Java 生态圈

Java是目前应用最为广泛的软件开发平台之一。随着Java以及Java社区的不断壮大Java 也早已不再是简简单单的一门计算机语言了，它更是一个平台、一种文化、一个社区。

- 作为一个平台，Java虚拟机扮演着举足轻重的作用
  - Groovy、Scala、JRuby、Kotlin等都是Java平台的一部分
- 作为一种文化，Java几乎成为了"开源"的代名词。
  - 第三方开源软件和框架。如Tomcat、Struts，MyBatis，Spring等。
  - 就连JDK和JVM自身也有不少开源的实现，如openJDK、Harmony。
- 作为一个社区，Java拥有全世界最多的技术拥护者和开源社区支持，有数不清的论坛和资料。从桌面应用软件、嵌入式开发到企业级应用、后台服务器、中间件，都可以看到Java的身影。其应用形式之复杂、参与人数之众多也令人咋舌。

# 8.Java的跨平台性

- 每个语言都需要转换成字节码文件，最后转换的字节码文件都能通过Java虚拟机进行运行和处理
- 随着Java7的正式发布，Java虚拟机的设计者们通过JSR-292规范基本实现在Java虚拟机平台上运行非Java语言编写的程序。
- Java虚拟机根本不关心运行在其内部的程序到底是使用何种编程语言编写的，它只关心“字节码”文件。也就是说Java虚拟机拥有语言无关性，并不会单纯地与Java语言“终身绑定”，只要其他编程语言的编译结果满足并包含Java虚拟机的内部指令集、符号表以及其他的辅助信息，它就是一个有效的字节码文件，就能够被虚拟机所识别并装载运行。

![image-20200727121755076](https://img-blog.csdnimg.cn/img_convert/f216e3a1e22e770179adf8cd6fd07700.png)

就是java程序经过编译后生成字节码文件在不同平台上解释运行。

所有的java虚拟机都遵循规范

# 9.字节码

- 我们平时说的java字节码，指的是用java语言编译成的字节码。准确的说任何能在jvm平台上执行的字节码格式都是一样的。所以应该统称为：`jvm字节码`。
- 不同的编译器，可以编译出相同的字节码文件，字节码文件也可以在不同的JVM上运行。
- Java虚拟机与Java语言并没有必然的联系，它只与特定的二进制文件格式——Class文件格式所关联，Class文件中包含了Java虚拟机指令集（或者称为字节码、Bytecodes）和符号表，还有一些其他辅助信息。

![image-20200727121725188](https://img-blog.csdnimg.cn/img_convert/a74cf3af2cc388c272c7d1ed74c50bf3.png)

**由上图可得，java虚拟机不止用来解释运行java生成的字节码文件，只要该语言被各自编译后生成的字节码文件遵循java虚拟机的规范都可以。**



# 10.多语言混合编程

- `Java平台上的多语言混合编程正成为主流，通过特定领域的语言去解决特定领域的问题是当前软件开发应对日趋复杂的项目需求的一个方向`。
- 试想一下，在一个项目之中，并行处理用Clojure语言编写，展示层使用JRuby/Rails，中间层则是Java，每个应用层都将使用不同的编程语言来完成，而且，接口对每一层的开发者都是透明的，各种语言之间的交互不存在任何困难，就像使用自己语言的原生API一样方便，因为它们最终都运行在一个虚拟机之上。
- 对这些运行于Java虚拟机之上、Java之外的语言，来自系统级的、底层的支持正在迅速增强，以JSR-292为核心的一系列项目和功能改进（如DaVinci Machine项目、Nashorn引擎、InvokeDynamic指令、java.lang.invoke包等），`推动Java虚拟机从"Java语言的虚拟机"向"多语言虚拟机"的方向发展`。

# 11.自己写个jvm

- Java虚拟机非常复杂，要想真正理解它的工作原理，最好的方式就是自己动手编写一个！
- 自己动手写一个Java虚拟机，难吗？
- 天下事有难易乎？为之，则难者亦易矣；不为，则易者亦难矣

![image-20200727122014010](file:///A:/%E5%B0%9A%E7%A1%85%E8%B0%B7/Jvm/%E5%8D%9A%E5%AE%A2%E7%BD%91%E9%A1%B5/(26%E6%9D%A1%E6%B6%88%E6%81%AF)%20%E7%AC%AC%E4%B8%80%E7%AB%A0%20JVM%E5%92%8CJava%E4%BD%93%E7%B3%BB%E6%9E%B6%E6%9E%84_JavaAlenboy-CSDN%E5%8D%9A%E5%AE%A2_files/ec969bca432daa43278bb9cbaf6ff7a2.png)

# 12.Java的重大事件

- 1990年，在Sun计算机公司中，由Patrick Naughton、MikeSheridan及James Gosling领导的小组Green Team，开发出的新的程序语言，命名为Oak，后期命名为Java
- 1995年，Sun正式发布Java和HotJava产品，Java首次公开亮相。
- 1996年1月23日Sun Microsystems发布了JDK 1.0。
- 1998年，JDK1.2版本发布。同时，Sun发布了JSP/Servlet、EJB规范，以及将Java分成了J2EE、J2SE和J2ME。这表明了Java开始向企业、桌面应用和移动设备应用3大领域挺进。
- 2000年，JDK1.3发布，Java HotSpot Virtual Machine正式发布，成为Java的默认虚拟机。
- 2002年，JDK1.4发布，古老的Classic虚拟机退出历史舞台。
- 2003年年底，Java平台的scala正式发布，同年Groovy也加入了Java阵营。
- 2004年，JDK1.5发布。同时JDK1.5改名为JavaSE5.0。
- 2006年，JDK6发布。同年，Java开源并建立了OpenJDK。顺理成章，Hotspot虚拟机也成为了OpenJDK中的默认虚拟机。
- 2007年，Java平台迎来了新伙伴Clojure。
- 2008年，oracle收购了BEA，得到了JRockit虚拟机。
- 2009年，Twitter宣布把后台大部分程序从Ruby迁移到Scala，这是Java平台的又一次大规模应用。
- 2010年，Oracle收购了Sun，获得Java商标和最真价值的HotSpot虚拟机。此时，Oracle拥有市场占用率最高的两款虚拟机HotSpot和JRockit，并计划在未来对它们进行整合：HotRockit
- 2011年，JDK7发布。在JDK1.7u4中，正式启用了新的垃圾回收器G1。
- 2017年，JDK9发布。将G1设置为默认GC，替代CMS
- 同年，IBM的J9开源，形成了现在的Open J9社区
- 2018年，Android的Java侵权案判决，Google赔偿Oracle计88亿美元（**法务人员比开发人员更牛逼**）。
- 同年，Oracle宣告JavagE成为历史名词JDBC、JMS、Servlet赠予Eclipse基金会
- 同年，JDK11发布，LTS版本的JDK，**发布革命性的ZGC**，调整JDK授权许可
- 2019年，JDK12发布，加入RedHat领导开发的Shenandoah GC（美国的一个河流命令，首个非Sun公司发布的）
- 现在JDK最新是JDK13。

![image-20200727123230088](file:///A:/%E5%B0%9A%E7%A1%85%E8%B0%B7/Jvm/%E5%8D%9A%E5%AE%A2%E7%BD%91%E9%A1%B5/(26%E6%9D%A1%E6%B6%88%E6%81%AF)%20%E7%AC%AC%E4%B8%80%E7%AB%A0%20JVM%E5%92%8CJava%E4%BD%93%E7%B3%BB%E6%9E%B6%E6%9E%84_JavaAlenboy-CSDN%E5%8D%9A%E5%AE%A2_files/fe9e92090d381be838f06c0504f92db5.png)

商用版本比开放版本内容还要少一些。





# 13.虚拟机介绍

## 13.1 虚拟机概念

所谓虚拟机（Virtual Machine），就是一台`虚拟的计算机`。它是一款`软件`，用来执行一系列虚拟计算机指令。

大体上，虚拟机可以分为`系统虚拟机`和`程序虚拟机`。

- 大名鼎鼎的Virtual Box，VMware就属于系统虚拟机，它们完全是对物理计算机的仿真，提供了一个可运行完整操作系统的软件平台。
- 程序虚拟机的典型代表就是`Java虚拟机`，它专门为执行单个计算机程序而设计，在Java虚拟机中执行的指令我们称为Java字节码指令。
- 无论是系统虚拟机还是程序虚拟机，在上面运行的软件都被限制于虚拟机提供的资源中。

## 13.2 Java虚拟机

- Java虚拟机是一台执行Java字节码的虚拟计算机，它拥有独立的运行机制，其运行的Java字节码也未必由Java语言编译而成。
- JVM平台的各种语言可以共享Java虚拟机带来的跨平台性、优秀的垃圾回器，以及可靠的即时编译器。
- Java技术的核心就是Java虚拟机（JVM，Java Virtual Machine），因为所有的Java程序都运行在Java虚拟机内部。
- Java虚拟机就是二进制字节码的运行环境，负责装载字节码到其内部，解释/编译为对应平台上的机器指令执行。每一条Java指令，Java虚拟机规范中都有详细定义，如怎么取操作数，怎么处理操作数，处理结果放在哪里。（这点跟计算机组成原理学过的一致，本质上都是一样的）

> 特点

1. `一次编译，到处运行`
2. `自动内存管理`
3. `自动垃圾回收功能`

# 14.jvm的位置

> **JVM是运行在操作系统之上的**，它与硬件没有直接的交互

![image-20201118090425668](file:///A:/%E5%B0%9A%E7%A1%85%E8%B0%B7/Jvm/%E5%8D%9A%E5%AE%A2%E7%BD%91%E9%A1%B5/(26%E6%9D%A1%E6%B6%88%E6%81%AF)%20%E7%AC%AC%E4%B8%80%E7%AB%A0%20JVM%E5%92%8CJava%E4%BD%93%E7%B3%BB%E6%9E%B6%E6%9E%84_JavaAlenboy-CSDN%E5%8D%9A%E5%AE%A2_files/336a400ae9e87411ec1fa9151316f40e.png)

> Java的体系结构

![image-20201118090556097](file:///A:/%E5%B0%9A%E7%A1%85%E8%B0%B7/Jvm/%E5%8D%9A%E5%AE%A2%E7%BD%91%E9%A1%B5/(26%E6%9D%A1%E6%B6%88%E6%81%AF)%20%E7%AC%AC%E4%B8%80%E7%AB%A0%20JVM%E5%92%8CJava%E4%BD%93%E7%B3%BB%E6%9E%B6%E6%9E%84_JavaAlenboy-CSDN%E5%8D%9A%E5%AE%A2_files/4a1e986875b97026f5cb9ef32aff07c9.png)



java源代码首先被前端编译器编译成字节码文件

# 15.jvm的整体结构

- `HotSpot VM`是目前市面上高性能虚拟机的代表作之一。
- 它采用解释器与即时编译器并存的架构。
- 在今天，Java程序的运行性能早已脱胎换骨，已经达到了可以和C/C++程序一较高下的地步。
- 执行引擎包含三部分：`解释器`，`即时编译器`，`垃圾回收器`
- 

![image-20200727132330682](file:///A:/%E5%B0%9A%E7%A1%85%E8%B0%B7/Jvm/%E5%8D%9A%E5%AE%A2%E7%BD%91%E9%A1%B5/(26%E6%9D%A1%E6%B6%88%E6%81%AF)%20%E7%AC%AC%E4%B8%80%E7%AB%A0%20JVM%E5%92%8CJava%E4%BD%93%E7%B3%BB%E6%9E%B6%E6%9E%84_JavaAlenboy-CSDN%E5%8D%9A%E5%AE%A2_files/bfc18bc920d2531793d6f3cc87499ccb.png)

首先，class字节码文件被类加载器子系统加载生成一个大的class对象。

**执行引擎作用就是将字节码指令转换为机器识别的指令。**

# 16.Java代码执行流程

![image-20201118095710832](file:///A:/%E5%B0%9A%E7%A1%85%E8%B0%B7/Jvm/%E5%8D%9A%E5%AE%A2%E7%BD%91%E9%A1%B5/(26%E6%9D%A1%E6%B6%88%E6%81%AF)%20%E7%AC%AC%E4%B8%80%E7%AB%A0%20JVM%E5%92%8CJava%E4%BD%93%E7%B3%BB%E6%9E%B6%E6%9E%84_JavaAlenboy-CSDN%E5%8D%9A%E5%AE%A2_files/20201118095710.png)

# 17.JVM架构模型

Java编译器输入的指令流基本上是一种`基于栈的指令集架构`，另外一种指令集架构则是`基于寄存器的指令集架构`。具体来说：这两种架构之间的区别：

- 基于栈式架构的特点
  - 设计和实现更简单，适用于资源受限的系统
  - 避开了寄存器的分配难题：使用零地址指令方式分配
  - 指令流中的指令大部分是零地址指令，其执行过程依赖于`操作栈`。`指令集更小，编译器容易实现`
  - 不需要硬件支持，可移植性更好，更好`实现跨平台`
- 基于寄存器架构的特点
  - 典型的应用是x86的二进制指令集：比如传统的PC以及Android的Davlik虚拟机。
  - 指令集架构则`完全依赖硬件`，与硬件的耦合度高，`可移植性差`
  - `性能优秀和执行更高效`
  - 花费更少的指令去完成一项操作
  - 在大部分情况下，`基于寄存器架构的指令集往往都以一地址指令、二地址指令和三地址指令为主`，而基于栈式架构的指令集却是以零地址指令为主

## 17.1 两种架构的举例

同样执行2+3这种逻辑操作，其指令分别如下：

- 基于栈的计算流程（以Java虚拟机为例）

```java
iconst_2 //常量2入栈
istore_1
iconst_3 // 常量3入栈
istore_2
iload_1
iload_2
iadd //常量2/3出栈，执行相加
istore_0 // 结果5入栈
```

- 基于寄存器的计算流程

```java
mov eax,2 //将eax寄存器的值设为2
add eax,3 //使eax寄存器的值加3
```

## 17.2 反编译字节码文件

```java
/**
 * @author xiexu
 * @create 2020-11-18 10:14 上午
 */
public class StackStruTest {

    public static void main(String[] args) {
        int i = 2;
        int j = 3;
        int k = i + j;
    }

}
12345678910111213
javap -v StackStruTest.class
1
```

> 反编译得到的指令

```java
public static void main(java.lang.String[]);
    descriptor: ([Ljava/lang/String;)V
    flags: ACC_PUBLIC, ACC_STATIC
    Code:
      stack=2, locals=4, args_size=1
         0: iconst_2  // 将常量 2 压入栈中
         1: istore_1  // 将常量 2 保存至变量 i 中
         2: iconst_3  // 将常量 3 压入栈中
         3: istore_2  // 将常量 3 保存至变量 j 中
         4: iload_1   // 加载变量 i
         5: iload_2   // 加载变量 j
         6: iadd      // 执行累加操作
         7: istore_3  // 加法结果保存在变量 k 中
         8: return
      LineNumberTable:
        line 10: 0
        line 11: 2
        line 12: 4
        line 13: 8
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0       9     0  args   [Ljava/lang/String;
            2       7     1     i   I
            4       5     2     j   I
            8       1     3     k   I
}
```

## 17.3 总结

- 由于跨平台性的设计，Java的指令都是根据栈来设计的。不同平台CPU架构不同，所以不能设计为基于寄存器的。优点是跨平台，指令集小，编译器容易实现，缺点是性能下降，实现同样的功能需要更多的指令
- 时至今日，尽管嵌入式平台已经不是Java程序的主流运行平台了（准确来说应该是HotSpot VM的宿主环境已经不局限于嵌入式平台了），那么为什么不将架构更换为基于寄存器的架构呢？
- 因为基于栈的架构跨平台性好、指令集小，虽然相对于基于寄存器的架构来说，基于栈的架构编译得到的指令更多，执行性能也不如基于寄存器的架构好，但考虑到其跨平台性与移植性，我们还是选用栈的架构

> 栈：跨平台性、指令集小、指令多；执行性能比寄存器差

# 18.jvm生命周期

- 虚拟机的启动
  - Java虚拟机的启动是通过`引导类加载器`（bootstrap class loader）创建一个初始类（initial class）来完成的，这个类是由虚拟机的具体实现指定的。
- 虚拟机的执行
  - 一个运行中的Java虚拟机有着一个清晰的任务：执行Java程序
  - 程序开始执行时他才运行，程序结束时他就停止
  - `执行一个所谓的Java程序的时候，真真正正在执行的是一个叫做Java虚拟机的进程`
- 虚拟机的退出
  - 程序正常执行结束
  - 程序在执行过程中遇到了异常或错误而异常终止
  - 由于操作系统用现错误而导致Java虚拟机进程终止
  - 某线程调用Runtime类或`System类的exit( )`方法，或`Runtime类的halt( )`方法，并且Java安全管理器也允许这次exit( )或halt( )操作。
  - 除此之外，JNI（Java Native Interface）规范描述了用JNI Invocation API来加载或卸载 Java虚拟机时，Java虚拟机的退出情况。

 

# 19.jvm介绍

1. **Sun classIc VM**

   最早的java1.0版本使用的虚拟机 Sun classIc VM

   只提供了内部解释器，如果要使用jit，则要使用外挂，特点就是jit和解释器无法配合工作

   现在hotspot内置此虚拟机

2. **Exact VM**

   JDK1.2推出的虚拟机，Exact MEMORY 准确式内存管理

   具有热点特测和jit和解释器混合工作的功能

3. **Hotspot**

   JDK1.3的时候设置成了默认的虚拟机

   即最牛逼的就是热点代码技术

   1. 通过计数器找到最具编译价值的代码，触发即时编译和栈上替换
   2. 通过编译器与解释器配合工作，在优化程序响应时间和最佳执行性能中取得平衡

   

   

   