# Chapter 0 - Introduction
## 0.1 - Rational Agent
> 理性代理(Rational Agent)是根据其感知到的**环境信息**，通过一定的**决策过程**，**采取行动**以实现**特定目标**的代理。
> 理性(Rational)在这里指的是**做出最优选择**或**最大化预期效用**。
> 一个理性代理的行为会根据其所掌握的信息，通过**某种决策过程**做出最合适的行动。这些所掌握的信息包括：
> 	- 知识库：所知道的这个世界的信息
> 	- 感知序列：他观察到的环境状态序列
> 	- 目标：代理需要实现的任务或效用函数
- **Rational** behavior: doing the right things
- An agent is an entity that perceives and acts
- An agent is a function from **percept histories** to **actions**, i.e.:
$$f:\ P*\to A$$
- We seek the best-performing agent for a certain task, and must consider computation limits.
### Function from percept histories to actions
$$f: P* \to A$$
- $P*$: Anything that can be viewed as **perceiving** its **environment** through **sensors**; **acting** upon that environment through **actuators(执行器)**. 表示所有可能的感知序列的集合。星号（ * ）通常用于表示序列可以是任意长度的，包括零。这些感知序列代表了代理从环境中获得的信息，可能包括视觉、听觉或其他感官的数据。在不同的时间点，代理可能会感知到不同的环境状态。
	- **Actuators (执行器)**: 指将软件系统的决策转化为物理世界动作的设备或机构部件。例如机器人的电机，伺服机等，他们能够执行移动和操作对象的任务
	- *Human agent*: eyes, ears, skin etc. are sensors; hands, legs, mouth, and other body parts are actuators.
	- *Robotic agent*: cameras and laser range finders for sensors; various motors for actuators.
- $A$: 表示所有可能行动的集合。行动是代理(agent)课执行的操作，比如移动，说话，或进行某种计算等。
- $f$: 是一个函数，他将**感知序列映射到行动上**。这意味着基于代理过去的感知（即它所经历的环境状态序列），函数$f$将决定代理接下来应该执行什么行动
- 在代理模型中，此函数**实质上定义了代理的行为策略**。换句话说，此函数是一个决策规则或策略，告诉代理在任何给定的情况下该如何行动以达成目标。这个映射可以通过各种方式实现，包括但不限于查表法，基于规则的系统，机器学习模型等。在理想情况下，函数$f$应该是**理性的**，意味着函数可以帮助代理以某种方式最大化其性能度量或达成目标。
## 0.2 - Task Environment
以下的概念，与之前讨论的理性代理概念紧密相关。这些概念直接影响理性代理的设计，决策制定能力和行为表现。理性代理的目标是在给定环境中做出最佳的决策，以实现其设定的目标或最大化其效用。
### Fully Observable (vs. Partially Observable)
- Sensors provide access to complete state of the environment at each point of time
- **完全可观测性**：在一个完全可观测的环境中，智能代理可以获取到环境的所有状态信息，这意味着代理的每一个决策都可以基于对当前环境状态的全面了解来进行。棋类游戏（如国际象棋）是完全可观测环境的典型例子，因为玩家可以看到棋盘上所有棋子的位置。
- **部分可观测性**：相反，在一个部分可观测的环境中，代理无法获得环境的全部状态信息，这可能是因为信息被隐藏了，或者代理的感知能力有限。在这种环境中，代理需要基于不完全的信息作出决策。大多数真实世界的情况都是部分可观测的，例如自动驾驶汽车不能完全知道其他车辆的意图。
### Deterministic (vs. stochastic)
- The next state of the environment is completely determined by the current state and the action executed by the agent
- **确定性**：在确定性环境中，当前状态和采取的行动可以唯一确定下一个状态。这意味着如果代理对环境的操作和环境本身都是已知的，则环境的反应（即下一个状态）是可以预测的。
- **随机性**：在随机性环境中，当前状态和行动不能唯一确定下一个状态。即使在相同的状态下采取相同的行动，环境的反应（即下一个状态）也可能因随机因素而有所不同。很多真实世界的环境都是随机性的，因为它们受到很多不可控因素的影响。
### Episodic (vs. sequential)
- The choice of **current** action does not depend on actions in past episodes
- Alternatively: **current** action does not affect future decisions
- **情节性**：在情节性环境中，代理的经历被划分为独立的“情节”，每个情节中的决策和行动不会影响到其他情节。在每个情节中，代理的目标是在给定的情节内做出最优决策。例如，一个图像识别系统对每张输入图片的处理可以看作是一个独立的情节。
- **顺序性**：与情节性不同，顺序性环境中的决策是连续的，当前的决策会影响到未来的状态和决策。顺序性环境要求代理考虑长期策略，因为其行动会对未来产生连锁反应。大多数策略游戏和真实世界问题都是顺序性的。
## 0.3 - Properties of Task Environment
### Static (vs. dynamic)
- The environment is unchanged while an agent is deliberating (审议)
### Discrete (vs. continuous)
- A finite number of distinct states, percepts, and actions
### Single Agent (vs. Multi-agent)
- An agent operating by itself in an environment
## 0.4 - Agent Functions and Programs
### Table-Lookup Agent
查表代理（Table Lookup Agent）是一种基本的人工智能代理设计模式，其行为决策完全基于一个预先定义的查找表。这个表格详细列出了代理可能遇到的每一个环境状态以及对应于每个状态的最佳行动。在任何给定的时间点，代理通过查询这个表格以确定其当前状态对应的最佳行动，并执行该行动。这种代理不涉及任何学习过程或对环境的动态适应；它的所有决策都是静态定义并且固定的。

查表代理的核心特点如下：
- **静态决策规则**：所有的行动决策都是预先定义好的，代理在运行时不会改变这些决策规则。
- **完全依赖于预定义表格**：代理的所有决策都依赖于这个查找表，这意味着表中必须包含代理可能遇到的每一种环境状态。
- **简单但有限的适用性**：查表代理因其设计简单而易于实现，但只适用于状态空间非常小的问题。随着状态空间的增大，所需存储的表格迅速变得庞大并不可行。
- **无学习能力**：查表代理在其生命周期中不具备学习或适应环境变化的能力。所有决策都是基于其初始编程，而不是通过经验学习得来的。

