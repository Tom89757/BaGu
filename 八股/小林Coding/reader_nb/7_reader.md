## 大三就啃框架源码！轻松因对字节面试

大家好，我是小林。

上周我发了个[读者字节三面的面经](https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247496990&idx=2&sn=160eaa432d4bfe7115fa7baee19db3ed&scene=21#wechat_redirect)，结果评论区很多人不相信这是校招的面经，觉得难度有点高。

![图片](https://img-blog.csdnimg.cn/img_convert/8fe33baf189b2fb06919e79583abf93d.png)

首先这个确实是读者真实的校招面经，再来因为他之前实习过，他的实习项目里涉及到了不少中间件，所以面试官对于高并发问题考察比较多，也算是按简历来问的了。

正好他自己在学习的时候，**有看源码的习惯**，所以面试的问题，他都能应对，甚至能说到面试官眼前一亮，然后在几天拿到了字节 Java 后端的意向。

我也邀请了这位读者分享他的学习路线和心得，**他最后的心得讨论八股文的事情，说的很好，值得一读！**

------

## 我的情况

我先说说我的基本情况。

双非一本，科班，大学 0 基础，随着学校课程，选择后端开发，大三寒假在某独角兽企业 Java 实习到提前批，字节已 oc。

我这次的分享更多的适合准备校招或者是大学已经决定选择后端方向的同学，社招大佬见笑~

首先这里要说明一下哈，下面的路线可能对于很多人是「填鸭式教学」，就是基本会是面向面试准备的，关于面试工作实际开发以及程序员自我修养的这部分会放在最后心得部分，感兴趣的可以选择性观看。

我的观点始终是由点到线，由线再到面。

很多东西肯定是经典的书籍会更加权威和全面，但是说实话，不是每个人都能抱着本书看的进去，并且理解透彻，比如我一开始看书的时候就是很迷。

所以我的建议一直都是，**从弱智的，易懂的，有实际案例的博客或者是视频看起，了解大概，动动手撞撞坑之后，再去系统性的看书**，这样会比较好理解。

起码我是这样经历过来的，因为实在没有其他办法。

## 学习路线

首先推荐几个后端学习的仓库吧：

Github 上很出名的：

- javaguide
- cs-note
- JavaFamily

当然我也很期待小林大佬能早日推出自己的仓库啦~

首先要搞清楚，作为后端开发，我们需要掌握一下什么知识点，其实无外乎就是如下内容。

### 编程语言

以 Java 为例子。

#### Java 语法基础

这个没啥好说的，科班的话有教材，非科班的话建议看一下入门教程，菜鸟教程之类的（别嫌弱智、简单）。

看完之后可以全面的看一下进阶书籍（这是面向科班&非科班），例如著名的：Java 核心卷等（说实话，一开始让我看，真心看不下去，可能是我菜……）。

#### 集合框架源码

必须是源码，现在这种烂八股应该不会有人不会源码吧？而且源码里面很多设计思想可以学到很多，例如 hash 的泊松分布推导等。

上面那部分基础看完应该都知道这是什么了吧……有能力有自信的可以根据面经题目自己去分析源码，小白同学建议网上找一些源码分析（这里一定要注意，我是很建议经常百度的，但是不要无脑百度，一个源码可以看多一些博客对比一下，然后自己实际去看一下分析一下是不是如此，切忌人云亦云），有一些能力之后自己去总结。

#### 并发编程

并发编程是现在后端语言很重要的一块基础（当然工作中可能比较少机会可以用到），但是并发编程扎不扎实，运用的熟不熟练可以很好的体现一个程序员的编程素养和基本功。

这里肯定有大佬会吐槽说面试造航母，进门拧螺丝哈，hhh 确实并发编程其实一般场景运用不多，但是在项目里，很多可以优化的细节，别人做不到你能做到的，往往就是在这些点，包括下文 JVM。

- 基础：上述的教程，自己打一下练练手。
- 进阶：书籍《并发编程的艺术》、《并发编程实战》。

#### JVM 虚拟机

这里可能很多人有些疑问了哈，实际开发中你写项目需要了解虚拟机吗？真正调优轮得到你吗？

emmm，这块的话只能说见仁见智了，个人认为开发里的虚拟机小调试以及一些常见溢出的分析还是很有必要的。

退一万步说，学 Java 的，总不能连虚拟机都不知道吧。我个人认为啊，任何东西都是知其然、知其所以然、知其所以必然，了解清楚了，知道原理，你写代码的时候会有一种看透的感觉以及会有前所未有的安全感。

- 基础：虚拟机有很多原理分析的整套文章，我这里就不推荐了，都可以搜的到。
- 全面进阶：推荐周志明大佬的《深入 Java 虚拟机》，现在应该有第三版了。

#### Java 相关框架使用以及源码了解

从常见的 ssm 到 spring 全家桶，这一块真心不好学，资料很杂，入门的话我建议去看一下黑马程序员，尚硅谷相关教程，或者是 how2j 这个网站，上面也有详细的路线和简要入门教程（各位大佬别吐槽哈，不是宣传培训班，但是确实作为小白入门很香）。

上面是简单入门，无脑运用，实际进阶的话还是看看源码看看书哈，一定要找些项目来做做。

- 推荐书籍：《spring 源码分析》。
- 面试重点：这块多去看面经和源码吧，实际开发里需要关注的点还是有的，例如异步注解的循环依赖报错，我在实习的时候就遇到了，不懂原理真心不好解决。

### 数据库

以 Mysql 为例子。

科班基础有教材，非科班基础推荐小林大佬的《图解 mysql》。

进阶的话，极客时间的《mysql45 讲》，书籍主要两本，分别是《高性能 mysql》和《mysql 技术内幕》，书籍建议有一定基础再看。

面试重点：小林&帅地的文章里都有很多，不再赘述。

### 中间件

#### Redis

这个入门也是看一下教程会快一些，科班应该也没有专门的课程吧？

入门可以考虑尚硅谷之类的视频，进阶的话可以看看书和一些源码分析：《redis 的设计与实现》，老经典了吧。

不过 redis 个人认为难点在于运用，这点就不多说了，学完基础大家应该都会知道后续的学习路线了，可以期待一下小林大佬的《图解 redis》

#### mq、kafka

这个有余力可以学一下，面向面试的话两者都行，实际运用看业务场景，这里不再赘述。

入门还是推荐看视频，b 站很多，随便搜，没有什么特别推荐。

进阶的话，推荐书籍《rocketmq 的技术内幕》，不过说实话，我自己也在看 mq 源码，感觉这本书写的一般，不够细节，目前没发现什么特别全面的书籍。

### 计算机基础

#### 算法与数据结构

这一块的重要性不再多说啦，当然也有很多人吐槽这个没用的，确实我也很烦应试刷题，可以没办法，确实是面试硬性要求，尤其是外企入门推荐左程云大神视频&帅地玩编程的相关文章。

#### 设计模式

科班有教材，非科班建议《大话设计模式》这类书籍入门

这一块偏抽象与实践，主要还是业务场景，需要自己多找找实际案例看看多理解。

#### 计算机网络

科班有教材，非科班直接无脑小林大佬的《图解网络》。

看完之后进阶可以考虑详细的看一下《计算机自顶向下》，源码分析等，例如：开发者内功修炼公众号。

面试重点，后面心得会提到。

#### 操作系统

科班有教材，非科班直接入手小林《图解系统》。

进阶可以考虑看一下《操作系统导论》，国外的课程 CSAPP，MIT 相关课程等等（动手会比较多）。

面试重点，后面心得会提到

#### 汇编、计组

这一块科班应该很熟悉，噩梦，非科班的话建议找一些视频入手，b 站很多大学的计算机相关课程，播放量高的都挺不错。

#### 分布式 rpc

这里不再赘述了，校招生估计大都是了解基本概念，相信学完上述内容，自己应该清楚该怎么学了~

#### 云原生云计算

docker、k8s 这些这里不赘述了哈，相信需要学这个的大佬自己知道如何学了~

## 一些心得

说实在的，刚刚那个路线其实稍微学过点后端的估计都知道，而且现在开源仓库太多啦，我想可能对大家帮助更大的还是自己的学习感悟吧。

其实说到这里相信大家肯定很清楚了，太多资料，太多八股了……

这里聊一下我对八股的一些看法吧（因为我看到上次小林大佬发的面经下面评论有同学提到八股的问题）。

首先得搞清楚八股是什么，**一个知识点，你能把使用以及原理说出来，我称之为八股，但是你能把底层关联以及业务使用，优化历程也能搞清楚，我称之为能力**。

固然，现在的 CS 基本已经形成了套路，一套一套的面试题，很多人无脑跟着背就行，甚至现在还有分公司，分部门，对应的面经和知识点都有人总结，可见八股影响之深。

但是退一步说，**八股真的没用吗？八股不能体现你的能力吗？八股对于你的工作真的没有提升吗？**

以我自己为例吧，这里不以偏概全哈，单纯就是分享一下自己的经历和看法。

***例子一\***

刚刚上文学习路线有说到虚拟机的学习，很多人吐槽是不是这玩意没必要学？

但其实呢，我在实习的时候就遇到了自己的一个模块线上 oom 了，排查了很久通过动态数据定位到是新生代与老年代比例的一个问题。

当然了，对于很多大佬来说，这不算什么。但是对于我来说，假设我连这一块的基本知识都没掌握的话，我即便百度到了解决办法（例如无脑把比例调大，把内存调大），还是没法从根本上解决问题，所以我还是挺庆幸的，不然那天就背锅了……

***例子二\***

再者说吧，还是八股的问题，面试的时候这可以作为你的一个优势，别人回答 CMS 就是简单的说下基本过程（我称之为八股），但是你回答可以把三色标记出现的问题以及 CMS 短暂的 STW 的问题引出 G1，并且还能举出例子，你在实习或者业务中使用的是什么收集器，为什么，怎么切换的（我称之为能力）。

***例子三\***

再举个例子吧，一个很八股的问题，三次握手，老八股了。如果是简单的说出过程甚至需要说出中间的标志位，我都认为这是基础（八股），但是如果你能说出为什么前两次握手不能带数据，怎么避免攻击的，实际企业应用是怎么做的（开发者内功修炼里有相关文章），我称之为能力，我到现在还记得面试的时候把相关过程分析以及这一块内核的源码说出来的时候面试官惊讶的表情，这就不是八股了，这是你的优势。

同样的，工作中也是一样，我实习的部门是做底层开发的，网络嗅探，内核参数监控是常事，所以我会认为，作为一名程序员，不管说是不是真正用到了，但是实际上经常接触的东西，这些东西，还是值得多去了解的。

例如之前面经提到的 QUIC，实际上很多厂内部已经有类似协议开发的应用了，所以个人认为还算是一个很常见的东西。

***例子四\***

多给一个例子吧，也是面试的小技巧，可以多说一点内容体现你的基本素养。

例如 Java 很熟悉的 volatile 关键字，假设说我是面试官，我的面试者只说到原子性有序性，JMM 内存模型这些，我会认为这是八股。

但是如果能说到汇编文件的 lock 前缀，内存屏障，MESI 设计，MESI 与 volatile 的关系，MESI 优化队列，总线锁与缓存锁，总线风暴，那么我认为这是能力。

至于这对工作有没有用，我个人认为，见仁见智吧（总线风暴就是一个点）。

***例子四\***

上次面经文章分享的是我的实习项目，具体就不方便透露了，但是还是说一个点吧。

实习项目里使用了 mq，我在开发的时候会注意去看其他企业的相关实施方案，会去整理源码，然后开发过程中会进行压测，无意间我发现，我的 mq 使用的比隔壁一位高级开发还要溜，当然我就是随眼一瞟觉得他写的不怎么样。

那么我在面试的过程中，面试官同样的一个 mq 怎么保证消费可靠这种问题，我与别人回答的差距就出来了。

这里面我就不强调 os 和网络，数据库这些基础知识的重要性啦，我个人不是很建议出了什么新技术就莽着去学习，因为万物离不开底层，吃透底层，再搞清楚业务，那么现在的很多中间件啊，分布式相关的知识啊，个人认为只是新瓶装旧酒。

举上述例子我不是想秀自己的知识储备，这些在各位大佬面前真的是不值一提，羞愧万分，只是想通过个人在校招准备过程中说明一点。

就是**八股 ≠无用，面试通过 ≠ 背八股**。

很多时候你以为你问题都回答上来了，面试却挂了，面试官是在刷你 KPI（当然确实也有可能是）。

但是我更多的认为要多反思自己，是不是说到位了，是单纯的在背，还是说自己的理解，结合业务场景来说，并且说出优化的点，说出这种方法存在的问题，我个人觉得这是会让面试官眼前一亮的点。

同时，也是我在“八股”过程中的一点感悟吧，其实校招只是人生的一个阶段，欲速则不达，要珍惜现在能静下心来沉淀知识的时间。

程序员的内功修养与素养真的很重要，所以在“八股”之余会多去看看一些知识的源码以及企业里面的应用，会去看看《代码整洁之道》、《程序员的基本素养》等，总结成自己的笔记，未来希望能开源。

关于有人问到如何学的问题？

其实很简单，还是那句话，知识点都是那么多，深度和延伸得靠你自己了，一个大方向就是，从语言的实现到操作系统（网络）的实现，按照这个方向去搜集资料，去看源码，相信会很有收获的。

肯定有人提到，学这么多，进去还不是拧螺丝？

这个经典问题，只能说见仁见智了，我始终认为，有拧螺丝的时候，当然也有造航母的机会，这得看你的选择与把握机会的能力。

当然这里也要大厂小厂的争论，这里就不说了。不管在哪里，肯定会有拧螺丝的时候，但这不妨碍你有一颗自我学习，自己提升的心，与君共勉，这可能是我年轻气盛的想法。

最后再次说明一下，我是小林大佬的忠诚读者，他的图解系列给了我很多灵感和帮助，应他邀请写分享，第一次写这些类型的内容，如果有任何语言斟酌的不到位的话，望各位海涵！

最后如果大家能够从中有一点点的收获或者是认同，借小林大佬的光，万分荣幸，希望大家也能找到自己满意的工作。