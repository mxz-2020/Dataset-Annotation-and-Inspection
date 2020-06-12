# 审核人员审核指南
审核人员拿到实习生标注过的数据集之后，需要在每个数据集code文件夹下建立新的python3文件，命名为inspection.ipynb 不可以直接在别人的代码上改动！负责人不代表工作内容只有一个人干，如果一下子需要审核太多数据集，请及时求助其他组员，保证项目进行的的流畅性。
## 一审
负责人：张萌栩
派发步骤：
### 初筛
- 前一周周五下发下一周需要的筛选的数据集总表，周日晚九点完成填写。预计平均每人每次有15-25个需要分类的文章。
- 一审同学可通过浏览文章 title 和 abstract 确定文章是否符合相关主题，是否可以使用。
- 列表回收后负责人会检查文章分类和可用性，并根据数据集是否已经被标注筛选可以使用的文章。
- 对于可以使用的文章，请填写表格中需要填写的空白项目，包括：PMID, accessionNumber, topic, queue, featurePublication, isDiscarded, - discardedReason, others.
- 一审同学将对个人初筛的文章进行一审。在最终确定文章是否是用前，初筛不需要检查 cluster、tSNE、UMAP 等信息。

- 当前数据收集目录：scRNA-seq, snRNA-seq, CITE-seq, CAR-T, TCR-seq, BCR-seq.

##### 表格填写指南
- accessionNumber: 填写文章做tSNE、UMAP 或者基因热图使用的所有数据编号（一般就是所有作者自己产生的新数据，如果是用了别人的数据做了以上三种图，请一并填写，并在 others 列里备注哪个数据属于别人，e.g. GSE12345 from PMID:13579 for fig.1-a）。accessionNumber 用英文逗号隔开，中间没有空格。如果涉及网址，请粘贴网址。如果文章属于可使用文章，但没有数据号且未提供下载链接，则填写notAvailable；如果文章不属于可使用文章则 accessionNumber 填写“-”。填写示例：GSE12345,GSE67890,GSE13579 全为英文符号且中间没有空格。

- topic: 仅填写文章主题关键词即可，例如：cancer, liver, heart, aorta, eye, brain, neuroscience, immunology, cell atlas, etc. 
  - queue 1: cancer, immunology, organs (e.g. heart, lung, liver…), neuroscience, cell atlas, regeneration 等等，检测、治疗学相关，或者其他所有看起来有商业价值的东西. 
  - queue 2: differentiation (mammal), differentiation (non-mammal, 但是仅限于nature, cell, science上关于脊椎动物的研究), somatic, 等等其他不是很重要的东西。
  - queue 3: 作者自己产生了新数据的方法学研究。
  - queue 4-5: 其他各种不重要的东西，比如关于线虫的研究可以是 queue 5。
  - queue 6: methodology，方法学，且作者只用了别人的数据。
  - 另：每篇文章可以有多个topic，比如 (cancer, cancer immunology), (eye, neurosciences), 等等组合。

- queue: 参见 topic queue

- featurePublication: therapy, therapy resistance, testing or prediction 等等很有医学或药物研究、检测用处的相关文章，填写 TRUE or FALSE。

- isDiscarded: TRUE/FALSE

- discardedReason: 被discaded的文章填写此项。参考以下字段填写：not scRNA-seq, ATAC-seq only,… 一切数据不能使用的原因，可以是主题过差，比如研究了蟒蛇、酵母…。被保留的文章填写“-”。

- others: 如果某数据在未来公开则需填写此项，e.g. GSE12345 available on 2020.06.01。对于方法学的文章，如果作者只用了别人的数据，则把被使用的数据号填写在这里。方法学文章如果找不到accessionNumber则 others 空着。对于其他类型的文章，如果作者借鉴了别人用到数据，但是借鉴的数据并没有用于 tSNE、UMAP 或者基因热图，则不用填写。

- Literature alignment, 包括根据作者聚类进行的 part 划分，data/code availability or supplementary files 中附加数据的检查和每个 part 使用数据的整理 (相应 part 文件夹中应仅包含该 part 使用的数据)。

- 注意除了 data availability 和 supplementary files 以外，需要特别查看 code availability 里面有没有 GitHub 或者其他可能有数据的网站链接，里面有时会有诸如 cluster 信息、tSNE、UMAP 坐标等等的东西，请进行下载，并加入 downloaded data 文件夹。

