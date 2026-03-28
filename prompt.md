# 请调用 skill-creator 创建一个 架构师 的 AI Agent SKILL ,这个Skill 里面包含了 架构师 不同skills,
1, 而且这个架构师具备skill是写在配置文件里面的, 
2, 这个架构师能完成的任务是可以配置的
3, 架构师 完成任务 通过不同 skill 去完成,并且任务使用的架构师skill 也是可以配置的的, 一个任务可以使用多个 skill, 使用skills 的顺序也是可以配置的,而且支持并行出发多个skills.

不要立即创建 skill, 我们确认好后在创建


#
你首先按照1，2，3 要求把skill 搭建起来。


❯ 现在我们有两个任务：任务一：根据我们聊的内容，以 @docs/superpowers/specs/2026-03-16-code-design-analysis-design.md                   编写一个这个system-design 对应的文档，方便 skill-creator根据这个文档生成新的skill。 第二个任务：根据我们聊 ，调用 skill-creator生成一个 同步一步一步聊天创建出一个skill 思路的。然后根据这些思路 以                                             @docs/superpowers/specs/2026-03-16-code-design-analysis-design.md  文档为模版，使用skill-creator来生成skill 





#
我先在想创建一个架构师 Ai Agent Skill , 这个 Ai Agent Skill 是根据客户指定topic和 现有项目代码路径， 去调查如果实现这个 topic 的技术解决方案。
第一步，
你根据这个项目的代码路径，读取这个项目代码、文档或者你认为有价值的东西。

我要编写一个 prompt，这个prompt 是调用 skill creator,来创建一个 AI Agent Skill， 完成这个任务。 这个 ai agent skill 的要求：



第一，根据客户的需求和当前任务目标，你生产一个问题清单为了挖掘客户真实需求，并引导客户行业内标准应该怎么做，这个任务清单是可以配置的，稍后你会根据这个问题清单来跟客户交互，获取用户真实的诉求；并将客户回答问题记录系来，为后续的任务提供参考。