- Drawbacks:
	- Huge table to store
	- Take a long time to build the table
	- No autonomy: impossible to learn all correct table entries from experience
	- No guidance on filling in the correct table entries
### Agent Types
#### 简单反射代理 Simple reflex agent
- Passive(被动): only acts when observes a percept(感知)
- Updates state based on percept only
- Easy to implement
> 简单反射代理是最基础的代理类型，它们根据当前的感知直接选择行动，不考虑过去的状态或行动的历史。这种代理通常使用一系列的条件-行动规则（if-then规则）来决定怎样行动。例如，一个简单反射代理可能有一个规则：“如果感知到前方有障碍物，则转向”。简单反射代理的主要局限性是它们无法考虑历史信息，只能基于当前的感知做出反应。

例子：
一个简单的温控系统。如果室温低于设定的最低温度阈值，则加热器开启；如果高于设定的最高温度阈值，则加热器关闭。这个系统**直接根据当前的温度感知来做出行动决策**，**不涉及过去的温度变化和未来的预测**
#### 基于模型的反射代理 Model-based reflex agent
- Passive: only acts when observes a percept
- state is updated based on percept, current state, most recent action, and model of world
> 基于模型的反射代理维护一个**内部状态的模型**，该模型代表了此代理关于世界的知识。这允许代理在做出决策时**考虑到世界的变化**，即使这些变化当前无法通过感知直接观察到。基于模型的代理使用这个世界模型来预测不同性的的后果，从而做出更加合理的决策。这种类型的代理可以处理部分可观测的环境。

例子：
一个室内照明控制系统。他不仅根据房间的当前光线强度来开关灯光，还考虑到房间**使用模式和时间**（例如，如果是夜间且没有人在房间内，即使房间暗，灯也不会开启）。这个系统使用了一个**内部模型**来**预测房间的使用情况**，从而做出更合适的决策。
#### 目标导向代理 Goal-based agent
- Has **goals**, acts to achieve them (not passive)
- state is updated based on percept, current state, most recent action, and model of world
> 目标导向代理除了维护关于世界的模型之外，还有一个或多个的目标，用来指导其决策的过程。这些目标定义了代理希望达成的状态，代理的行动选择不仅基于对当前世界状态的理解，还基于**其行动是否帮助它达到这些目标**。目标导向代理在决策时会考虑多种可能的行动序列，并评估哪一系列行动最可能达成其目标。

例子：
一个自动驾驶汽车系统。他的目标是安全地将乘客从一个地点运送到另一个地点。为了时间这个目标，代理需要考虑当前的交通状况，路况，交通法规以及潜在的障碍物等**多种因素**来做出决策。
#### 基于效用的代理 Utility-based agent
- Has **utility function**, acts to maximise it
- state is updated based on percept, current state, most recent action, and model of world
> 基于效用的代理在目标导向代理的基础上引入了效用概念，它们不仅追求达成目标，还试图最大化某种效用函数。**效用函数是一种衡量某状态好坏的评价标准**，它允许代理在面对可能达成多个目标的情况下做出选择。基于效用的代理选择的是那些根据效用函数评估结果最优的行动，这允许它们在相似或冲突的目标间进行权衡。

例子：
一个投资顾问软件。基于用户的风险偏好（效用函数），软件分析并推荐不同的投资组合。对于风险厌恶型的用户，它可能推荐债券或货币市场基金；对于风险承受型用户，他可能推荐股票或投资基金，以最大化用户的长期收益和满意度。
# Chapter 1 - Intelligent Agents
## 1.1 - Motivation
- An intelligent agent can:
	- Sense, or otherwise gather information about the environment around it.
	- Form “sentences” about what it has sensed, and store these in its “Knowledge Base”
	- Infer new knowledge from the knowledge base
	- Make decision and take actions using “actuators” based on these decisions
## 1.2 - Example Agent Components
### Sensors
- Infrared sensors, LIDAR, microswitches, accelerometers and gyroscopes
- Tells the agent about the **environment**
- May also get this information from other computer systems
### Knowledge Bases
- Made up of:
	- A domain independent inference engine that infers knew knowledge and makes decisions
	- A domain dependent knowledge base consisting of “sentences” specified in a formal language
