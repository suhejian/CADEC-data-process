# CADEC-data-process
对CADEC数据进行处理

原项目地址：https://github.com/daixiangau/acl2020-transition-discontinuous-ner
本项目仅添加注释用于个人学习
## 数据集介绍
`CADEC`数据集，全称`CSIRO Adverse Drug Event Corpus`，是关于患者报告的药物不良事件（`ADE`）的丰富注释语料库。</br>
根据原项目提供的数据下载地址，其中有两个版本，Xiang Dai选用`CADEC.v2.zip`数据集，同时只关注`ADR`实体类型，因为只有该类型有非连续实体。</br>
该数据目录下一共有四个子目录，其中只需要用到`text`和`original`两个子目录：
- `text`：原文
- `original`：标注

## 运行流程
把下载的数据集放在当前目录下，名称改为`cadec_dataset`。
1. `python .\extract_annotations.py --type_of_interest ADR`</br>
一共提取出6318个实体，每一行的数据：`document_name`, `entity type`, `start_index, end_index`, `mention`
2. `python .\tokenization.py`</br>
对文本做`tokenization`，生成的数据的每一行：`token`, `document_name`, `start index`, `end index`
3. `python .\convert_ann_using_token_idx.py`</br>
将字符级的索引转换为`token`级别的索引，生产的数据的每一行：`document name`, `entity type`, `start_index, end_index`, `mention`
4. `python .\convert_text_inline.py`</br>
每一个样例的格式：`document_name`, `sentence`, `entity type | entity indexes`
5. `python .\split_train_test.py`</br>
根据`split`文件夹中提供的`train.id`, `dev.id`和`test.id`划分训练集，验证集和测试集，所谓的`id`是文档的名称