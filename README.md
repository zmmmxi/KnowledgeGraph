# 瑶医特色诊疗知识图谱的构建研究
少数民族特色治疗是我国民族文化中一笔珍贵的财富，但至今为止，由于有些民族没有文字，加上人数较少，文化传承岌岌可危，极待保护。本研究通过构建少数民族常见病特色诊疗知识图谱来保护少数民族医疗传承，知识图谱技术可将瑶医特色诊疗知识以图谱的形式表现，使得知识能以更直观的方式呈现给大众，将知识之间的关系表达的更加清晰，不仅可以有效的显示民族医的特色，利于文化传承，也可以更方便地理解民族医相关知识。

## 使用说明

### 数据文件
数据来源于罗金裕先生于1987年广西民族出版社出版的图书《瑶医效方选编》。    
本研究将该数据分为药物诊疗和烧刺诊疗csv两个文件。

### 代码文件
该文件写了整个瑶医特色诊疗知识图谱的构建过程。

## 构建过程
### 1.数据来源
本研究数据来源于罗金裕先生于1987年广西民族出版社出版的图书《瑶医效方选编》。罗金裕先生多年到瑶族地区特别是金秀瑶族自治县进行调查采访收集效方419条。这些方均是当地威信较高的瑶族医师和瑶族民间医生或少数积极应用瑶族医生传授的方药而杂居的汉、壮民间医生共103名，多年常用且疗效较好的祖传秘方或验方。这些方按照瑶名、正名、当地汉别名、用法、疗效的次序说明，并按其主治病症分类。

### 2.数据标准化
数据标准化是将不同的数据转换为一致和通用格式的过程。它被认为是确保数据质量的关键部分。本文所用瑶族特色诊疗数据是非结构化数据，里面包含了大量的瑶名，在实际应用中存在着诸多的问题。在处理过程中是人工抽取整理录入得到的瑶医特色诊疗实体数据存入excel文件中，分别包括药物疗法和烧刺疗法两个实体文件。根据书写规范和诊疗标准将数据标准化，按照书中目录将数据整理成表格，保证节点数据一致性。

### 3.关系定义
知识图谱通过知识图形的可视化表示，它可以作为机器和人类之间的联系，数据的格式被构造得足以让人和机器理解其语义。知识可以在资源描述框架(RDF)下以<head,relation,tail>的形式表达为事实三要素，例如，<疗法,包含,专科>。它也可以表示为一个有向图，节点为实体，边为关系。实体关系遵循瑶医理论定义，其疗法-专科-病症-疾病-处方之间是具有相互关系的元素集合，而这种基本辨证关系刚好符合“有向图”的定义。

### 4.知识导入
Neo4j图形数据库被设计用来处理数据之间的关系和数据本身一样重要。它被认为是一个本机图形数据库，因为数据存储在一起，每个单独的实体如何与其他实体连接或相关。本文使用py2neo库将数据导入neo4j图数据库中。首先需要import py2neo库，使用Graph（地址，用户名，密码）连接数据库。  
1）节点导入  
节点是保存在知识图谱中的数据存储单元，向图中添加节点非常简单，通过Node对象来创建结点，同时也可以采用merge方法来创建节点，使用merge方法是程序会通过对laber和property进行匹配。  
2）关系导入  
与导入节点的方法类似，利用Relationship对象创建节点和节点之间的关系，Relationship`(*start_ node*, *type*, *end_ node*, ***properties*)关系语句中定义了开始节点，节点关系和结束节点的一个三元组。在创建关系时必须指定关系的类型，这个与创建节点时必须指定节点标签是相似的。  

