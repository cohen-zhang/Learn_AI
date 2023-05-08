# 新

## 工具

PromptFlow 是一款工具，可以让您创建可执行的流程图，将 LLM、Prompts、Python 函数和条件逻辑链接在一起。使用视觉方式创建复杂的工作流程，而不必编写太多代码或处理复杂的逻辑。

该工具提供了一个可视化界面，可以轻松创建复杂的 LLM Prompt 流程图。它还支持将多个流程图组合在一起，以创建更大的工作流程，并自动处理流程中的错误和异常情况。此外，PromptFlow 还支持将工作流程导出为 Python 代码，以供进一步修改和使用。

如果您正在寻找一款能够简化工作流程设计的工具，那么 PromptFlow 绝对值得一试。您可以在官网 https://www.promptflow.org 上了解更多信息。

## 教育

给朋友家的孩子创建了一个 7x24 小时在线的「英语学习教练」AI，得到的反馈是比私教老师讲得要好 😅

https://app.copilothub.ai/chat?id=4364

## 吴恩达老师学Prompt Engineering课

猜测不少人跟我一样，曾信誓旦旦，计划五一跟吴恩达老师学Prompt Engineering课，实际假期都在吃喝玩乐。

直到今天才开始学，课程地址：https://learn.deeplearning.ai/chatgpt-prompt-eng/lesson/1/introduction

学习笔记如下：

一、善用分隔符
以前我的Prompt写法，帮我做 xxxx ，加上“：”号，后面跟待处理的文本。例：帮我翻译成中文：hello world。

课程中常用的文本分隔符是前后三个反引号 ```（键盘数字1左边的按键，用英文标点）

除了反引号，也可以用三个引号（"""）、三个中横线（---）、尖括号（<>）、XML标签等成对包裹。

好处是让ChatGPT清晰的区分任务和待处理文本，防Prompt注入等。

二、指定格式输出
课程举的例子是指定用JSON和XML输出。
结构化好处：更容易校验格式，方便被编程语言调用处理。

其实也可以给例子，自定义输出结构。

参考 One/Few-shot Prompt用法。
https://learnprompting.org/zh-Hans/docs/basics/few_shot

三、任务序列化
Prompt 可指定多项任务，例如深度学习一个单词，多任务例子：

Task1：给出单词释义、发音
Task2：词根词缀来源
Task3：生成场景例句
Task4：用单词生成故事

然后再引用这些任务结果 ...，排版成自己想要的输出格式。

四、持续迭代
Prompt需要持续迭代：清晰具体的Prompt -> 结果和预期对比 -> 分析完善Prompt/增加示例 -> 重复前面流程

经验分享：
① 3.5 结果不稳定，不要求发挥创造性的场景，可调低Temperture值。

② 让ChatGPT找到相关信息，再引用这些信息回答减少幻觉（Hallucination）

五、常用场景

总结摘要：
根据自己需求限定单词数、句子数、字符数。（use at most 50 words/3 sentences/280 characters）

最好指定话题或关键词总结，否则总结很泛，没重点。

推测：

① 用Prompt轻松实现情绪识别（What is the sentiment of the following xxx）

② 识别指定Item（Identify the following items from the text）

转换：
语言转换：各种语言之间的互翻任务
口气转换：描述具体应用场景，给出语调转换（商务/个人等等）
格式转换：JSON、CSV、HTML等等

扩展：
除了写大纲等概要的东西，从0让ChatGPT生成的内容价值往往没那么高。

要点感觉还是定义角色、描述场景任务等常见技巧。

写在后面

吴恩达老师这套课程挺用心，最棒的有在线Jupyter notebook可运行代码（对不少人帮助更大）

但从内容丰富度和学习效率角度看，还是推荐以下资源

① 开源多语言Prompt学习课程
https://learnprompting.org/zh-Hans/docs/

②  
@thinkingjimmy
 提供的课程

https://learningprompt.wiki/docs/chatgpt-learning-path

另外，推荐
@huangyun_122
 黄赟写的吴恩达课程笔记，更全面详细：
https://twitter.com/huangyun_122/s