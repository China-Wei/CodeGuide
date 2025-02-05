---
title: 面试：技能、简历、问题汇总
lock: no
---

# 《大营销平台系统》，关于面试中的技能、简历、问题汇总

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>课程：[https://t.zsxq.com/17gswKIeX](https://t.zsxq.com/17gswKIeX)

>沉淀、分享、成长，让自己和他人都能有所收获！😄

此部分主要用于向读者提供星球项目之一的《大营销平台系统》项目如何体现到简历中，包括；专业技能、项目经验。

## 一、项目介绍

面试官您好，大营销平台的 Raffle 抽奖模块，是我独立负责实现的一个（学习/工作）项目，此项目模块在架构设计上运用了 DDD 分层架构和模板模式、责任链模式、组合模式、工厂模式等，这样的设计模式对业务流程进行解耦和实现。

Raffle 抽奖模块的完整开发，让我对 SpringBoot 框架技术，分布式技术栈的运用更加熟练，也把设计模式在实际场景的使用了起来，积累了丰富的设计实现经验。这写技术学习的内容，也可以更好的应对以后的开发工作。非常感谢您给我这次面试机会。

## 二、简历模板

- 项目名称：大营销平台 - Raffle 抽奖服务
- 项目架构：微服务架构、DDD 领域驱动模型、前后端分离设计
- 核心技术：SpringBoot、MyBatis、MySQL、Redis、SpringCloud/Dubbo【按需添加，只是对外的接口形式】、React、TypeScript
- 项目描述：Raffle 抽奖模块是整个大营销平台系统中非常重要的一个模块，也是本次项目中我来负责的设计和实现的模块。此模块主要以支撑各类差异化抽奖流程，如；通用抽奖、黑名单、人群、N消耗积分指定抽奖范围、抽奖N次解锁奖品等各类玩法的支持。在此系统模块的设计中运用到了模板模式、责任链模式、组合模式、工厂模式，解决代码的可扩展性，并对抽奖的计算和秒杀做了设计的优化，可以支撑单机 2c4g 服务器 1500 ~ 2000 TPS 的吞吐量，抽奖接口响应时长`45毫秒`左右。「不同服务器，带宽，以及是否还配置有环境相关，会有不同的数据效果」
- 核心职责：
    - 以PRD文档诉求和对功能的评审，设计出抽奖的领域模型功能，以及在抽奖的流程抽象上，分为；抽奖前、抽奖中、抽奖后，的节点上扩展各项行为动作。如抽奖前的人群判断、抽奖中库存扣减、抽奖后兜底奖励等。
    - 依赖于领域模型的定义，设计出抽奖库表。抽象抽奖过程为抽奖策略表、策略明细表、规则配置表、规则树动作表，这样会让抽奖更好扩展。
    - 设计模板模式定义抽奖流程标准，再在模板模式中，调用责任链完成抽奖，对于抽奖中和后的动作使用组合模式的规则树进行动态处理【支持库表配置】。
    - 在项目架构中定义统一标准的 api 由触发器层实现，在触发器层定义监听、任务、http、rpc模块，所有的行为动作，都理解为触发行为。
    - 抽奖也是一种峰值流量高的业务场景，因此在设计奖品库存扣减上，采用了 Redis decr 分段消费和加锁兜底的设计，同时对于消费成功的库存，异步队列方式 + 定时任务更新库存。这样可以不超卖的同时，又减少数据库的压力。
    - 在项目开发中熟练运用了 IntelliJ IDEA、WEbStorm、Docker、MySQL、云服务器、SSH工具，并已将项目完整部署到线上【在校伙伴可以提供线上案例版】。

## 三、面试问题

小傅哥本身也是一个面试官，面试过实习、校招、社招、架构师，不同的面试诉求会有不同的考察范围。通过这些考察范围的问题让求职者通过案例举证，来阐述自己的能力项。而这些能力项的匹配，则是招聘的要求。这里不得不提到，有些小卡拉米的简历，只言片语的项目描述，浮皮潦草的个人职责。是真的没进入面试就没了！

接下来是关于大营销平台项目的面试问题解答，可以参考。

### 1. 你的项目工程是怎么搭建的？

项目的搭建类似于使用 start.spring.io 脚手架创建的，在我们的项目中，使用了统一 maven-archetype-plugin 插件，自定义了一套 DDD 工程骨架脚手架。同类项目都是使用这套脚手架创建项目，因为脚手架定义了统一的版本标准和对应配套的开发环境，所以使用起来更加容易。【如果延伸提问，你还了解哪种搭建脚手架的方式，可以回答 [FreeMarker](http://freemarker.foofun.cn/)】

### 2. 在你的这个项目中，都用到了什么开发工具？项目是怎么部署的

使用到了 IntelliJ IDEA、WebStorm、Sequel Ace/Navicat、ApiPost、Docker、SwitchHosts、Termius（SSH）等，项目上线的时候使用了2个方式，一个是本地构建前后端镜像，PUSH 到 Docker Hub，再通过编写 docker compose 脚本，在云服务器部署。另外一个是搭建 Jenkins 配置部署流水线的方式进行部署。

### 3. 整个项目开发过程中，你熟练的掌握了哪些技术栈

在整个项目开发中熟练的使用了 SpringBoot、MyBatis、Redisson 等技术框架，在编程功能实现，熟练的结合与 Spring 容器，通过 Map 自动装配 Java 语言实现的策略模式。以及在项目中较多的使用了 Redisson 框架，向 Redis 写入 key-value、queue、map、lock 等数据类型，实现业务功能。

### 4. 在项目开发过程中，你有遇到过哪些运行时异常，怎么排查解决的

如刚开始项目开发引入脚手架以外的组件，进行调试的时候，因为Jar版本不同。出现过编译通过，调用的时候方法不存在。通过 Maven Helper 插件，检查到有其他组件多引入了相同Jar包。另外还有一些如开发调试中发现的空指针问题，如查后需要增加空对象判断。此外其他一些更多是功能流程实现细节上，如项目中的规则树节点判断流程问题，抛出一些自定义的异常。这些通过在方法上断点调试逐步的解决。

### 5. 因为你的项目是前后端分离的，接口跨域怎么做的？

首先我们知道，Web跨域（Cross-Origin Resource Sharing，CORS）是一种安全机制，用于限制一个域下的文档或脚本如何与另一个源的资源进行交互。这是一个由浏览器强制执行的安全特性，旨在防止恶意网站读取或修改另一个网站的数据，这种攻击通常被称为“跨站点脚本”（Cross-Site Scripting，XSS）。

所以在我的前后端分离项目中，通过配置 @CrossOrigin 注解来解决跨越问题。开发阶段 `Access-Control-Allow-Origin: *`、上线阶段 `Access-Control-Allow-Origin: https://gaga.plus`

### 6. 看到你的项目用到了 DDD，这也是我们很感兴趣的技术点，你可以介绍下你在使用 DDD 做这个项目时，都运用了 DDD 哪些知识。

DDD 是一种软件设计方法，软件设计方法涵盖了范式、模型、框架、方法论等内容，而 DDD 的很多规范约定，都是为了提高工程交付质量。如几个很重要的知识点；框架分层结构、领域、实体、聚合、值对象、依赖倒置等。它所有的手段，都希望以一个功能逻辑的实现为聚合，将功能所需的对象、接口、逻辑，按照领域划分到自己的领域内。

就像在这个项目中，我负责实现的抽奖中的策略，就是一个独立的领域模型。在这个领域中我需要提供策略的装载、随机数算法计算、抽奖模板调用（含责任链和规则树）功能，这样一个领域就像划分好的一个独立个体，它拥有属于它的对象信息（实体、值对象、聚合），当需要使用数据库资源、缓存资源，以及外部接口资源的时候，都通过依赖倒置进行调用。也就是说，我的领域不做其他模块的引入，而是领域只负责业务功能实现，所需的所有数据，则有外部接口通过依赖倒置提供。[更多理论知识](https://t.zsxq.com/17tqSU5CE)

### 7. 你的抽奖流程中，哪些被定义为值对象，哪些被定义为实体对象

在 DDD 的规范定义中，值对象通常用于描述对象属性的值，不具备唯一ID，不影响数据变化。如；数据库中字段的枚举值、业务流程中属性对象。如抽奖流程中，RuleLimitTypeVO 规则限定方式的枚举值对象、还有 RuleTreeVO 规则树值对象。而那些实体对象，则具备唯一ID，会影响到最后的写库动作。如；抽奖发起实体、奖品信息实体对象。并且我们可以把一些和实体对象相关的功能聚合到对象内，这样的通用性会更好，避免所有调用方都需要自己编写逻辑。

### 8. 关于访问数据层的依赖倒置，是怎么使用的，有什么好处，你可以描述下吗

DDD 中的依赖倒置是一个非常好的设计，尤其是与 MVC 结构对比的时候，MVC 的贫血模型结构设计，数据库持久化对象，很容易被当做业务对象使用，这样后期非常难维护。但在 DDD 的分层结构用，是以 domain 领域实现为核心，一个 domain 领域下所需的外部服务，都由领域层定义接口，让基础层做具体实现。而数据库持久化操作，定义的 PO 对象，就被这样的方式被限定在基础层了，外部是没法引入使用的，也就天然的防止了数据库持久化对象进入业务中。

### 9. 我看你简历有提到，把抽奖划分为抽奖前、中、后，三个动作。请具体结合场景讲解下，为什么这样设计

这个的设计得益于在 Spring/MyBatis 框架源码的学习，在源码中经常会出现对一个流程进行拆分解耦，流程可扩展的点，如 Spring 是 Bean 对象的拆解，MyBatis 是会话流程的拆解。所以在设计大营销的抽奖模块时，对于需求中的各类功能点；黑名单抽奖、权重抽奖、默认抽奖、抽奖N次解锁、兜底抽奖等等情况，是可以拆解为抽奖前、中、后，3个行为动作的，基于这样的考虑后，就可以设计出非常容易扩展的松耦合结构。

### 10. 是什么场景下使用了责任链模式，什么场景使用了组合模式，为什么？

在设计完抽奖前、中、后，搜耦合的结构模型后，对于抽奖前要执行哪种抽奖，但单向选择问题。所以这里使用了责任链模式，进行节点流程判断，从黑名单、权重，最后到默认，走一个单独的具体抽奖，所以使用责任链更为合适。

之后是进入抽奖的中和后，这两部的流程是相对复杂的，需要判断用户抽奖了几次，对于不同次会限定是否能获得某个奖品，同时还有库存的扣减，如果库存不足或者不满足n次抽奖得到某个奖品，则会进行兜底。那么这就是一个树规则的交叉流程，所以会使用了组合模式构建一颗规则树，并通过数据库表的动态配置决定在抽奖前完成后，后续的流程要如何进行。

### 11. 抽奖也是一种瞬时峰值很高的业务场景，那么对于抽中奖品后的库存扣减是怎么做的？

关于库存的扣减，是一个非常重要的流程。尤其是这种单独资源竞争的场景，如果设计的不好，很容易把服务打挂。

所以在这套系统设计中，为了避免库存扣减直接更新库表的行级锁，而导致大量的用户进行等待状态。所以把数据库表的库存同步到 Redis 缓存中，在通过 incr 扣减的方式进行消费，同时为了确保在临界状态、库存恢复、异常处理等情况下不超卖，而对每一条产生从 incr 值，与抽奖的策略ID组合一个key，进行 setnx 加锁兜底，来保证不超卖。—— 这样的设计是颗粒度更小的锁方案设计，性能接近于无锁化。

### 12. 你讲到库存的扣减是通过 Redis 滑块锁实现的👍🏻，那么最终同步库是怎么做的，怎么降低对数据库的压力的？

关于 redis 缓存和数据库表库存数据的流程，设计了异步更新，保持最终一致性的设计。在执行完库存的扣减操作后（在抽奖中规则树库存节点流程），发送一个扣减完成到 Redis 的异步队列（可以使用MQ+延迟消费），之后通过定时 Schedule Job 来消费队列。这样就可以控制效率速率，降低对数据库的压力。（因为我们不能 Redis 扣减的多快，就直接打到库表上，那样对数据库的压力依然很大，容易打挂）

### 13. 你提到了接口的单一职责设计，这部分具体讲解下。

单一职责原则的核心思想是，一个类应该只有一个引起它变化的原因。也就是说一个类应该只负责一项任务或功能，如果一个类承担了过多的职责，那么这个类就会变得复杂，难以维护和扩展。

这样的原则在一些需要长期使用、迭代、维护的功能设计上，是非常重要的。我们要尽可能的让大营销的抽奖领域领域模块具备独立性，所以要使用单一职责原则。在这个原则约束下，设计了3个接口类；抽奖策略接口、奖品信息接口、库存处理接口（异步扣减等），这样3个接口的设计，在将来需要扩展的时候，会非常容易。（可能会问具体编码，问的比较多样性，这部分需要自己阅读代码来学习）

### 14. 在项目中你提到了可以支持不同场景的抽奖诉求，比如；多少积分后可以抽奖一个固定范围的奖品，或者抽奖n次后，才可以中奖某个奖品。这部分你是怎么做的？库表怎么设计的？

这块的流程，就是前面关于大营销抽奖领域模型的设计，从而确定的库表设计。也就是常说的领域->驱动设计。

库表包括；策略表、策略明细（库存、概率、规则key）、奖品表、规则表、规则树（3个表）—— 这部分在学习项目后，需要具备能在纸上画出库表ER图。

### 15. 你的抽奖接口响应时间是多少？

这样的问题主要考察你是否做了项目的上线，以及了解过接口的响应时间。如果做过就非常好回答，没做过乱说是挺容易被继续提问的。

参考数据；2c2g 云服务器，部署项目（含mysql、redis），占用63%内存，抽奖接口响应时间为38~55毫秒（项目有完整的手把手部署教程，还有监控部署教程，可以自己部署验证）。

### 16.（开放问题）你在做项目中，什么问题难住你的时间最长，为什么？

这是一个开放问题，重点考察你对项目的开发中个人的积累。你可以针对自己的学习过程中，有哪个流程的实现，让你最为有感触，即可回答。

如；可以对大营销抽奖模型流程的设计和库表设计，最为耗时，因为你不断的在思考如何拆解出一个好扩展的松耦合结构，同时拆解后，还要保证搜耦合下的高内聚。所以这部分是比较耗时的。同时也可以说在设定某个方法的，名称、入参、出参时，做了大量的思考。因为名字的定义非常影响以后的理解。好的代码就是文档，所以对于这样的东西花费不少时间。