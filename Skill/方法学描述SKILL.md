---
name: method-desc
description: 将生物信息学/组学分析方法整理为标准化的中文方法学描述。当用户提供一组方法名称、引用文献或混乱的方法描述文本，要求"整理格式"、"写方法学描述"、"格式化方法"、"储存描述格式"时触发此 skill。输出格式固定为 $method_name ($citation): 方法学描述，描述简洁、纯方法学、中文。
---

# 方法学描述格式化 Skill

## 输出格式

每条方法严格遵循以下模板，一行一条：

```
**$method_name** ($first_author et al., *$journal*, $year): [方法学描述]
```

## 方法学描述写作规则

1. **语言**：中文
2. **长度**：1-2 句话，不超过 60 字
3. **内容只包含**：
   - 方法的核心原理（它是怎么做的）
   - 适用场景或数据类型
4. **内容不包含**：
   - 优点 / 缺点 / 局限性
   - 与其他方法的比较
   - 最新进展或版本更新
   - 推荐/评价性语言（如"广泛引用"、"金标准"）
5. **引用格式**：
   - 有文献：`(First Author et al., *Journal abbreviation*, Year)`
   - 斜体期刊名
   - 无文献时：`(方法来源/软件官网)` 或省略括号

## 示例

输入（混乱文本）：
> ComBat（Johnson et al., Biostatistics, 2007）— 最广泛引用的批次校正方法，SVA（Leek & Storey, PLoS Genet, 2007），RUVSeq（Risso et al., Nat Biotechnol, 2014）— Remove Unwanted Variation

输出：

**ComBat** (Johnson et al., *Biostatistics*, 2007): 基于经验贝叶斯框架，将批次效应建模为加性和乘性因子，估计并移除跨样本的批次偏差。

**SVA** (Leek & Storey, *PLoS Genet*, 2007): 通过从数据中推断替代变量（surrogate variables）来捕捉包括批次在内的未知混杂因素，无需预先提供批次标签。

**RUVSeq** (Risso et al., *Nat Biotechnol*, 2014): 利用阴性对照基因或 spike-in 内标估计不必要的技术变异，并将其回归去除，适用于 RNA-seq 等测序数据。

---

## 处理流程

1. 从用户输入中**提取所有方法名称和引用**（忽略评价性描述）
2. 对每个方法按模板输出一条描述
3. 如某方法缺少引用，根据已知知识补充标准引用；若完全未知则省略引用
4. 按用户提供的原始顺序排列，不重新排序