- 对于可能有划分 part 问题的文章请联系负责人确认。一审结束后交由张萌栩下发标注，会有无规律一审质检。

- 聚类的意义：所有实验的最终目的是区分不同的细胞并找到它们之间的差异基因 (candidate drug targets marker genes)。tSNE 和 UMAP 的作用就是通过调节参数把不同类型的细胞分开，同类型细胞归为一组。每一类细胞有他们的特异基因，作者的 tSNE 和 UMAP 的好坏标志着细胞分类是否正确合理，同时展现了根据该聚类结果得到的 marker genes 的正确性。

### 一审内容：
1.	一审人员在确定每周要发包的数据集有哪些之后，需要给每个数据集分part，并保证每个数据集下面只有相应的part需要用的GEO数据信息，并写出一部分unstructuredData的内容在数据集文件夹下的descriptio.txt中。
2.	由实习生标注的时候把相应内容黏贴到数据集里，防止直接写到文简里被随意更改掉。
3.	记录到本地检查表格中，并把表格交给二审负责人，并把分好part的数据集，放入二审负责人用户下文件夹里

- Part 分类方法(在把数据集下发给实习生之前就已分好)：
  - 分part实际操作：和原作者一致即可，避免 part 划分人员的主观判断。
    - 1) 最主要根据文章中的聚类分析来进行分part，不管分了几次聚类分析，只要cluster和tSNE/UMAP等的相关信息齐全，就可以算是一个part。
    - 2） 如果信息不那么齐全 
        - 若是文中进行了2次独立的聚类分析，那么应该将数据拆分成2个part。
        - 但是，如果part2的聚类分析是对part1聚类中的某一簇细胞进行的再聚类，只算一个part。
        - 如果多次聚类，都是对同一组细胞的，那么只保留一次。
        - 例：如果一篇文章涉及 T cell 和 B cell，作者仅做了一次整体聚类，那么我们不需将 T cell 和 B cell 再聚类。如果作者后续单独对 T cell 的集合做了新的聚类，那么我们就新增细化的 T cell part。
    - 3） 如果实在不知道该不该分part，那就分就可以了。
    - 4) 划分 part 后，在数据集文件夹(../GSE*****/)下新建一个description.txt文档,写入每个part对应的 description，subDataset，和 correspondingFigure。

    - 保证part_1, part_2, part_3 文件中仅含该 part 所需 GSE 数据信息，如果需要 数据标注人员从同一个 GSE 中挑选该part 所用细胞时，一审人员需要在 description中添加描述。

- unstructuredData填写三项：
    
    - subDataset：如果有不只一个part，则根据part_n填为SubDataset-n。只有一个part就空着即可，不可以填。

    - description：填写对part，即subDataset的描述。只有一个part就空着即可，不可以填。格式：description: The original article contains ? subdatasets, based on e.g. species, cell type(s). This subdataset is based on e.g. Mouse, cell A, B and C.  (should match the initial description).

    - correspondingFigure：这里填写该数据对应的文章tSNE聚类图，格式为形如"1-a"，意思为figure1的图a，如果是附录里面的图，可以填写成“s1-a”的形式，ExtendedData里面发现的图可以填写成：”'extended2-a' 这种形式，没有对应的图填notAvailable。


4. 一审进行时需填写 description 文件，内容及格式如下：
- title:
- PMID:
- subDataset-n
- description:The original article contains N subDatasets, which are different by species/library preparation method/tissues/cells/protocols (放用于区分part的关键词). This subDataset is based on human/mouse data/xxx tissue/xxx cells/xxx method (填写part间的区别信息).
part_n 仅一个part省去 subDataset 和 description
- correspondingFigure:1-a
- tissue:

- clusterAvailability:
- tSNEAvailability:
- UMAPAvailability:

 以上三项如果是 TRUE 则需要在 downloaded data 里面有相应文件，可以自行下载后上传，或者使用 linux 命令 nohup wget xxxx(网址链接) > log.txt & 后台下载到 downloaded data 文件夹，生成的 log.txt 日志请检查是否显示 100% 下载完成，确认下载无误请删去 log.txt。如有下载问题请联系我们。非后台下载：cd 到 downloaded data 文件夹直接使用 wget xxxx(链接) 会自动显示下载百分比。

