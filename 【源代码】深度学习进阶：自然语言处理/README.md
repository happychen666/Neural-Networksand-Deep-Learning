深度学习进阶：自然语言处理（Deep Learning from Scratch ❷）
==========================





## 文件结构

|文件夹名   |说明                         |
|:--        |:--                          |
|ch01       |第1章使用的源代码            |
|ch02       |第2章使用的源代码            |
|...        |...                          |
|ch08       |第8章使用的源代码            |
|common     |共同使用的源代码             |
|dataset    |数据集用的源代码             | 

训练完的权重文件（第6~7章使用）可从以下URL获取。
<https://www.oreilly.co.jp/pub/9784873118369/BetterRnnlm.pkl>

源代码的解释请参考本书。


## Python和外部库
执行源代码需要安装以下软件。

* Python 3.x
* NumPy
* Matplotlib
 
另外，作为可选项，使用以下库。

* SciPy（可选）
* CuPy（可选）

## 执行方法

移动到各章的文件夹，执行Python命令。

```
$ cd ch01
$ python train.py

$ cd ../ch05
$ python train_custom_loop.py
```

## 使用许可

本源代码使用[MIT许可协议](http://www.opensource.org/licenses/MIT)。
无论是否为商业行为，均可自由使用。

## 勘误表

本书的勘误信息在以下网址中公开。读者可以在以下网址中查看和提交勘误。

https://www.ituring.com.cn/book/2678


当前阶段主要是在与同事进行产品需求沟通，因此主要集中在需求分析和需求澄清阶段，需求未定清楚前，开发无法快速产生代码,这种情况属于项目的正常开发阶段。需求开发需要与其他同事进行协调沟通，在本人已经被针对且办公条件被限制的情况下，本人仍然在积极准备开发工作，也在积极主动推进整体需求开发流程，同时团队内部也有较多的非编程任务，代码审查和前期调试自测工作，这些工作都无法从代码量角度进行度量，但对产品的质量和长期效能有非常重要的作用，虽然没有新增代码量，但目前有对现有代码进行优化和质量为稳工作，提升系统的长期可维护性和性能。
