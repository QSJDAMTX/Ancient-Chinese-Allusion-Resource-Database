[English Version](#english-version) | [中文版](#中文版-readme)


### 中文版 README

# 古汉语典故资源库

本项目旨在提供**古汉语典故资源库**，以支持计算机自动分析古籍文本中的用典现象，并为人文学科研究及语文教育提供助力。项目基于典故辞书构建了以下两大核心资源：  
1. **典故知识库**：收录了2.3万个典形，结构化存储了典故的源流关系、释义及例句。  
2. **典故标注语料库**：包含3万余条标注数据，包括所用典故、典形位置及语料出处等详细信息。  

此外，项目设计了两项任务：  
- **用典判断**：检测文本中是否使用了典故。  
- **典故识别**：自动识别文本中使用的具体典故及典形。  

基于上述资源，项目提供了机器学习模型、神经网络模型及大语言模型的评测基线，旨在探测当前模型在典故自动识别中的表现。资源库还广泛适用于大语言模型评测、汉语学习及古典文学研究等领域。  

---

## 数据集目录

### 1. 典故知识库
**数据结构**  
该知识库以典故为核心，组织了典故及其不同衍生释义与典形词的层级结构，便于分析用典背后的语义关系。部分典形词后会加数字，这是为了区分同形不同义的情况。使用时可根据需求自行处理。
  

数据结构示例如下：  
```python
{
  "典源词": "阿戎",
  "典源内容": "南朝宋刘义庆《世说新语·雅量》：“王戎七岁，尝与诸小儿游。看道边李树多子折枝。诸儿竞走取之，唯戎不动。人问之，答曰：‘树在道边而多子，此必苦李。’取之信然。”",
  "衍生列表": [
    {
      "典形词": "阿戎1",
      "释义": "后因以阿戎美称他人之子。",
      "同源列表": [
        {
          "典形词": "阿戎",
          "例句": [
            "唐王维《送李员外贤郎》诗：“借问阿戎父，知为童子郎。”"
          ]
        }
      ]
    }
  ]
}

```

- **典源词** (str)：典故的名称。  
- **典源内容** (str)：典故的来源与出处。  
- **衍生列表** (list)：该典故的衍生释义及对应的典形词。  
  - **典形词** (str)：衍生词汇的名称。  
  - **释义** (str)：该衍生意义的解释。  
  - **同源列表** (list)：包含具有相同释义的典形词及其示例句。  
    - **典形词** (str)：同释义典形词的名称。  
    - **例句** (list)：示例句子列表。  

---

### 2. 训练数据集
用于训练模型的两个数据文件：  
- **task1_human_core_pure.jsonl**：用于用典判断任务的训练集。  
- **task2_human_balance_pure.jsonl**：用于典故识别任务的训练集。  

---

### 3. 测试集
用于评估模型性能的两个测试集：  

1. **Task1_testset_3.0.jsonl**  
    - **任务类型**：用典判断（二分类任务）  
    - **数据量**：共 2562 条  
    - **字段说明**：  
      - **id** : 唯一标识符，用于标识每条数据。
      - **sentence** : 包含典故的句子，以简体中文表示。模型需判断该句子是否使用了典故，或者识别出句子中使用了哪些典故。
      - **source** : 该句子的来源出处，指明该句子属于哪个文本或书籍。

2. **Task2_testset_3.0.jsonl**  
    - **任务类型**：用典识别（多标签分类任务）  
    - **数据量**：共 1310 条  
    - **字段说明**：  
      - **id** : 唯一标识符，用于标识每条数据。
      - **sentence** : 包含典故的句子，以简体中文表示。模型需判断该句子是否使用了典故，或者识别出句子中使用了哪些典故。
      - **source** : 该句子的来源出处，指明该句子属于哪个文本或书籍。 

如果您希望获取模型在典故识别任务中的表现，请将模型对测试集的预测结果提交至 [mokaijie@mail.bnu.edu.cn](mailto:mokaijie@mail.bnu.edu.cn)。

---

## 引用
如果您在研究中使用了本数据集，请引用以下论文：
```
@article{Kaijie2024,
  title={古汉语典故资源库的构建及应用研究},
  author={莫凯洁，丘子靓，王予沛，胡韧奋},
  journal={中文信息学报},
  year={2024}
}
```

---

## 许可证
本项目的数据集使用 [MIT License](https://opensource.org/licenses/MIT)。

---


## English Version

# Ancient Chinese Allusion Dataset

This project provides an **Ancient Chinese Allusion Resource Library** to facilitate the automatic analysis of allusions in classical texts and to support research in humanities and language education. The project consists of the following two core resources:  
1. **Allusion Knowledge Base**: Contains 23,000 allusion forms with structured information on their origins, meanings, and examples.  
2. **Allusion Annotated Corpus**: Includes over 30,000 annotated cases, providing details such as used allusions, their positions, and sources of the sentences.  

Additionally, the project introduces two key tasks:  
- **Allusion Judgment**: Detecting whether a text contains allusions.  
- **Allusion Recognition**: Automatically identifying specific allusions and forms used in the text.  

Based on these resources, the project provides evaluation baselines using machine learning models, neural network models, and large language models, aiming to explore their performance in allusion recognition. This resource library is widely applicable to large language model evaluation, Chinese language learning, and classical literature studies.  

---

## Dataset Overview

### 1. Allusion Knowledge Base
**Structure**  
The knowledge base organizes Chinese allusions into a hierarchical structure, focusing on their meanings and derived forms to facilitate semantic analysis. Some allusion forms(典形词) are followed by numbers to distinguish different meanings of the same form. You can handle them according to your needs when using the data.

Example structure:  
```python
{
  "典源词": "阿戎",
  "典源内容": "南朝宋刘义庆《世说新语·雅量》：“王戎七岁，尝与诸小儿游。看道边李树多子折枝。诸儿竞走取之，唯戎不动。人问之，答曰：‘树在道边而多子，此必苦李。’取之信然。”",
  "衍生列表": [
    {
      "典形词": "阿戎1",
      "释义": "后因以阿戎美称他人之子。",
      "同源列表": [
        {
          "典形词": "阿戎",
          "例句": [
            "唐王维《送李员外贤郎》诗：“借问阿戎父，知为童子郎。”"
          ]
        }
      ]
    }
  ]
}
```

- **allusion_name** (str): The name of the allusion.  
- **source_content** (str): The origin or source of the allusion.  
- **derived_meanings** (list): A list of meanings derived from the allusion.  
  - **derived_term** (str): The name of the derived term.  
  - **definition** (str): The explanation of the derived meaning.  
  - **related_terms** (list): Related terms sharing the same meaning, along with example sentences.  
    - **term** (str): The name of the related term.  
    - **examples** (list): Example sentences using the term.  

---

### 2. Training Dataset
Two files are provided for training models:  
- **task1_human_core_pure.jsonl**: Training set for allusion classification (binary classification).  
- **task2_human_balance_pure.jsonl**: Training set for allusion recognition (multi-label classification).  

---

### 3. Test Sets
Two test sets are provided to evaluate model performance:  

1. **Task1_testset_3.0.jsonl**  
    - **Task**: Allusion classification (binary classification)  
    - **Data size**: 2,562 samples  
    - **Fields**:  
      - **id** (str): A unique identifier for each data entry.
      - **sentence** (str): The sentence containing the allusion, in Simplified Chinese. The model needs to determine whether the sentence uses an allusion, or identify which allusions are used.
      - **source** (str): The source of the sentence, indicating which text or book the sentence comes from.

2. **Task2_testset_3.0.jsonl**  
    - **Task**: Allusion recognition (multi-label classification)  
    - **Data size**: 1,310 samples  
    - **Fields**:  
      - **id** (str): A unique identifier for each data entry.
      - **sentence** (str): The sentence containing the allusion, in Simplified Chinese. The model needs to determine whether the sentence uses an allusion, or identify which allusions are used.
      - **source** (str): The source of the sentence, indicating which text or book the sentence comes from.

---


## Citation
If you use this dataset in your research, please cite the following paper:  
```
@article{Kaijie2024,
  title={Construction and Application of Ancient Chinese Allusion Resources},
  author={Kaijie Mo, Ziliang Qiu, Yupei Wang, Renfen Hu},
  journal={Journal of Chinese Information Processing},
  year={2024}
}
```

---

## License
This project dataset is licensed under the [MIT License](https://opensource.org/licenses/MIT).