- genomeBuild:
- taxonomyID:
- libraryPreparationMethod:
- sequencingPlatform:

## 二审：
负责人：张萌栩 
#### 二审基本原则：检查数据集中每一项填写的内容是否有问题。

### 二审 修改回收步骤：
负责人分配任务，
- 1）	二审（可以找优秀的实习生帮忙了），首先把数据集标注的任务在redmine上asign给空闲的实习生，把数据集scp 到修改人的目录中(针对在node02服务器上审核的人)或者move到修改人的目录下面（针对在阿里云服务器上修改的人）

- 2）	之后等实习生做完标注并上传report在redmine上，就需要在report和数据集的基础上进行审核，如果有错误，记录在redmine上并在report中使用修订模式指出，然后返回实习生修改。除metadata的错误可由审查人员直接在原文件中自行改动之外，其余错误均需按照以下步骤！

- 3）	当修改人在redmine上反馈修改完成之后，审查人去该目录下进行二次检查。除了原有问题之外，需重点看以下几点：
    - 如果是矩阵需要改动，需检查其相应的自动生成函数是否都运行了（可根据文件更新时间进行判断），包括：tsne, cluster, auto_calculation, downsample（downsample这个只有回溯时会有）等；
    - metadata里面的research topic，clusterAvailability以及tSNEAvailability需进行二次核查，tissue，journal，libraryPreparationMethod需要确保格式正确

- 4）	如果没有错误，把report一起保存在数据集中，并回收数据集到：
针对在node02服务器上修改的人：将数据集打包压缩(如果数据集较小可不打包压缩，但还是建议先打包压缩)，并scp回来，拷贝到路径：/home/biodb/data/dataset_collection/datasets/2_inspection_stage/revised/；针对在阿里云服务器上修改的人：将数据集move到路径：/home/biodb/data/3rd_inspection/。在数据改完之后均需要放在以上这个路径中。

- 5）	确认数据集已拷贝至指定路径后，需要删除原来的修改人目录中的数据（不要留有冗余数据）。

- 6）	在redmine上更改任务情况的状态为Feedback,非紧急任务时需要在本地表格记录审核情况，每周五交给数据集流程管理人员进行汇总。错误记录只需简略提及要点即可，标注人、审核人（在二审表格中）一定要写清楚。

- 7）	最后由三审人员在指定3rd_inspection文件夹下做最后审查。小错误自己改改就好的，可以在直接改完后移动到correct文件夹下。做好本地表格记录即可！

- 8）	如果有优秀的实习生，并且其本人有意愿，可以让他们接触审核工作，帮忙分担工作压力，但是质量控制要把握好。

### 补充教程：
可以跟管理员要inspection_template.ipynb
1.	Unstructured Data 
在 inspection.ipynb 中参照 实习生数据标注指南 核验 unstructured data 中每一项是否有错误，需要看文献，并点开填写的各个网址查看，还需要确认markergene是否文章中给了却没有填写等待这些情况。如有错误，随时记录在redmine相应的任务下。

2.	Cell Annotation 和tSNE 检查
- 1）cellAnnotation
   -重点检查meta部分,包括是否是有效信息，有无缺漏，表头填写是否正确，是否有错字等
   -注意检查cluster以及cellOntology部分，set（）出来查看一下
   -对于自动生成cluster信息的数据集，需要检查所有途径是否真的没有提供此信息，包括检查CodeAvailability里面是否有github链接提供此代码等。
   -还要注意检查细胞数量是否与矩阵和文章中一致

- 2）使用代码，调用计算脚本画出tSNE/UMAP的图,或者可以直接使用my_builder.tSNEplot()和my_builder.UMPAplot()来画图，但是图比较小不太好观察

    import seaborn as sns
    import matplotlib.pyplot as plt #下一行开始需要在两个不同的block里运行
    clusterName = df_cell['clusterName'].tolist()
    tsne1 = df_cell['tSNE1'].tolist()
    tsne2 = df_cell['tSNE2'].tolist()
    plt.figure(figsize=(10,10))
    sns.scatterplot(x = tsne1, y = tsne2, hue = clusterName)
    
