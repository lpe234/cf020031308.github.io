# 【摘译】建立像人一样学习与思考的机器

原文：[Building machines that learn and think like people](https://www.cambridge.org/core/journals/behavioral-and-brain-sciences/article/building-machines-that-learn-and-think-like-people/A9535B1D745A0377E16C590E14B94993/core-reader)


```BibTeX
@article{lake2017building,
  title={Building machines that learn and think like people},
  author={Lake, Brenden M and Ullman, Tomer D and Tenenbaum, Joshua B and Gershman, Samuel J},
  journal={Behavioral and brain sciences},
  volume={40},
  year={2017},
  publisher={Cambridge University Press}
}
```

## 目录

```
  摘要
  1. 导言
    1.1 范围澄清
    1.2 关键思想
  2. 认知和神经对 AI 的启发
  3. 构建更像人的机器中的挑战
    3.1 字符挑战
    3.2 Frostbite 挑战
  4. 人类智力的核心元素
    4.1 “启动软件”
      4.1.1 物理常识
      4.1.2 心理常识
    4.2 快速建模式的学习
      4.2.1 组合性
      4.2.2 因果性
      4.2.3 元学习
    4.3 快速思考
      4.3.1 结构化生成模型中的近似推理
      4.3.2 基于模型的与无模型的强化学习
  5. 回答一些常见问题
    5.1 人类与神经网络在具体任务上的速度比较没有意义，因为人类有广泛的先验知识
    5.2 理论上智力始于神经网络更符合生物合理性
    5.3 语言对人类智力至关重要，为什么却很少提及？
  6. 展望
    6.1 深度学习的前景
    6.2 实际 AI 问题的未来应用
    6.3 走向更像人类的学习和思考机器
```

## 摘要

真正像人类学习和思考的机器必须在能学什么以及如何学习两方面超越当前的工程趋势。它们应能：

1. 建立便于解释与理解的因果模型；
2. 用物理与心理的基础理论支撑并加深所学；
3. 通过组合性（Compositionality）与元学习（Learning-to-learn）快速获取知识并推广到新的任务和场景。

## 1. 导言


对于“像人一样学习与思考的机器”，本文有如下主要内容：

1. 回顾当前对其的一些标准；
2. 结合理论与实验数据，说明我们认为其必需的元素；
3. 以上元素很多尚未纳入现代的深度学习模型，造成机器解决问题的方式可能不同于人类；
4. 讨论其最可行的实现路径。


除此之外，我们还对基于统计的模式识别方法和建模方法做了更广泛的区分。  
前者以预测为主，发现具有高价值状态的共同特征；后者以建立现实世界的模型为主，以此理解和解释现实世界、想象和实现未来世界。


我们还讨论了模式识别方法虽非建模方法的核心，但仍对其有所帮助。

### 1.1 范围澄清

AI 有两种，一种据称是模拟人类的认知，从其概念中汲取灵感，另一种则不是。  
本文聚焦于前者：我们相信尤其是在人类更加擅长的领域，解构人类的智力可改进 AI/ML。

另外，本文虽聚集于神经网络方法，但这并非 AI 的唯一改进方向。



### 1.2 关键思想

本文的中心目标是提出一套用于建立更像人一样学习和思考的机器的核心元素。分为三组：


1. “启动软件”，即初期的认知能力。有助于学习新任务和加快学习。包括：
   1. 物理常识；
   2. 心理常识。


2. 学习能力。我们认为其要点在于建模，即通过建立世界的因果模型来解释观察到的数据。人类之所以能够快速建模，是因为：
   1. 组合性；
   2. 元学习。


3. 实时应变。
   1. 神经网络与建模方法结合进行推理；
   2. 我们证明人类结合了基于模型的和无模型的两种学习算法。这一方向尚未应用但极有前景。

## 2. 认知和神经对 AI 的启发


Turing 认为类人机器的实现方式应该是先实现一种像小孩一样一片空白的基础机器，然后通过奖惩对其进行训练（类似强化学习）。


当时大多研究者认为知识是可以符号化、可以通过演算的方式被理解的。  
与此同时却出现了一种“深层符号化（sub-symbolic）”的类神经方法，导致人们提出认知的本质是“并行分布式处理（PDP）”。  
神经网络乃至之后的深度学习都借鉴了 PDP 模型。

值得说明的是 PDP 的观念与“建模”是相容的，同时也与“模式识别”相容。


神经网络模型与 PDP 似乎都暗示人脑是深层符号化的，只存在少量的约束或感性成见用于指导学习。

因此常见的科研策略是训练一个相对通用的神经网络去完成任务，而只在必要时才添加其它元素。

那么问题来了，如果不添加这些额外元素，我们能开发出真正的像人一样学习与思考的机器吗？如果不能，又能多接近这个目标？

## 3. 构建更像人的机器中的挑战


既然现代认知科学对人脑或智力尚无定论，那么声称其是一组没多少初始约束的通用神经网络集合是很极端的。

因此出现的另一种看法强调早期感性成见的重要性，以及强调依靠先验知识从少量训练数据中提取知识的强大学习算法。


这里我们先举两个 ML/AL 面临的难题：简单视觉概念与 Frostbite 游戏，并在后面以其为例说明核心认知元素的重要性。

### 3.1 字符挑战


神经网络在文字识别与更大规模图片分类任务中的表现都与人相当，但这并不表示人类与机器的学习思考方式一样，区别主要有两点：

1. 人类能通过更少的例子学习到更多的表示形式；
2. 人类不但能学会识别模式，还能从中归纳出概念，并进行应用。


更高难度的挑战可能需要结合深度学习和概率性程序归纳（Probabilistic Program Induction）才能解决。

### 3.2 Frostbite 挑战


DQN 是强化学习的一个重大进步，证实了即使只用单一的算法也能学会多种的复杂任务。

DQN 结合了模式识别的 Deep CNN 模型和无模型强化学习的 Q-learning 算法。


除了对固有的图像结构的假设，该网络中内置的东西很少，因此每个新游戏都必须从头开始为学习视觉和概念系统。  
但更新的研究表明这些不同游戏的神经网络之间可以共享视觉特征、用于训练复合任务，以及帮助学习新的游戏。


Frostbite 游戏的研究表明即使是玩过了上千款游戏的深度网络，也需要上千小时的训练才能达到游戏新手玩几分钟就能达到的效果，并且仅限于特定的输入和目标。  
而人类对游戏的理解更加深刻，不同于 DQN 更依赖于靠不断完成小目标的反馈来最终达到大目标，人类很容易就能理解更高层次的大目标。  
并且人类可以从学习中总结出模型，并灵活应用于任意新的任务或目标。


所以人类的特殊之处在哪里？如果仅是有更丰富的先验知识，要如何使用这些先验知识才能帮助机器快速学习与解决问题？

## 4. 人类智力的核心元素


导言中提到的元素不一定全面，但确是当今大多数基于学习的 AI 系统所不具备的重要部分。

我们说“核心元素”时并不表示某个元素一定是天生的或者某个算法预装的。  
我们不打算讨论这些关键元素的来源。诚然这些核心元素受益甚至直接来源于先验知识，但我们想强调的是它们在建立更像人的机器中起着重要作用，却并未应用在现今的机器学习中。

### 4.1 “启动软件”

#### 4.1.1 物理常识


小孩在一岁前就能依次建立起物理的规律、表象与概念，其成因尚无定论。  
最新的研究将物理常识看作基于物理模拟引擎的推导。照此说法，人类是通过主观对物理性质的理解重建所感所知。  
这种“物理常识引擎”尽管粗糙和简略，却足以对事物的短期运动进行判断。并且即使缺少感知线索，也能灵活地适应多种日常场景。


将物理常识集成进深度学习系统有什么前景？


包括基于深度 CNN 的 PhysNet 在内的方法，虽然表现不错，但都需要大量训练，来完成单一的任务，且仅限于小范围的场景，缺乏人类的灵活性。


抛开这种脱离物理模拟进行预测的方法，我们换个方向，神经网络可以像小孩一样经过训练就掌握对通用物理知识的模拟吗？  
这里面的挑战在于，通用神经网络通过训练掌握的是暗知识，它能像掌握了明确物理概念的人类一样将知识推广到训练场景以外的地方吗？


无论是用神经网络学习物理的暗知识，还是在模拟器中预装物理的明知识，深度学习要集成物理常识可能很难，但会为学习速度和效果带来巨大提升，这会是通往更像人的学习算法的重要一步。

这个方向还没有研究，我们觉得可以有。

#### 4.1.2 心理常识


婴儿开口说话前就懂得通过对低级线索的天生感知区分主体和客体，随后可进一步分辨主体的不同社会性。  
通常认为婴儿期望主体活动是目标驱动的、有效的、社会性的。


一个解释把心理常识看作简单推论的叠加。  
虽然推论本身容易计算，但场景既可能复杂，需要更多数量的推论，也易于变化，需要更多类型的推论。  
这都会使得基于推论组合的表示迅速膨胀。


另一个解释认为心理常识就是对行为选项的生成模型。假设人们期望其它主体都是行为理性的，即人类通过模拟其它主体的规划过程来根据它们的目标预测它们的下一步，或者根据它们的一系列动作反推出它们想干嘛。  
这种心理常识中基于对其它主体进行模拟的推理还可以递归嵌套，进而理解到社交。


深度网络是可能学习到涉及主体的场景中的视觉线索、启发法和摘要统计的，如果这就是人类心理推理的全部基础，那么数据驱动的深度学习方法早就在涉及心理理论和心理常识的领域取得成功了。  
所以与物理常识一样，通用深度网络能否获得心理常识推理，部分还取决于人类对心理常识的表示。  
就像不理解物理常识就难以推广，不理解心理常识就难以推理。


然而任何心理常识推理的完整表示都包含了主体、目标、效率、互惠关系的概念。而这些概念尚不确定能否被单纯训练预测能力的深度网络学到。  
因为通过大量训练后，即使没学到这些概念，也有了接近婴儿的推理能力。  
而且这些概念也不一定真就是人类学习、理解，以及应用心理常识的真实抽象。


除了预装，心理常识还有多种方式可与现代的深度学习系统结合。  
例如用少量感性成见激发推理出更多主体的抽象概念，将大量的目标导向行为和社会导向行为分解为简单元叠加的结果。


心理常识的起源仍有争议，但对人类学习与思考非常重要。

### 4.2 快速建模式的学习

自成立以来，神经网络模型一直强调学习的重要性。无论什么算法，都将学习当作一个对数据间联系的强度进行逐步调整的过程。

最近又因 BP 神经网络与大数据集解决了困难的模式识别问题而使机器学习大获成功。但即使在少数问题上与人相当，它们在大多其它问题上仍远不如人。


深度神经网络需要更多的数据。

在学习母语词汇时，儿童能对非常稀疏的数据进行有意义的归纳，比成人更善于学习新概念。  
与高效的人类学习相比，神经网络因其通用性而总是渴求更多数据，显然它们对信息的利用率并不高。


必须指出，在很多领域机器比人更擅长，并且有很多困难的概念人类学起来也很慢，但对大多数认知类自然概念（类似小孩学词语），人类都学得更好。这类学习是本节主要内容，它是人类学习之所以成功的基石，更适合我们解构与重建。并可能集成到下一代 ML/AL 算法中，有望使其在概念的学习中取得进步。


即使只有一点样例，人类也能学到实用的概念上的模型，并灵活运用。

这种实用与灵活表明建模学习法比模式识别学习法更近似人类。

其它类型的任务上机器也不具备人类这样从小数据集中学到通用知识的能力。另外，神经网络能轻易推广到新任务上的知识表示也是很难学习的。


但我们基于贝叶斯程序学习（BPL）做了个字符挑战的模型，将概念表示为可复用的似然图元按一定结构进行的组合，使用不同的方式可组合成不同的概念。对于新的概念，只要一个例子就可以生成其它新的例子（结构不变，替换图元为其它似然图元）。

BPL 这种学习模型在具有挑战性的一次性分类任务上表现与人相似，优于 CNN 等深度学习模型，并可创造性地推广，就是因为有接下来要讨论的三个元素：组合性、因果性和元学习。

#### 4.2.1 组合性


组合性是很经典的想法：新的概念可表示为原始元的组合。  
组合性在 AI 和认知科学中都有广泛的影响。  
组合性与元学习天然搭配，但也有依赖更少前置学习的组合形式。  
通过组合，字符挑战的学习模型就具备了可操作性，Frostbite 挑战也可以更有效。


深度网络至少有有限的组合性概念，不但部件、物体、场景这些概念内含了组合性，组合性对于目标分解也很重要。  
我们希望深度网络能有更丰富的组合性概念，以学得更快更灵活。


另外，模型要明确表示物体、个性和关系需要协调一致，也就是下面要说的因果性。

#### 4.2.2 因果性


概念学习与场景识别中，因果模型是对真实过程的假设；控制与强化学习中，因果模型是环境结构的表示。  
带因果性的概念学习与视觉模型通常是可生成的，但不是所有可生成模型都是因果性的。  
因果性在感知理论中很有影响力，但它不一定得是真实生成机制的严格逆变换。

因果知识会影响人们如何学习新的概念。  
因果性对于学习的重要性在于它强化概念的核心特性之间的联接、弱化其它。


理解场景时，人类也会建立因果模型，集成物理常识、心理常识和组合性，解释与描述表象。  
缺少这三者以及将它们联接起来的因果性，就会导致错误认识，例如图像描述生成。


深度网络相关的方法学会因果模型还有很多路要走，近来出现的相关改进还都存在各自的问题，但它们的改进点都可以解释为对真实因果的近似，所以因果性是有大幅改进深度学习模型的可能的。


在更复杂的因果模型中，深度网络可能有两种使用方式：作为结构化生成模型的底层，使概率推理更容易，或在元素齐全时作为因果生成模型。

#### 4.2.3 元学习


先验知识一定会导致人类和机器对数据进行推理的不同。
“元学习”是先验知识的获取方式之一，与“转移学习”“多任务学习”“表示学习”紧密相关。它使得对任务的学习可以加速其它任务的学习。

这一机制已有一批实现，但仍不如人类快速与灵活。也许它们需要先实现更有组合性、因果性的表示形式。


元学习有潜力帮助解决本文所举的两个挑战。


目前的神经网络方法离解决字符挑战还远，却需要远多于人类的前置训练。  
我们不确定人类是如何获得这些领域的知识的，但也许类似 BPL。  
元学习已经应用在 BPL 生成过程的多个层次中，我们还可以像人类一样，将生成好的重要结构作为 BPL 的先验知识。  
此外类比学习也发生在很多人类学习新模型的过程中，我们相信这里面的组合性、层次性、因果性对深度网络也是有益的。


在 Frostbite 一类的电子游戏的挑战中，元学习的高效与知识的表示形式密不可分。人类的知识转移发生在从认知到策略的各个层次，一方面迅速识别出游戏场景里的物体，一方面理解游戏的目标与正反反馈，这都依赖于已有的现实知识与游戏经验。

深度强化学习在转移学习中很成功，但仍不像人类学玩新游戏这么快。


总之，经验与表示之间的交互也许是建立像人一样快速学习的机器的关键。

### 4.3 快速思考


上一节集中论述了从稀疏数据中学习丰富模型的类人能力，人类的这种能力最惊人的就是它的速度。

丰富模型配合高效推理是另一种可利用心理学与神经学的方法，这也可能是建立成功深度学习的新方法。

这一节讨论解决快速推理与结构化表示之间冲突的两个可能方法。

#### 4.3.1 结构化生成模型中的近似推理


多层贝叶斯模型能解决现实的理论结构与因果表示，但因计算量大而不实用。对学习与推理的完整描述必须能解释为何人脑可以只用有限的计算资源就做到这么多事。

概率机器学习中近似推理的热门算法已作为心理学模型被提出，最突出的是提出人类通过蒙特卡罗方法逼近贝叶斯推理。


蒙特卡罗方法虽然功能强大且具有渐近保证，但对程序归纳和理论学习等复杂问题的处理仍是一项挑战，通常为了寻找一个好的模型不得不遍寻整个庞大的假设空间。  
但人类不同，他们不是渐近地搜寻最好的办法，而是通过跳跃式的学习将知识碎片快速拼凑成符合因果的理解，与蒙特卡罗随意的推理模式不同，这更像是一个有指导的过程。


在快速学习领域，人类的感性成见很可能不只是用于对假设进行评估，还用于指导假设的选用。这种从问题到可能答案之间的快速映射要如何学到？


最近的成果是用一种高效的前馈映射分摊概念推理的计算，这种分摊的意义还在于，由于存在共享的分摊部分，不同问题的解决方案是相关的，而有证据表明人类的推理就是具有相关性的。  
这是深度学习模型集成概率模型与概率程序的一条潜在道路，即训练神经网络进行生成模型或概率程序中的概率推理。

另一条道路是基于梯度下降的微分程序。

#### 4.3.2 基于模型的与无模型的强化学习


有实质性的证据表明，人类在简单的联想学习或区分学习任务中使用了类似 DQN 的无模型学习算法，能够快速选用行动。

同时，大量证据表明人类还有基于模型的学习系统负责建立对环境的“认知地图”，并用来进行复杂任务的行动规划。  
这对人类智力是必需的，使人类能灵活地适应新的任务与目标。

但同时，人类日常事务的“习惯化”也许表明基于模型的规划可能转向无模型的快速估算，这可能是源于学习系统对灵活性与速度的权衡。


人类的强化学习系统是通过基于模型的系统模拟训练数据供给无模型系统，将行动规划的计算分摊并提前缓存，这一过程可以离线完成（例如对人来说，可能是睡觉时或发呆时）。于是就兼顾了灵活性与效率。


内在动机对人类的学习与行为也很重要，深度强化学习刚开始探索这个方向。

## 5. 回答一些常见问题

### 5.1 人类与神经网络在具体任务上的速度比较没有意义，因为人类有广泛的先验知识

人类不但有相关或不相关任务的经验，甚至还经历了长期的进化，有长期历史的“提前训练”确实是多任务学习和转移学习的道理。


这些都形成了前面提到的“启动软件”或其它模块，但我们的重点不是讨论这些是怎么形成的，而是说这些是促进从稀疏数据中快速学习的基础模块。

多任务间的元学习是形成这些模块的可信道路，但仅靠大量训练相关任务的 CNN 是不够的，因为元学习还取决于建立有正确表示结构的模型。


有些研究者仍觉得给深度学习足够大的训练数据有望学到媲美人类的先验知识，我们觉得这不现实。因为要从头建立起人类的知识表示可能需要探索网络架构中的基本结构变化，目前的这部分探索与创造性工作还是由作为研究者的人类本身完成，这不是权重空间中基于梯度的学习能做到的。

另一个方向是为基于学习的 AI 系统建立接近婴儿的知识表示与核心元素或感性成见。


不论 AI 开发者选哪个方向，都可以与本文提出的认知元素相协同，并不矛盾。

### 5.2 理论上智力始于神经网络更符合生物合理性


不同于宣称受神经科学启发的深度神经网络，我们主要聚焦在认知科学如何指导和促进类人 AI 的工程上，毕竟相比于“硬件”，人类智力的形成明显来自于对“软件”的理解。


神经科学确实给认知模型和 AI 研究者都提供了宝贵的灵感，但同时也有很多似是而非却被广泛接受的观念，不足以用来否定我们的方法。  
比如现今最好的模式识别系统中起着重大作用的反向传播就并不符合生物合理性，还有 Hebbian 学习中的认知学意义也没什么生物学的根据。


所以我们当然相信未来神经科学能对智力理论提供更多的条件，但当前，认知合理性还是比生物合理性更重要。

### 5.3 语言对人类智力至关重要，为什么却很少提及？


人类使用自然语言进行交流与思考的认知能力远强于机器，人们已广泛认识到神经网络离具备人类语言能力还差得很远。我们怎样让机器有更强的语言能力呢？  
我们相信理解本文提出的元素有助于理解语言对于智力的作用，因为这些元素先于人类掌握语言和语义存在。


学会语言还需要什么？不知道，但我们的元素列表不一定是全面的。获得语言能力所需要的元素都应加入这个列表，因为语言对人类智力确实至关重要，建立像人一样学习与思考的机器最终必须具备语言能力。

## 6. 展望


近年 ML/AI 取得了极大进展，但还不能超越人类。

人类能从更少的数据中学习并进行灵活与丰富的应用，我们认为这是人类知识表示的因果性与组合性带来的。

结束前我们谈一下深度学习的前景。

### 6.1 深度学习的前景

近来的一个趋势是在深度网络中集成心理学的元素，尤其是选择性关注、强化工作记忆、经验重放等，这些方法的结合是建立类人 AI 的重要一步。

另一个模式识别与基于模型搜索的例子来自围棋，AI 对于围棋的挑战不仅是已经达到的世界级棋力，还像人一样尝试基于相同类型与数量的数据、明确的规则、社会学习机会来理解与归纳围棋。我们相信围棋也可作为本文探讨的元素的测试平台。

### 6.2 实际 AI 问题的未来应用

1. 场景理解。现在深度学习已经超脱物体识别，开始进入对场景的理解。组合性、因果性、物理常识与心理常识缺一不可。
2. 自主主体与智能设备。需要具备从小样本中学习新概念的能力，这离不开因果过程和元学习。
3. 无人驾驶。完美的无人驾驶必须具备心理常识，以理解其他司机和行人的动向。
4. 创造性设计。组合性与元学习提供新创意，因果性保证设计能协调一致。

### 6.3 走向更像人类的学习和思考机器


希望我们在本文提出的元素有助于机器实现以下目标：

1. 认识物与主体，而不是特征；
2. 建立因果模型，而不是识别模式；
3. 重组知识表示，而不是重新训练；
4. 学会学习，而不是重头开始。

## [评论](https://github.com/cf020031308/cf020031308.github.io/issues/18)
