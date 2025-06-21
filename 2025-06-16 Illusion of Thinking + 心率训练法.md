![](https://hits.sh/liufinback.github.io/2025-06-16 Illusion of Thinking + 心率训练法.md.svg)

1. 苹果实习生[Parshin Shojaee](https://parshinsh.github.io/)发的论文[The Illusion of Thinking](https://machinelearning.apple.com/research/illusion-of-thinking) 否定了模型推理Scaling的能力，激起了热烈的讨论。论文的基本思路是Large Reasoning Models相比于Large Language Model，增加了回答前的推理过程，提高了模型回答的准确度。
    但目前对模型能力的评价以数学和编程能力为主，难以避免数据污染问题，并且没有评价回答前推理过程的质量。这篇论文通过可控难度的题目：汉诺塔、Checkers Jumping、River Crossing和Blocks World四个题目测试了LRM与LLM的能力。结论是低难度题目LRM不如LLM，中等难度题目LRM优于LLM，高难度题目（汉诺塔中大于8个disc）LRM和LLM都会失败崩溃。所以最终的结论是大于一定难度后LRM和LLM都会崩溃，所以不能Scaling。
    [The Illusion of the Illusion of Thinking A Comment on Shojaee et al. (2025)](https://arxiv.org/html/2506.09250v1)提出了严厉的批评，说Illusion of Thinking主要限制在模型的输出token的数量，如果让模型输出可以解决汉诺塔问题的Lua代码，模型可以轻松的输出代码结果。**所以作者设计的试验不能区分推理和打字（The question isn’t whether LRMs can reason, but whether our evaluations can distinguish reasoning from typing.）**。

2. 翻了翻[心率训练法](https://book.douban.com/subject/26849847/)，其中提到的关键的三点：
    1）监测静息心率（每天清晨起床后立即测得的心率），静息心率会随着体能的改善而降低，也会随着疲惫等状态升高；
    2）计算最大心率：慢跑800到1600米热身，然后以最快速度在400到600米的跑道上冲刺，然后立即查看心率。走或者慢跑2分钟恢复，然后再冲刺一次。再用2分钟恢复，然后冲刺第三次，这次结束时的心率便是最准的最大心率。
    3）使用法克莱跑，通过变换速度把心率控制在60%到75%之间来提升体能。60%心率的计算方法是（最大心率 - 静息心率）x 60% + 静息心率。先热身，然后持续运动让心率上升到75%的上限，当达到心率上限时就减速让心率降低到60%下限。通过这样的循环训练，数周的训练后耐力就会得到很大的提升。