- 3）检查tSNE图质量，不同颜色的点不可过多重合，过多重合即为 isBadtSNE：True

- 4）使用代码画图查看某个基因在细胞中表达的情况 3.矩阵检查 中第四部分也有提到。
    
3.	矩阵检查（最重要的部分，需要着重检查）
- 1）	TPM 检查
   -读取 expressionMatrix_TPM.tsv 这个文件，检验各行基因的和相加是否为100 000。着重检查不是从rawdata来的矩阵，其转换成TPM的算法是否正确。
   -检查normalizationMethod书写是否规范，规范写法例如：TPM from FPKM; TPM from log2(TPM+1), ect。
   -检查cellID和cellAnnotation中的cellID是否完全一致，包括顺序和数量和字符。
   -检查gene和geneAnnotation.tsv中的是否一致，是否有重复的gene？注意当genes在矩阵中作者给的为ensemblID时，转换成geneSymbol
- 2）	rawCounts矩阵检查
   -读取expressionMatrix_rawCounts.tsv 文件，看是否有把normalized矩阵和rawCounts矩阵弄混。
   -还需要去源代码script.ipynb 中检查是否有矩阵拼接上的错误。cellAnnotation中的细胞数量（即，有多少行）应该和矩阵里的细胞数量都是一样的。
   -其他cellID和gene的检查要注意的事情跟TPM一样
- 3）	Normalized矩阵检查
   -读取expressionMatrix_normalized.tsv 文件， 看是否有把normalized矩阵和rawCounts矩阵弄混。
   -cellAnnotation中的细胞数量（即有多少行）应该和矩阵里的细胞数量都是一样的。
   -其他cellID和gene的检查要注意的事情跟TPM一样
- 4）	如何检查矩阵的正确性？ 
分为两个层面：
   - 第一看作者提供的原始数据，（downloaded data里）看看实习生在拼接过程中是否有出错。
   - 第二，找到文章里的marker gene然后画一下图，如果跟文章的图差不多，就问题不大了。
     - 只有clusterAvailability为True的数据集需要保存genesPlot.pdf
     - 基因的选取，当文章中有画gene在tsne上的表达图时，复现出与原文献相同的gene在细胞上的表达；当文章没有画marker gene 的表达图时也不需要画图。
     - 调用函数把所有图合并成一个名为genesPlot.png的形式存储在processed_data/文件夹下
     - pipeline中有函数可以直接调用


## 三审
负责人：陈淳、天然（暂定）
## 只有三审人员可以在redmine上进行任务的关闭，即把任务状态更改为closed。
### 三审 修改回收步骤：

- 1）	再进行一次二审的操作，不过可以大体浏览。发现错误后在renmine上记录，同时返回实习生修改。(请注意记录二审的漏检率，用作汇报时证明三道审核制度下的优势)

- 2）	完全没有错误了之后，需要把README.json中的notPassed改为passed,并保存。

- 3）	在redmine网站上close相应的任务。

- 4）	在本地表格记录自己的审核情况（包括漏检率的记录），每周五交给数据集流程管理人员进行汇总。标注人、审核人（在三审表格中）一定要写清楚。

- 5）	最后，把更改好的数据集转移到node01服务器上。

### 审核的汇总表格流程
周期：每周更新一次数据集回收情况
流程
1. 每月生成一张新的dataset_inspection.xlsx表格记录整个月的数据集标注情况，
2．每周五下发数据集时，由一审负责人更新excel表格中数据集编号和title信息。
3. 收包时由二审负责人更新完成的信息到excel表格中，包括三道审查中改出的错误用“×”记录，还要填写标注人员的信息，每周五收集各个二审和三审人员的本地记录表格，完成汇总后每周并上传至Github，共享给组员。
4. 除此之外，管理员需每周回收数据集的时候查看各个实习生完成的数据集数量，若是超过两个周的时间中完成不超过两个数据集，需要沟通了解情况。
下发数据及之后长时间不做怎么办？
在每周回收数据集时，会发现是否有本周下发的数据集没能close，这时需要审核没做完的数据集是因为什么原因。
- 1）	数据集过于复杂（可以适当延长回收日期）
- 2）	实习生没有做，并且没有及时通知（需询问是何原因，是否还有意愿继续做数据集？）如果没办法完成数据集，及时换人。