> **推理引擎(inference engine)：** 负责从知识库(knowledge base)中提取只是，并使用这些知识通过逻辑推理来解决特定问题。
> **领域独立算法(Domain-independent algorithm):** 不针对任何特定领域的问题或数据设计的算法。这类算法具有广泛的适用性，可以被应用于多个不同领域的问题解决中，通常解决一些通用的问题，例如排序，搜索，优化等。这类算法的特点是在解决问题时**不依赖于领域特定的知识**
> **领域特定内容(Domain-Specific content):** 针对特定领域(如医疗，金融，环境科学等)的知识，数据和解决问题的策略。领域特定内容可以使人工智能更有效地处理特定类型的问题。
### Actuators
- Devices that the agent uses to **effect changes in its surrounding**
- Examples: Motors, solenoids, relays, speakers, LEDs
### A simple knowledge-based agent
![image.png](https://images.wu.engineer/images/2024/03/08/202403082216336.png)
- `Tell(KB, Make-Percept-Sentence(percept, t))`: **更新知识库**。将当前的感知转换成一句话，并告诉（更新）知识库。
- `action <- Ask(KB, Make-Action-Query(t))`: **行动决策**。询问知识库在*当前时间点*应当采取什么行动。这个查询基于当前知识库的状态，并考虑了所有至今为止的感知信息。
- `Tell(KB, Make-Action-Sentence(action, t))`: **执行行动并更新知识库**。一旦行动被决定，这个命令将此行动以一种句子的形式告诉（更新）知识库，意味着知识库会记录下这个行动和对应的时间。
- `t <- t+1`: **时间推进**。为下一次感知做准备。
- `return action`: **返回行动**。最后，函数将决定的行动返回给代理执行。
## 1.3 - Logic
- **逻辑（Logic）**：是一种符号系统，它包括形式语言、操作符和推理规则，使我们能够关于周围世界得出合理的结论。在人工智能中，逻辑被用来表示事实、事件、对象之间的关系，以及推导出新的知识。
- **命题逻辑（Propositional Logic）**：是逻辑的一种形式，它处理关于具体事物的具体陈述。命题逻辑中的基本元素是命题，命题可以是真也可以是假，但不涉及更复杂的结构，如对象的属性或它们之间的关系。
- **一阶逻辑（First Order Logic，也称谓词逻辑 Predicate Logic）**：是比命题逻辑更复杂的逻辑形式，它允许我们讨论类别或群组的事物，并可以表达事物的属性和事物间的关系。一阶逻辑使用量词（如存在量词“存在”，全称量词“对所有”）来表达语句。
- **Logic**: A system of symbols, formal language, operators and inference rules that lets you draw sound conclusions about the world around you.
- **Propositional Logic**: This is logic over particular statements about particular “things”
- **First Order Logic (Predicate Logic)**: This is logic over classes and groups of “things”
- Our knowledge base will then consist of:
	- Observations from our sensors, written as statements in our logic language
	- A set of conclusions that can be drawn from the observations, again written as statements in our logic language
	- A set of inference rules that can be applied to derive valid conclusions and actions to be taken
# Chapter 2 - The Logic of Compound Statements
## 2.1 - Logical Form and Logical Equivalence
### 2.1.1 - Statements
- If *Jane is a math major* or *Jane is a computer science major*, then *Jane will take MA1101R*
- *Jane is a computer science major*
- Therefore, *Jane will take MA1101R*
Above are statements.

- A **statement** (or **proposition**) is a sentence that is true or false, but not both.

- If `p` or `q`, then `r`
- `q`
- Therefore, `r`
Above the `p,q,r`, are **statement variables**
### 2.1.2 - Compound Statements
![image.png](https://images.wu.engineer/images/2024/03/09/202403091431692.png)
- **Negation**: If `p` is a statement variable, the **negation** of `p` is “**not** `p`” or “it is not the case that `p`” and is denoted as `~p`
- **Conjunction**: If `p` and `q` are statement variables, the **conjunction** of `p` and `q` is “`p` and `q`”, denoted as $p \wedge q$
- **Disjunction**: If `p` or `q` are statement variables, the **disjunction** of `p` and `q` is “`p` or `q`”, denoted as $p \vee q$
- **Order of operations**:
	- ~ is performed first
	- $\vee$ and $\wedge$ are **coequal** in order of operation
	  ![image.png](https://images.wu.engineer/images/2024/03/09/202403091438646.png)
- Use **parentheses(括号)** to override or disambiguate order of operations
![image.png](https://images.wu.engineer/images/2024/03/09/202403091439191.png)
- Given:
	- h = “It is hot”
	- s = “It is sunny”
- Write logical statement for the following:
	- It is *not hot* but it is sunny
	  ~h $\wedge s$
	- It is *neither* hot nor sunny
	  ~h $\wedge$ ~s or ~$(h\vee s)$
### 2.1.3 - Statement Form
- A **statement form** (or **propositional form**) is an expression made up of *statement variables* and *logical connectives* that becomes a statement when actual statements are substituted for component statement variables.
- **XOR (Exclusive-OR)**
  ![image.png](https://images.wu.engineer/images/2024/03/09/202403091447123.png)
	- $(p \vee q) \wedge \neg (p \wedge q))$
	- Denoted as $p\oplus q$ or $p\ XOR\  q$
### 2.1.4 - Logical Equivalence
![image.png](https://images.wu.engineer/images/2024/03/09/202403091450337.png)
- Two statement forms are called **logically equivalent** if, and only if, they have *identical truth values* for each possible substitution of statements for their statement variables. The logical equivalence of statement forms P and Q is denoted by $P \equiv Q$
![image.png](https://images.wu.engineer/images/2024/03/09/202403091452224.png)
- **Double Negation**
![image.png](https://images.wu.engineer/images/2024/03/09/202403091452312.png)
#### Showing Non-equivalence
- To show that statement forms P and Q are *not* logically equivalent, there are two ways:
	- *Truth table* - find at least one row where their truth values differ
	- Find a *counter example* - concrete statements for each of two forms, one of which is true and the other of which is false.
![image.png](https://images.wu.engineer/images/2024/03/09/202403091456841.png)
![image.png](https://images.wu.engineer/images/2024/03/09/202403091456046.png)
#### De Morgan’s Laws
![image.png](https://images.wu.engineer/images/2024/03/09/202403091500848.png)
- Write negations for each of the following:
	- John is 6 feet tall and he weighs at least 200 pounds
	  *John is not 6 feet tall or he weighs less than 200 pounds*
	- The bus was late or Tom’s watch was slow
	  *The bus was not late and Tom’s watch was not slow*
	  or *Neither was the bus late nor was Tom’s watch slow*
### 2.1.5 - Tautologies and Contradictions
- A **tautology** is a statement form that is **always true** regardless of the truth values of the individual statements substituted for its statement variables. A statement whose form is a tautology is a **tautological statement**
  **重言式(tautology)**：是一种总是真的逻辑陈述，不管其组成部分的真值如何。重言式在所有可能的情况下都是正确的。例如，在命题逻辑中，陈述“P或非P”，被称为*排中律*，这是一个重言式，因为无论P的真值是什么，这个陈述总是真的。
- A **contradiction** is a statement form that is **always false** regardless of the truth values of the individual statements substituted for its statement variables. A statement whose form is a contradiction is a **contradictory statement**
  **矛盾(Contradictions)**: 是一种总是假的逻辑陈述，也就是说在所有可能的情况下都不成立。例如，在命题逻辑中，陈述“P且非P”，这个陈述不可能为真，因为P不可能同时为真和假。
### 2.1.6 - Summary of Logical Equivalence
![image.png](https://images.wu.engineer/images/2024/03/09/202403091512006.png)
![image.png](https://images.wu.engineer/images/2024/03/09/202403091512442.png)
## 2.2 - Conditional Statement
### 2.2.1 - Conditional Statements
![image.png](https://images.wu.engineer/images/2024/03/09/202403091519121.png)
![image.png](https://images.wu.engineer/images/2024/03/09/202403091529372.png)
- If `p` and `q` are statement variables, the **conditional** of `q` by `p` is “if `p` then `q`” or “`p` implies `q`”, denoted $p\to q$
  It is false when `p` is true and `q` is false; otherwise it is true
  We called `p` the *hypothesis (or antecedent)* of the conditional, and `q` the *conclusion (or consequent)*
  **条件语句(Conditional Statement)**：是一种如果-那么的语句。条件语句的真值取决的其组成部分的真值。只有当P为真且Q为假时，整个条件语句P→Q才为假。在所有其他情况下，条件语句都被认为是真的。
- A conditional statement that is true by virtue of the fact that its hypothesis is false is often called **vacuously true** or **true by default**
- In general, when the “if" part is false, the statement as a whole is said to be true, regardless of whether the conclusion is true or false
#### Order of operations
![image.png](https://images.wu.engineer/images/2024/03/09/202403091540416.png)
#### Implication law
![image.png](https://images.wu.engineer/images/2024/03/09/202403091541941.png)
### 2.2.3 - Negation of a Conditional Statement
![image.png](https://images.wu.engineer/images/2024/03/09/202403091542346.png)
### 2.2.4 - Contrapositive of a Conditional Statement
- The **contrapositive** of a conditional statement of the form “if p then q” is:
  “if ~q then ~p”
  **逆否(contrapositive)**：逆否和原始的条件语句在逻辑上是等价的，这意味着如果原始语句为真，则其逆否也是真的。
  ![image.png](https://images.wu.engineer/images/2024/03/09/202403091545858.png)
### 2.2.5 - Converse and Inverse of a Conditional Statement
- The **converse** of a conditional statement “if p then q” is:
  “if q then p”
  Symbolically, the converse of p → q is q→ p
  **逆命题(Converse)**：将原始命题假设和结论的位置互换得到的命题。逆命题在逻辑上并不一定等价于原始命题。
- The **inverse** of a conditional statement “if p then q” is:
  “if ~p then ~q”
  Symbolically, the inverse of p → q is ~p → ~q
  **反命题(Inverse)**：将原始命题的假设和结论都否定所得到的命题。反命题在逻辑上并不一定等价于原始命题。
- 反命题和逆命题在逻辑上等价，原始命题和逆否命题在逻辑上等价
![image.png](https://images.wu.engineer/images/2024/03/09/202403091553000.png)
### 2.2.6 - Only if and the Biconditional
- **Only if**: p only if q, which means p can take place only if q take place also.
![image.png](https://images.wu.engineer/images/2024/03/09/202403091601425.png)
- **Biconditional**: Given statement variables p and q, the **biconditional** of p and q is “p if, and only if, q”, and is denoted p ←> q
  **双条件(Biconditional)**：两个命题P和Q是等价的，即P成立当且仅当Q成立。这意味着P是Q的必要条件，同时Q也是P的必要条件。这个表达式仅在P和Q都为真或都为假时，才为真。
![image.png](https://images.wu.engineer/images/2024/03/09/202403091637066.png)
![image.png](https://images.wu.engineer/images/2024/03/09/202403091637697.png)
- Order of operations:
![image.png](https://images.wu.engineer/images/2024/03/09/202403091638538.png)
### 2.2.7 - Necessary and Sufficient Conditions
- If r and s are statements,
  “r is a *sufficient condition* for s” means “if r then s”
  “r is a *necessary condition* for s” means “if not r then not s” or “if s then r”
- **必要条件(Necessary Condition)**：如果命题P为真，则命题Q也必须为真，这时Q是P的必要条件。即”Q→P”
- **充分条件(Sufficient condition)**：如果命题P为真足以保证命题Q也为真，这时P是Q的充分条件。这意味着P的真实性会导致Q的真实性，即”P→Q”
## 2.3 - Valid and Invalid Arguments
- **Argument**: a sequence of statements ending in a conclusion
- An argument form is called **valid** if, and only if, whenever statements are substituted that make all the premises true, the conclusion is also true.
![image.png](https://images.wu.engineer/images/2024/03/09/202403091658503.png)
- An argument (argument form) is a sequence of statements (statement forms). All statements in an argument (argument form), except for the final one, are called premises (or assumptions or hypothesis). The final statement (statement form) is called the conclusion. The symbol $\bullet$ which is read “therefore”, is normally placed just before the conclusion.
  To say that an argument form is valid means that no matter what particular statements are substituted for the statement variables in its premises, if the resulting premises are all true, then the conclusion is also true. 
![image.png](https://images.wu.engineer/images/2024/03/09/202403091700037.png)
- When an argument is valid and its premises are true, the truth of the conclusion is said to be inferred or deduced from the truth of the premises.
- If a conclusion “ain’t necessarily so”, then it isn’t a valid deduction.
- **论证(Argument)** 是一系列陈述，旨在支持或证明某个特定观点。论证通常包含两部分：**前提(Premises)** 和 **结论(Conclusion)**。前提(premises)是支持结论的理由或证据；结论(conclusion)是从前提中推导出的陈述，是论证旨在证明的观点。
### 2.3.2 - Determining Validity or Invalidity
Testing an Argument Form for Validity
1. Identify the premises and conclusion of the argument form
   明确前提和结论
2. Construct a truth table showing the truth values of all the premises and the conclusions
   构建真值表
3. A row of the truth table in which all the premises are true is called a *critical row*.
   所有前提都为真的行被称为*关键行(Critical Row)*。有效的论证要求在所有前提都为真的情况下(即关键行)，结论也必须为真
	- If there is a critical row in which the conclusion is false → the argument form is invalid
	- If the conclusion in every critical row is true → the argument form is valid
### 2.3.3 - Modus Ponens and Modus Tollens
- **Syllogism (论证)**: An argument form consisting of two premises and a conclusion
- A famous form of syllogism is called **modus ponens (模态归谬)**
	- 给定一个条件语句(如果P，则Q)，如果知道P为真，则可以得出结论Q也为真。
![image.png](https://images.wu.engineer/images/2024/03/09/202403091722794.png)
- **Modus tollens** is another valid form of argument
  模态剥夺(Modus tollens)：如果P，则Q；非Q为真；因此非P为真
![image.png](https://images.wu.engineer/images/2024/03/09/202403091727801.png)
**Example**:
![image.png](https://images.wu.engineer/images/2024/03/09/202403091727511.png)
### 2.3.4 - Rules of Inference
- **A rule of inference** is a form of argument that is valid
	- *Modus ponens* and *modus tollens* are both rules of inference
- Other rules of inference:
	- Generalization
	  归纳：从特定的实例或情况中推导出一般性的规则
	- Specialization
	  特化：从一般性陈述或规则中推导出更具体的实例
	- Elimination
	  排除法：通过消除不可能或不适用的选项来逼近问题答案
	- Transitivity
	  传递性：如果一个关系在一对对象间成立，并且也在第二对对象间成立，那么它同样在第一对和第三对对象间成立的逻辑
	- Proof by Division into Cases
	  分情况证明：将问题分解为几个更容易管理的情况或子问题，并分别对每种情况进行证明
#### Generalization
![image.png](https://images.wu.engineer/images/2024/03/09/202403091730742.png)
#### Specialization
![image.png](https://images.wu.engineer/images/2024/03/09/202403091737792.png)
#### Elimination
![image.png](https://images.wu.engineer/images/2024/03/09/202403091739987.png)
#### Transitivity
![image.png](https://images.wu.engineer/images/2024/03/09/202403091740966.png)
#### Proof by Division into Cases
![image.png](https://images.wu.engineer/images/2024/03/09/202403091742643.png)
### 2.3.5 - Fallacies
- A **fallacy** is an error in reasoning that results in an invalid argument
- Three common fallacies:
	1. Using **ambiguous premises**, and treating them as if they were unambiguous
	   使用**含糊不清的前提**，但在推理过程中将它们当作明确无误的陈述。导致论证的结论站不住脚。
	2. **Circular reasoning** (assuming what is to be proved without having derived it from the premises)
	   **循环推理**指论证在推理过程中直接或间接地预设了要证明的结论。例如“我之所以正确，是因为我说的是对的”
	3. **Jumping to a conclusion** (without adequate grounds)
	   在论证的过程中**过于匆忙的得出结论**，而没有充分的理由或证据支持。
#### Converse Error
- Example:
  ![image.png](https://images.wu.engineer/images/2024/03/09/202403092217039.png)
![image.png](https://images.wu.engineer/images/2024/03/09/202403092218462.png)
#### A Valid Argument with a False Premise and a False Conclusion
- The argument below is **valid** by modus ponens. But its **major premise is false**, and so is its conclusion":
	- If Joseph Schooling is a Singaporean, then Joseph Schooling is a badminton player
	  *Premise*: Joseph Schooling is a Singaporean
	  *Conclusion*: Joseph Schooling is a badminton player
- 这个例子强调了评估论证(Argument)时必须同时考虑逻辑有效性和真实性。一个论证可能在逻辑上是正确的，但是如果其基于的信息是错误的，则其结论也无法反映实际情况的真相。
#### An *Invalid* Argument with True Premises and a True Conclusion
- The argument below is **invalid** by the converse error, but it has a **true conclusion**:
	- If Singapore is a garden city, then Singapore has lots of trees
	  *Premise*: Singapore has lots of trees
	  *Conclusion*: Singapore is a garden city
- 这段内容的问题是：错误的认为原始条件语句的**逆命题(Converse)** 也是有效的。逻辑上，原始条件语句的真实性并不能保证其逆命题的有效性。
#### Sound and Unsound Arguments
- An argument is called **sound** if, and only if, it is valid and all its premise are true
  An argument that is not sound is called **unsound**
- **有效论证(Valid Argument)**：如果所有前提都是真的，那么结论必须是真的。有效性关注的是论证的形式和逻辑结构，而**不涉及**前提的真实性。
- **真实论证(Sound Argument)**：一个真实的论证不仅是**有效的(Valid)**，同时其所有前提实际上都是*真的*。这意味着真实论证满足两个条件：逻辑结构是正确的（有效性），所有前提都是正确的（真实性）。
- **无效论证(Unsound Argument)**：任何不满足有效论证(Valid Argument)定义的论证都是无效的。这意味着即使所有前提都是真的，结论也不一定是真的。无效论证可能基于错误的逻辑结构(有效性)，或包含不真实的前提(真实性)，或两者都有。
### 2.3.6 - Contradiction and Valid Arguments
- The concept of logical contradiction can be used to make inferences through a technique of reasoning called the **contradiction rule**. Suppose `p` is some statement whose truth you wish to deduce.
- **Contradiction Rule**: If you can show that the supposition that statement `p` is false leads logically to a contradiction, then you can conclude that `p` is true
- 矛盾规则的基本思想是，如果我们假设某个命题“P”是假的，然后通过逻辑推理发现这个假设会导致一个逻辑矛盾（即导出了一个同时包含某个命题及其否定的情况），那么我们就可以得出结论，命题“P”实际上是真的。这是因为在逻辑系统中，矛盾是不被允许的，所以如果假设“P”是假的会导致矛盾，那么“P”不能是假的，只能是真的。
- The contradiction rule is the logical heart of the method of **proof by contradiction**
### 2.3.7 - Summary of Rules of Inference
![image.png](https://images.wu.engineer/images/2024/03/09/202403092238792.png)
![image.png](https://images.wu.engineer/images/2024/03/09/202403092238364.png)
# Chapter 3 - The Logic of Quantified Statements
## 3.1 - Predicates and Quantified Statements I
### 3.1.1 - Predicates 谓词
- In logic, **predicates (谓词)** can be obtained by removing some or all of the nouns from a statement. For instance, let P stands for “is a student at Bedford College” and let Q stand for “is student at”. Then both P and Q are **predicate symbols**
- **Predicate variables**:
  P(x) = “x is a student at Bedford College”
  Q(x, y) = “x is a student at y”
- When concrete values are substituted in place of *predicate variables*, a **statement** results.
  **谓词语句(Predicate statement)** 用来描述对象的属性或关系，通常包含变量，通过将变量替换成具体的值来判断语句的真假。
- A **predicate** is a sentence that contains a finite number of variables and becomes a statement when specific values are substituted for the variables.
  一个**谓词(predicate)** 是一个或多个变量的函数，其返回值是真值（通常是真或假）。当谓词中的所有变量都被具体的值替代时，谓词成为一个谓词语句。这是它可以被评估真或假。
- The **domain** of a predicate variable is the set of all values that may be substituted in place of the variable.
  **谓词变量的域(domain of a predicate variable)** 是指可以合法代入变量的所有可能值的集合。例如，如果我们有一个谓词”x是一个正整数“，那么谓词变量x的域就是所有正整数的集合。
- When an element in the domain of the variable of a *one-variable* predicate is substituted for the variable, the resulting *statement* is either true or false. The set of all such elements that make the predicate true is called the **truth set** of the predicate.
- If P(x) is a predicate and x has domain D, the **truth set** is the set of all elements of D that make P(x) *true* when they are substituted for x
### 3.1.2 - The Universal Quantifier: $\forall$ 全称量词
- One sure way to change predicates into statements is to assign *specific* values to all their variables.
	- For example: *If x represents the number 35, the sentence “x is divisible by 5” is a true statement*

- Another way to obtain statements from predicates is to add **quantifiers**
- **Quantifier(量词)**: words that refer to quantities such as “some” or “all” (个，辆，匹，只) and tell how many elements a given predicate is true
- The symbol $\forall$ denotes “for all” (or “for any”, “for every”, “for each”) and is called the **universal quantifier**
  **全称量词(Universal Quantifier)**：表达”对所有“的断言。当我们使用全称量词对某个命题进行量化时，我们是在说这个命题对于某个范围内的所有对象都是真的。

- Let Q(x) be a predicate and D the domain of x. A **universal statement** is a statement of the form “$\forall x \in D,\ Q(x)$”
  **全称陈述(Universal Statement)**：对于D域中的所有x，命题Q(x)都成立。
	- It is defined to be true if Q(x) is **true for every** x in D
	  全称陈述被定义为真，当且仅当在定义域D中的每一个元素x对于谓词Q(x)都是真的
	- It is defined to be false if Q(x) is **false for at least one** x in D
	  全称陈述被定义为假，当定义域D中至少存在一个元素x，使得Q(x)是假的
		- A value for x for which Q(x) is false is called a **counterexample**
		  这被称为**反例(counterexample)**
#### Method of exhaustion 穷竭法
![image.png](https://images.wu.engineer/images/2024/03/09/202403092356362.png)
![image.png](https://images.wu.engineer/images/2024/03/09/202403092356597.png)
### 3.1.3 - The Existential Quantifier: $\exists$ 存在量词
- Example: “There is a student in IT5005” can be written as:
  *$\exists$ a person p such that p is a student in IT5005*
  Or, more formally
  *$\exists \ p \in P$ such that p is a student in IT5005*
  Where P is the set of all people
- The words *such that* are inserted just before the predicate. If the context is clear, sometimes the abbreviation s.t. is used
- Sentences that are quantified existentially are defined as statements by giving them the truth values specified in the following definition:
- **Existential Statement**: Let Q(x) be a predicate and D the domain of x. An **existential statement** is a statement of the form “$\exists x \in D$ such that Q(x)”
  **存在量词(Existential Quantifier)**: 使用存在量词对某个谓词进行量化时，我们是在说，在考虑的域（集合）中，至少存在一个元素使得该谓词为真。
	- It is defined to be true if Q(x) is **true for at least one** x in D
	- It is defined to be false if Q(x) is **false for all** x in D
#### Symbol $\exists !$
- The symbol $\exists !$ is used to denote “there exists a unique” or “there is one and only one”
  此符号表示**存在唯一**，指的是存在着有且仅有一个元素满足指定的条件或属性。
### 3.1.4 Skolemization
- When a “$\exists$” exists outside of a universal $\forall$ quantifier, we can replace the variable with a new constant, known as a “Skolem constant”
- For example:
	- $\exists x\ Female(x)$
	  Can be re-written as $Female(c)$
	- Where c refers to one particular person in the universe of discourse
### 3.1.5 - Universal Conditional Statements
A reasonable argument can be made that the most important form of statement in mathematics is the **universal conditional statement**:
![image.png](https://images.wu.engineer/images/2024/03/09/202403100047837.png)
![image.png](https://images.wu.engineer/images/2024/03/09/202403100047698.png)
![image.png](https://images.wu.engineer/images/2024/03/09/202403100048939.png)
- Similarly, statement “$\exists$ x such that P(x) and Q(x)” can be narrowed to: “$\exists\ x \in D$ such that Q(x)”
## 3.2 - Predicates and Quantified Statements II
### 3.2.1 - Negations of Quantified Statements
- **Negation of a Universal Statement**: The *negation* of a statement of the form $\forall x \in D,P(x)$, is logically equivalent to the statement of the form $\exists x \in D \text{ such that }$~$P(x)$.
- That is, the negation of a universal statement (“all are”) is logically equivalent to an existential statement (“some are not” or “there is at least one that is not”)
- **量化语句的否定(Negation of quantified statement)**：对包含全称量词($\forall$)或存在量词($\exists$)的语句进行否定。
- **全称量词的否定**：一个全称量词语句的形式是“对所有x，P(x)都成立”。要否定这个语句，意味着“存在至少一个x使得P(x)不成立”。因此，全称量词的否定转换为存在量词的形式：
  原始语句：∀x, P(x)
  否定之后：∃x, ¬P(x)
- 存在量词的否定：一个存在量词语句的形式是“存在至少一个x使得P(x)成立”。要否定这个语句，意味着“对所有x，P(x)都不成立”。因此，存在量词的否定转换为全称量词的形式：
  原始语句：∃x, P(x)
  否定之后：∀x, ¬P(x)
### 3.2.2 - Negations of Universal Conditional Statements
![image.png](https://images.wu.engineer/images/2024/03/10/202403101403008.png)
![image.png](https://images.wu.engineer/images/2024/03/10/202403101403947.png)
### 3.2.3 - The relation among $\forall,\exists,\land,\lor$
- Analogous to De Morgan’s Law, which state that the negation of an *and* statement is an *or* statement and that the negation of an *or* statement is an *and* statement
- This similarity is not accidental. In a sense, universal statements are generalizations of *and* statements, and existential statements are generalizations of *or* statements
![image.png](https://images.wu.engineer/images/2024/03/10/202403101406753.png)
### 3.2.5 - Variants of Universal Conditional Statements
![image.png](https://images.wu.engineer/images/2024/03/10/202403101408280.png)
![image.png](https://images.wu.engineer/images/2024/03/10/202403101408095.png)
- The universal conditional statement is: 
	- **equivalent** to its contrapositive (逆否命题)
	- **not logically equivalent** to its converse (转置命题)
	- **not logically equivalent** to its inverse (逆命题)
### 3.2.6 - Necessary and Sufficient Conditions, Only if
#### 充分条件（Sufficient Condition）
在语句“如果P(x)，那么Q(x)”中，P(x)是Q(x)的充分条件。这意味着P(x)的真实性足以保证Q(x)的真实性。换句话说，每当P(x)发生时，Q(x)必然发生。但请注意，Q(x)的真实性不一定依赖于P(x)；Q(x)也可能因为其他原因而为真。
#### 必要条件（Necessary Condition）
在同一个语句中，Q(x)是P(x)的必要条件。这意味着Q(x)的真实性是P(x)真实性的必要条件。如果Q(x)不为真，那么P(x)也不可能为真。但Q(x)的真实性并不保证P(x)的真实性，因为即使Q(x)为真，P(x)也可能为假。
#### “Only If”的含义
“Only if”用于指出必要条件。当我们说“P(x) only if Q(x)”时，意思是Q(x)是P(x)成立的必要条件。用另一种方式表达，就是“如果P(x)，那么Q(x)”。这强调了无论何时P(x)为真，Q(x)也必须为真，但它并不意味着Q(x)为真就足以使P(x)为真。

总结来说：
- “如果P，那么Q”（P → Q）：P是Q的充分条件，Q是P的必要条件。
- “P only if Q”：强调了Q是P成立的必要条件，与P → Q逻辑上等价。
![image.png](https://images.wu.engineer/images/2024/03/10/202403101414417.png)
## 3.3 - Statements with Multiple Quantifiers
1. **∀x ∈ D, ∃y ∈ E such that P(x, y)**
    - 这个语句的意思是“对于D中的每一个x，存在至少一个E中的y，使得P(x, y)成立。”
    - 这里的关键在于，对于D中的每一个元素，我们都可以找到至少一个在E中的元素，使得某个条件P(x, y)成立。这个“存在”的y可能对于不同的x而不同。
2. **∃x ∈ D such that ∀y ∈ E, P(x, y)**
    - 这个语句的意思是“存在至少一个D中的x，对于E中的所有y，P(x, y)都成立。”
    - 这里的关键在于，我们能找到至少一个特定的x，在这种情况下，对于E中的每一个y，条件P(x, y)都是成立的。这意味着这个特定的x与E中所有的y都满足条件P。
### 3.3.2 - Translating from Informal to Formal Language
- Example: The reciprocal of a real number a is a real number b such that ab=1. The following statements are true. Rewrite them formally using quantifiers and variables.
	- Every nonzero real number has a reciprocal
	  *$\forall$ nonzero real numbers u, $\exists$ a real number v such that uv=1*
	- There is a real number with no reciprocal
	  *$\exists$ real number c such that $\forall$ real number d, cd != 1*
### 3.3.4 - Negations of Multiply-Quantified Statements
![image.png](https://images.wu.engineer/images/2024/03/10/202403101423658.png)
### 3.3.6 - Formal Logical Notation
![image.png](https://images.wu.engineer/images/2024/03/10/202403101424651.png)
## 3.4 - Arguments with Quantified Statements

# Chapter 4 - Inference Mechanisms
## 4.1 - Motivation
- This chapter we will look at how to **automate proofs**.
  **自动化证明(automate proofs)**：使用计算机程序来验证逻辑命题的正确性的过程。此方法依赖算法，目的是减少或消除人类在证明过程中的直接参与。
- Some techniques we will look at:
	- *Model Checking*: 模型检查是一种自动化验证技术，用于检查一个模型是否满足一定的规范或属性。它通过系统地探索模型的所有可能状态来验证属性是否总是成立
	- *Unification*: 统一化是逻辑推理中的一个过程，目的是找到变量的赋值，使得两个逻辑表达式匹配。
	- *Forward Chaining*: 正向推理是一种从*已知事实*出发，应用规则推导出新事实的方法。它是基于数据驱动的推理方法，从一组初始事实开始，逐步应用推理规则，直到达到目标或无法进一步推理为止。
	- *Backword Chaining*: 反向推理从目标（要证明的陈述）开始，逆向应用规则寻找支持该目标的事实或规则。它是目标驱动的推理方法，常用于问题求解和逻辑编程。
## 4.2 - Logical Entailment
- A model M is a set of true/false assignments to individual relevant statement
	- If a statement `s` is true in a model M, then we say that “M satisfies s” or “M is a model of s”, written as $M(s)$
- We say that statement `a` *entails(蕴含)* statement `b`, if, in every model in which `a` is true, then `b` must be true. This is written as $a\models b$. Formally: $a\models b \iff M(a) \subseteq M(b)$
  **逻辑蕴涵(Logical Entailment)**：在一组命题（前提集合）的逻辑基础上必然导出另一个命题（结论）的关系。假设前提集合为`a`，结论为`b`，我们说`a`逻辑蕴含`b`，则如果在所有`a`为真的情形下，`b`也必定为真。
- Similarly, a knowledge base KB entails a statement `a` iff (if and only if) any model that makes KB true also makes `a` true:
  $KB \models b \iff M(KB) \subseteq M(b)$
  当我们说一个知识库逻辑蕴涵一个陈述B时，意味着如果知识库为真，则陈述B也必须为真。
- Entailment is similar to implication, but different:
	- Implication applies to statements:
		- $P\to Q$ means that if statement P is true, then statement Q is necessarily true
	- Entailment is *more general*; it can apply to groups of statements, each with their own true/false values.
	逻辑蕴涵比Condition Statement跟广泛。逻辑蕴涵可以适用于一组语句。
## 4.3 - Model Checking
- In model checking, we try all possible combinations of truth values for each variable, and see if `a` is true in all of these.
- Model Checking Steps: 假设要证明KB逻辑蕴涵`a`
	1. 写出KB和`a`的Truth Table
	2. 找到KB为真(1)的所有行(Crital Rows)，查看`a`是否为真
	3. 如果有KB为真但`a`为假的行，则证明KB不能逻辑蕴含`a`
	4. 反之，如果KB为真的所有行`a`都为真，则证明KB逻辑蕴涵`a`
## 4.4 - Resolution
- Resolution is a simple mechanical method for testing if $KB \models a$
	- Every “clause” in KB must be statements joined by disjunctions (i.e. OR)
	- All the statements in each clause are joined by conjunctions (i.e. AND)
	- This is known as **Conjunctive Normal Form (CNF)**. For example:
	  $(P\lor Q)\land (Q\lor R\lor S)$
	- **归结(Resolution)**: 是一种证明KB是否逻辑蕴涵某个命题`a`的方法。归结特别适用于合取范式(CNF)。合取范式由多个字句构成，每个字句中的运算符都为或($\lor$)，字句之间的链接都为与($\land$)
- To see if $KB \models a$:
	- Introduce $\sim a$ to the set of clauses
	- If there is a clause of the form $a\lor b$, then we have:
	  $a\lor b \land \sim a \equiv False \lor b \equiv b$
- **归结(Resolution)的工作原理**：
	1. *规范CNF*：在应用归结前，所有逻辑表达式必须转换成合取范式(CNF)。即命题a和KB都以合取范式的形式表示。
	2. *归结规则*：归结法基于一个简单的规则，即归结规则，它允许我们从两个包含互补文字的子句中推导出新的子句。如果一个子句包含某个文字 P，另一个子句包含该文字的否定 ¬P，那么通过归结可以得到一个新的子句，该子句包含这两个子句中的所有其他文字，但不包括 P 和 ¬P。
- If a series of resolution steps reduces a clause to an empty set:
	- This means that adding $\sim a$ to the knowledge base resulted in a contradiction
	- Thus $\sim a$ cannot be true, and $a$ must be true, i.e. $KB \models a$
## 4.5 - Conjunctive Normal Forms
- Recall that resolution requires:
	- Clauses to consist of statements joined by disjunctions (or $\lor$)
	- KB to consist of clauses joined by conjunctions
- Note that it is very intuitive that a KB should consist of a conjunction of clauses:
	- For the KB to be true, every one of its clauses must be true
	- This corresponds to the idea of “critical rows” in using truth tales to test the implications and entailments
![image.png](https://images.wu.engineer/images/2024/03/10/202403102223985.png)
## 4.6 - Definite and Horn Clauses
- Resolution allows us to work with clauses of any kind as long as it is expressed in CNF
- However, in practice we can restrict our clauses to just two kinds:
	- Definite clauses
	- Horn clauses
- With these restricted clauses we can employ less powerful but more efficient inference mechanisms
- A definite clause is a clause that has **exactly** one **positive** literal
  **确定性字句(definite clause)**：**恰好**包含一个*正文字*的字句。正文字指为被否定的变量，例如P。否定的文字，例如$\sim Q$，被视为负文字。
  For example:
	- $P\lor \sim Q \lor \sim R$ is a definite clause, because only P is positive
	- $P \ \lor \ Q \ \lor \ \sim R$ is not a definite clause, because it contains two positive literals P and Q
- A Horn clause is a clause that has **at most** one **positive** literal.
  **霍恩字句(Horn clause)**：包含**最多一个**正文字的字句。这意味着霍恩字句可以只有负文字，或者一个正文字加上任意数量的负文字。
  For example:
	- $P\lor \sim Q \lor \sim R$ is a Horn clause, because only P is positive
	- $\sim P \lor \sim Q \lor \sim R$ is also a Horn clause, since no literal is positive.
## 4.7 - Forward and Backward Chaining
- When a KB is written purely using Horn (or definite) clauses, we can apply forward or backward chaining to test whether or not in entails a sentence
### Forward Chaining
- Forward Chaining Algorithm:
	- Given the knowledge base KB consisting of Horn clauses, and query U:
		- When all the premises of an implication are true, add the consequent to the KB
		- Stop when either:
			- The query U is added to the KB, in which case $KB \models U$
			- We run out of Horn clauses, in which case $KB !\models U$
- 正向链接算法的工作原理：
	1. **初始化**：从已知的事实（知识库）开始。
	2. **规则匹配**：扫描所有的规则，找出其前提（如果部分）与当前已知事实匹配的规则。
	3. **规则应用**：对于匹配的规则，将其结论（那么部分）加入到已知事实中。这可能会引入一些新的事实。
	4. **重复过程**：重复步骤2和3，直到无法找到新的匹配规则，或者达到了特定的目标。
	5. **终止**：当没有更多的规则可以应用时，算法终止。此时，所有可以从初始事实集和规则集推导出的结论都已被推导出。
![image.png](https://images.wu.engineer/images/2024/03/10/202403102246516.png)
![image.png](https://images.wu.engineer/images/2024/03/10/202403102246832.png)
![image.png](https://images.wu.engineer/images/2024/03/10/202403102247064.png)
### Backward Chaining
- As shown earlier, Forward Chaining sometimes evaluates clauses that are irrelevant, in an attempt to find a clause that entails the query
- In Backward Chaining, we eliminate this by starting from the goal, and seeing if its premises can be satisfied.
	- If every term in the premise are true, then KB entails the goal
	- If the premise is false, then the KB may not entail the goal
	- Otherwise:
		- For each unknown term of the premise, set that term as a sub-goal and recursively find its truth value
![image.png](https://images.wu.engineer/images/2024/03/10/202403102253955.png)
## 4.8 - Extending to First Order Logic
- We have seen how inferencing can work with propositional logic. We now look to extend it to first order (predicate) logic
### 4.8.2 - Unification and Generalized Modus Ponens
- In previous chapter we saw how universal instantiation was combined with modus ponens to create generalized modus ponens
- Formally this is done through “**unification**”
  **统一unification**：**统一**用于确定是否可以通过变量替换使得两个或多个逻辑表达式在形式上相等。这种变量替换的集合称为**替换**（Substitution）θ。统一过程的目的是找到这样的替换θ，使得经过替换后，某些表达式在结构和内容上完全匹配
	- We can think of our KB as a series statements $p' _1 , p'_2,...,p'_n.p_{1} \land p_{2}\land ... \land p_{n}\to q$
	- In unification, we see a set of substitutions $\theta$ so that:
![image.png](https://images.wu.engineer/images/2024/03/10/202403102320636.png)
