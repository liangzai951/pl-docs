﻿# 类型 vs. 类型检查

## 引言

　　这篇文章是一些经常复用的常识科普的总结。

　　经问题太多，不得不绕过其它地方直接在这里填坑。

　　虽然对于内行可能很多废话，但是仍然建议自上而下阅读（发现有梗请按字面意思理解）。

## 什么是类型

　　高屋建瓴：类型是一种抽象的实体(entity) 。嗯，等于没说。

　　当然其实是说了些什么的。熟悉 C++ 基本概念（字面意思，语源是 [ISO/IEC 14882 Clause 3](http://www.eel.is/c++draft/#basic) 的标题）知道，至少类型不是**名称**，是被指称而不是指称别的什么玩意儿的——在几乎所有语言和习惯用法中都一致。

　　不过现实中的问题<s>破事</s>当然不那么简单。

## 类型 = 分类？

　　当然不是。

　　在说为什么不是之前，首先需要正视这是一个有些年头了的笑话，并且可能具有名人效应而带坏一些不明真相的小碰友，典型地如[这篇](https://commandcenter.blogspot.com/2012/06/less-is-exponentially-more.html)。在一口一个类型系统(type system) 如何如何时，不觉犯了基本的没搞清概念的内涵的低级错误，以至于把名义类型系统([nominal type system](https://en.wikipedia.org/wiki/Nominal_type_system)) 和类型系统混为一谈。鉴于[LtU 上的评论已经足够一针见血](http://lambda-the-ultimate.org/node/4554)，不在此多科普细节。

　　讽刺的是，造成这种误会的原因，恐怕就是原文批判的：类型系统烂设计过于有存在感——而影响了作者本应具有的视野。这样，应予以重视的教训除了“不要在不懂的领域跑火车”外，更要紧的是得先搞清楚要批判的东西到底是什么玩意儿，而不是一上来就想造个大煋闻，批判一番了事——不仅削弱本来可能性以微粒子程度存在的观点的合理性还误导群众，而且容易贻笑大方。

## 那么一个类型“到底是什么玩意儿”？

　　还是先不用急。这一节的重点是理解[“到底什么玩意儿”](https://zh.wikipedia.org/wiki/%E6%9C%AC%E4%BD%93%E8%AE%BA_%28%E5%93%B2%E5%AD%A6%29)这个说法。

　　其实这是一个哲<s>♂</s>学问题，确切地说是一个形而上学问题（不管对这个领域清楚不清楚，请忘记黑格尔的私货，总之这里的意思和辩证法没一腿）。

　　这类统称[本体论](https://zh.wikipedia.org/wiki/%E6%9C%AC%E4%BD%93%E8%AE%BA_%28%E5%93%B2%E5%AD%A6%29)问题的重点就是“是什么”。接下来，有意思的是，要指望谁来回答这个问题？对于一般形式来讲，的确可能只能哲学到底了，但对于**某个类型系统中的类型**——这种**人为设计**中的一份子，其实答案是很明显的：类型系统的设计者或者类型的设计者（类型系统的用户）说“我就是想要让它**叫**那个啥”，如是而已。

　　比较无奈的是，很多钦定类型“**是**什么”者自己就对这层含义并不怎么清楚，似乎自以为是天赋人权了。这个之后再提。先看一下祖宗长什么样再说吧。

## 历史上的“类型”是什么玩意儿

　　这段历史常识可能很多童鞋不知道，虽然真要追根溯源可能倒未必出很多人意料。

　　讨论当代程序设计语言使用的“类型”的直系高祖——其实本质上就是个哲学（数学）范畴的问题，因为“类型”是为了解决[第三次数学危机（罗素悖论）](https://zh.wikipedia.org/zh-cn/%E7%BD%97%E7%B4%A0%E6%82%96%E8%AE%BA)搞出来的副产品——[类型论](https://zh.wikipedia.org/wiki/%E7%B1%BB%E5%9E%8B%E8%AE%BA)的研究对象。

　　按照罗素本人的一些努力构造的解法之一是创造一个[公理系统](https://zh.wikipedia.org/wiki/%E7%BD%97%E7%B4%A0%E5%85%AC%E7%90%86%E4%BD%93%E7%B3%BB)——请注意其中的“[类(class)](https://zh.wikipedia.org/wiki/%E7%B1%BB_%28%E6%95%B0%E5%AD%A6%29)”和“面向对象”等并没有毛线关系（要是习惯望文生义可能就像上面提的搞不清什么是类型的那位一样中招了）。虽然作为事后诸葛亮，主流数学到现在也并不吃这套（而改用 [ZF(C)](https://zh.wikipedia.org/wiki/%E7%AD%96%E6%A2%85%E6%B4%9B-%E5%BC%97%E5%85%B0%E5%85%8B%E5%B0%94%E9%9B%86%E5%90%88%E8%AE%BA) ），但还是不妨提一些存在间接的深刻影响，特别是“类”的概念——比如 [NBG](https://zh.wikipedia.org/wiki/%E5%86%AF%E8%AF%BA%E4%BC%8A%E6%9B%BC-%E5%8D%9A%E5%86%85%E6%96%AF-%E5%93%A5%E5%BE%B7%E5%B0%94%E9%9B%86%E5%90%88%E8%AE%BA)（嗯不是某一心一教……）以及[“一般化的抽象废话”](https://zh.wikipedia.org/zh-cn/%E8%8C%83%E7%95%B4%E8%AE%BA)涉及的一些[重要基础](https://zh.wikipedia.org/wiki/%E9%9B%86%E5%90%88%E8%8C%83%E7%95%B4)（虽然这块东西即便是 Haskell 厨也并不方便抡圆了用）。

## 意义何在？

　　那么这些历史与上面有什么关系呢？嘛，至少对名义上的本体论意义，其实就是——**毫无关系**。

　　且不提当年的副产品[发展到现在](https://zh.wikipedia.org/wiki/%E5%90%8C%E4%BC%A6%E7%B1%BB%E5%9E%8B%E8%AE%BA)还在兴风作浪要顶掉集合论篡数学基础的大位，就是仅在程序语言理论中，它仍然是王道正统的几乎不二的形式基础。但是，纵观古今，我愣是没发现有一个类型论在一般意义上来指导用户**应该或必须把（具有类型论以外性质的）什么东西抽象成什么类型**。也就是说，**本体论意义的“类型”，根本就没有指导类型系统设计一般的数理逻辑理论支持，更不用提强调本体论意义的必要性了**。具体地，各种类型论中，并没有要求“类型”如同所谓面向对象的类一样，成为和某种领域外实体的对应，以作为**建模**或“分类”的基础，而仅仅是项(term) 上关联的一些抽象实体罢了。（像 C++ 的 tag dispatching 之类的所谓奇技淫巧，反倒更符合“类型”在这里的原意—— term 上的 tag ——虽然语言规则使之具有的性质并不怎么方便用。）

　　某些人使用语言时没人限制该干啥，仗着指哪打哪、**叫**啥**是**啥可以作为天赋人权来用（看起来像是鸭子类型么……），强制让一个类型和一个不符合（类型系统蕴含的）一般性质的本体对应还想甩锅给类型系统的设计？这甩锅路线也太烂了……

　　从这里更加可以看出之前的例子为什么是笑话。强要加给“类型”以含义的，明明是**没怎么搞清需求**以及很可能**对类型系统如何在编码时起作用一窍不通**的用户，而并不来源于类型系统自身的设计。反过来，符合这些上梁不正的需求的类型系统“设计”，倒极可能带来更高渣设计的语用风险——比如说，解决一类明明在设计目标领域内的（其它语言容易做到的）问题怎么用都麻烦，让用户怀疑人生之类……

## 类型正确(Type Correctness)

　　因为上梁不正的观念偏差，钦点“正确”的风气大势所趋严重；可惜排除少数几个坑明显特别大、涉及用户基数也大的话题（如 [`const` correctness](https://isocpp.org/wiki/faq/const-correctness) ），一个个都不怎么喜欢定义清楚什么叫“正确”……

　　当然，把“正确”当成“符合期望（上层规格说明隐含的规则）”其实在实用时本身问题不是很大。比较显著的问题来源于本体论认知混乱：要先知道“是”什么类型，才敢放心用。

　　这种通病集中体现在[类型推断](https://zh.wikipedia.org/wiki/%E7%B1%BB%E5%9E%8B%E6%8E%A8%E8%AE%BA)（这里 inference 译为“推断”指要求必须存在能用于确定项上类型指派的解否则失败，通译“推论”没有这层含义，而“推导”(deduction) 形式上更一般但更弱，一般不要求限制特定输入的形式）上。典型例子是 C# 提供了 `var` 关键字，“社区”意见迅速分为两派（中间派似乎惯于闷声大发财）：尽量用和尽量不用。虽然前者主要势力之一的 Reflector 党忍受性能拙计（也许他们都有 SSD ）我不是很能理解，切入点也非常奇怪，但整体还是算有那么些道理；而后者主要理由是不显式写出类型可读性差之类。

　　在此我需要指出，基于足够的理由，我旗帜鲜明地站在前者一边——**谁告诉你看不出显式的类型可读性就差**了？实际上，即便不管实际会发生多少重构需求，**多数**情况下**就不应该写出（即便是不重复的）显式类型**，因为这些情况问题的有效的解就**不依赖类型具体是什么**。背后的根本原因是，本来正常解决问题的套路就是**先理顺逻辑和实体之间的关系然后再考虑能在选定的语言中使用什么类型**，而**不是先看看自己知道些某种语言能支持什么本体论意义上的名义类型然后去凑解决方案**（如果只是因为选定的语言抽象起来实在太不方便，那是选型失败，是工程缺陷，没权没条件改掉就横竖都得忍）。后者虽然在推敲具体实现时作为**妥协**无可厚非，但显然是方法论意义上的颠倒因果，而且很容易造成 [leaky abstraction](https://en.wikipedia.org/wiki/Leaky_abstraction) 这类擦屁股后患无穷的问题。而这里依赖类型推断就是表达必要关系（而不是本体）的有效手段（如果只是编译器报错烂就别赖方法论问题了）。

　　注意上面这种情况把类型写得太清楚具体，反而是不那么“类型正确”的——不“合适”地符合解决问题的“期望”。

　　简而言之，**更清楚地限制使用的类型具体“是什么”，依赖不必要的从实现泄漏的假设，导致很可能更不正确**。

## 类型识别(Type Identification)

　　提到“是什么”的问题，最显然的实现是比较表示类型的数据结构（类型标识）是否相等。这也被一些语言直接提供为语言特性。

　　这种实现具体的操作也暴露了基于本体论意义上的判断的局限，而且被更多用于普遍地了解。比如说，一般尽量不要用 `typeid` 比较相等——倒未必是因为运行时 `typeid` 性能低（至少存在比 `dynamic_cast` 普遍快的实现），而主要是因为硬编码 `==` 扩展性烂得太感人了，和 `dynamic_cast` 啊虚函数啊比起来没啥优势。

　　当然不可否认运行时类型识别不少情况下可能仍然有必要（对 `typeid` 而言，实现 `any` 算是个主要的例子），但是提可扩展性和灵活性其实是不太必要关心运行时不运行时，道理都是类似的。为什么这里的理解就出了偏差呢？谁的责任？

## 类型安全(Type Safety)

　　比起比较类型标识而言，类型安全是在一般语言中更普遍存在的口水话题。所谓安全，和“正确”类似，仍然是“符合期望”，只不过更多地强调考虑风险而不是考虑具体对策评判尺度的唯一性，也相对不那么容易被语言规则强制。

　　按理说，既然选择措施的余地更大，就应该更容易有共识各取所需才对。可惜业界的坏毛病是信息不对等面不改色继续窝里斗——我所谓的安全和你所谓的安全，也许就是鸡同鸭讲，但这个没关系，不听我话的就是不安全的！（黑人问号……）

　　有些关于类型安全的命题可能足够众所周知之而被作为 soundness 的公认判断准则，比如[这个](http://typeof.net/2014/m/formation-of-modern-magic--why-functions-are-contravariant-in-the-input-type.html)。遗憾的是可用的结论虽然普适但过于基础而太少，而且仍然依赖特定对象语言的类型系统设计（有些语言根本就不支持表达这样的类型所以就是一句空话……）。

　　因为依赖的假设和类型系统设计不尽相同，超过类似上面的周知陈述地去讨论什么才能算类型安全而取得共识这点在一定意义上是徒劳的。但值得注意的是，相当多数用户的推理过程有相当大的漏洞：他们往往不清楚（各种不同的）“安全”是如何保证的。

## 类型检查(Typechecking)

　　现实的类型安全一般由两类手段：语言的构造性规则限制不安全类型构造的表达，以及语言对潜在不安全的表达进行额外的语义检查。前者涉及对不特定的项（如表达式）进行类型指派，也就是一般所谓的 typing ；后者相对比较事后诸葛亮但在设计语言时配置起来比较灵活（可以很容易地弱到没有而不那么容易影响其它语义），所谓 typechecking ；然而很多人根本没搞清楚**这两者根本不是一回事**。

　　（终于点题了……）

　　一般来说，这两者的确具有不少共性才容易被混淆。比如说，都可以作为实现某种类型安全规范的要素；再如，简单情形下都可以构造为判定性问题；再如，在语言实现的哪个阶段(phase) ——翻译时（“静态”）还是运行时（“动态”）检查（注意**区分出“运行时”和非“运行时”并非对所有语言都有意义**）；不一而足。只是混淆这两者问题可能还不大，但基于混乱的认知对语言设计分类而只能让围观群众继续不明觉厉，就不那么好笑了。

## 静态/动态（类型）？

　　首当其中的是一些关于静态/动态语言和静态类型/动态类型语言的混乱。在了解 typing 之后这就不攻自破了：静态类型或者动态类型都和 typing 的时机有关；而单纯静态/动态，对彻底不提供类型系统设计的 typeless 的语言都可能说得通。

　　重复，需注意，对一些不规定区分静态/动态阶段的语言，这些分类都毫无意义——除非就干脆认为静态只是特殊的动态得了。

## 强类型？

　　更严重的问题在于“强类型”(strong type) 这个说法。考虑到这个概念词源上基于 typing ，引用起来却杂糅了 typing 和 typechecking ，不同作者对什么是足够强的理解还不一样，混乱可见一斑。

　　这里的一般建议是避免混乱的用法。如果不能避免，仅在确定类型时使用，而讨论类型检查时直接以具体的机制（对 ××× 类型的检查）来避免混乱。特别地，应注意避免“弱类型”这样望文生义还模糊了原本可能已分清界限而使之失去实用价值的生造词。（后者的使用者通常还具有其它的认知混乱，比如无法区分强制(coercion) 和铸型(casting) ，不清楚强制可以作为一种多态([ad-hoc polymorphism](https://en.wikipedia.org/wiki/Ad-hoc_polymorphism)) 而不一定有损类型安全性等等。）对特定实体声明保持类型的性质，使用 manifest typing/latent typing 论述——这样“强类型”这个说法才有一些无歧义的生存空间，不至于像“弱类型”一样鸡肋且造成误会。

## 结语

　　……科普教育果然还是甩链接省时省劲。
