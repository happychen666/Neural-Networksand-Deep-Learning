要说明 **为什么没有缩放和偏移**（没有可学习的 \(\gamma\) 和 \(\beta\)）会导致模型的表达能力受限，我将通过对比两个场景来说明：一个场景没有缩放和偏移，另一个场景有缩放和偏移。

### 场景一：没有缩放和偏移

假设我们有一个神经网络要处理两个类别的数据，并且这两个类别的数据在输入时具有不同的分布。

- **类别1的输入数据**：\( h_1 = [50, 52, 54, 56] \)
- **类别2的输入数据**：\( h_2 = [2, 4, 6, 8] \)

这两个类别的数据具有不同的均值和方差。如果我们不使用任何缩放和平移，仅仅做了标准化操作，批量归一化后的数据将具有均值为0，方差为1的分布。

#### 步骤 1：对数据进行标准化

1. **对类别1数据进行标准化：**
   - 均值：
     \[
     \mathbb{E}[h_1] = \frac{50 + 52 + 54 + 56}{4} = 53
     \]
   - 方差：
     \[
     \text{Var}(h_1) = \frac{(50 - 53)^2 + (52 - 53)^2 + (54 - 53)^2 + (56 - 53)^2}{4} = \frac{9 + 1 + 1 + 9}{4} = 5
     \]
   - 标准化后的数据：
     \[
     \hat{h}_1 = \frac{h_1 - 53}{\sqrt{5}} = \left[\frac{50 - 53}{\sqrt{5}}, \frac{52 - 53}{\sqrt{5}}, \frac{54 - 53}{\sqrt{5}}, \frac{56 - 53}{\sqrt{5}}\right] \approx [-1.34, -0.45, 0.45, 1.34]
     \]

2. **对类别2数据进行标准化：**
   - 均值：
     \[
     \mathbb{E}[h_2] = \frac{2 + 4 + 6 + 8}{4} = 5
     \]
   - 方差：
     \[
     \text{Var}(h_2) = \frac{(2 - 5)^2 + (4 - 5)^2 + (6 - 5)^2 + (8 - 5)^2}{4} = \frac{9 + 1 + 1 + 9}{4} = 5
     \]
   - 标准化后的数据：
     \[
     \hat{h}_2 = \frac{h_2 - 5}{\sqrt{5}} = \left[\frac{2 - 5}{\sqrt{5}}, \frac{4 - 5}{\sqrt{5}}, \frac{6 - 5}{\sqrt{5}}, \frac{8 - 5}{\sqrt{5}}\right] \approx [-1.34, -0.45, 0.45, 1.34]
     \]

#### 结果

标准化后，**类别1和类别2的数据完全一致**，它们都在同一个区间 \( [-1.34, 1.34] \) 内。这就意味着在标准化后，这两组原本具有不同分布的数据现在完全重叠了，网络无法区分这两类数据，也就**丢失了模型的表达能力**。

### 场景二：引入缩放和偏移（\(\gamma\) 和 \(\beta\)）

现在我们对这两个类别的数据分别进行缩放和偏移，假设：

- 对类别1数据，设置 \( \gamma_1 = 5 \)， \( \beta_1 = 10 \)
- 对类别2数据，设置 \( \gamma_2 = 2 \)， \( \beta_2 = 3 \)

#### 步骤 2：对标准化后的数据进行缩放和平移

1. **对类别1数据进行缩放和平移：**
   \[
   h_{BN_1} = \gamma_1 \hat{h}_1 + \beta_1 = 5 \times [-1.34, -0.45, 0.45, 1.34] + 10 \approx [3.3, 7.75, 12.25, 16.7]
   \]

2. **对类别2数据进行缩放和平移：**
   \[
   h_{BN_2} = \gamma_2 \hat{h}_2 + \beta_2 = 2 \times [-1.34, -0.45, 0.45, 1.34] + 3 \approx [0.32, 2.1, 3.9, 5.68]
   \]

#### 结果

经过不同的缩放和平移，类别1的数据被映射到了 \( [3.3, 16.7] \) 的区间，而类别2的数据被映射到了 \( [0.32, 5.68] \) 的区间。这样一来，**两类数据重新具有了不同的分布**，网络就可以通过这些不同的分布进行分类或区分。

### 总结

- **没有缩放和平移时**：批量归一化将数据都压缩到了相同的标准正态分布，导致模型丢失了不同类别数据之间的差异，网络无法区分它们。
- **有缩放和平移时**：通过引入不同的 \(\gamma\) 和 \(\beta\) 参数，模型能够恢复原本的数据分布，允许网络继续区分不同类别的数据，保持模型的表达能力。

这个对比说明了缩放和平移对于批量归一化后的模型表达能力的重要性。
