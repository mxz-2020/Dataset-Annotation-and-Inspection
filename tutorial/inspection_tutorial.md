## 目录
- [ 审核人员审核指南](#head1)
	- [ 初筛](#head2)
		- [ 初筛流程](#head3)
		- [ 初筛内容](#head4)
	- [ 1. 一审](#head5)
		- [ 一审流程](#head6)
		- [ 一审内容](#head7)
	- [ 2. 二审](#head8)
   		- [ 二审 修改回收步骤](#head9)
   		- [ 补充教程](#head10)
	- [ 3. 三审](#head11)
  
# <span id="head1">审核人员审核指南 </span>
审核人员拿到实习生标注过的数据集之后，需要在每个数据集code文件夹下建立新的python3文件，命名为inspection.ipynb 不可以直接在别人的代码上改动！负责人不代表工作内容只有一个人干，如果一下子需要审核太多数据集，请及时求助其他组员，保证项目进行的的流畅性。
## <span id="head2">初筛 </span>
负责人：龚辰
派发步骤：
### <span id="head3">初筛流程 </span>
- 每周一更新总表，周一筛选最新发表的文章，下载发放一审；
- 优先筛选新文章，完成后可根据情况筛选旧文章，周五可再次发放一审
### <span id="head4">初筛内容 </span>
- 通过浏览文章 title 和 abstract 确定文章是否符合相关主题，是否可以使用，并根据数据集是否已经被标注筛选新的下发文章。在最终确定文章是否是用前，初筛不需要检查 cluster、tSNE、UMAP 等信息。
- 当前数据收集目录：scRNA-seq, snRNA-seq, CITE-seq, TCR-seq (CAR-T), BCR-seq.
  - snRNA-seq 测神经细胞 (轴比较长，一般只测核) 或冷冻肿瘤细胞核内 RNA，scRNA-seq 测新鲜样本的所有 RNA (主要还是核里的); TCR、BCR 除了检测T/B细胞RNA,还测T/B细胞表面受体clonotypes; CITE-seq 测单个细胞 RNA 加细胞表面蛋白质的检测。

- 筛选列表步骤
  - 新文章根据列impact factor筛选10分以上或10分左右的文章
  - 新文章中主题较好的impact factor在五分以上的，也需要查看
  - 旧文章中可优先筛选origin较多的行以及impact factor10分以上的
  - 查看的文章都需要填写对应的表格中的内容，包括：PMID, accessionNumber, topic, queue, featurePublication, isDiscarded, discardedReason, others.

##### 表格填写指南
- accessionNumber: 填写文章做tSNE、UMAP 或者基因热图使用的所有数据编号（一般就是所有作者自己产生的新数据，如果是用了别人的数据做了以上三种图，请一并填写，并在 others 列里备注哪个数据属于别人，e.g. GSE12345 from PMID:13579 for fig.1-a）。如果作者使用别人的数据做参考，但并没有用旧数据做自己文章的新图则无需填写旧数据号。accessionNumber 用英文逗号隔开，中间没有空格。如果涉及网址，请粘贴网址。如果文章属于可使用文章，但没有数据号且未提供下载链接，请填写 request 并给作者发送邮件询问，如果作者两次不回邮件或者告知数据不公开或者需特别申请访问权限，则将 request 改写为 notAvailable (其余各选填项无需变更)；如果文章主题不符，不属于可使用文章则 accessionNumber 填写“-”。 填写示例：GSE12345,GSE67890,GSE13579 全为英文符号且中间没有空格。

- topic: 仅填写文章主题关键词即可，例如：cancer, liver, heart, aorta, eye, brain, neuroscience, immunology, cell atlas, cell landscape, etc. 根据文章主题给文章排序
  - 每篇文章可以有多个topic，比如 (cancer, cancer immunology), (eye, neuroscience), 等等组合。
- queue
  - queue 1: cancer, immunology, organs (e.g. heart, lung, liver…), neuroscience, cell atlas, regeneration 等等，检测、治疗学相关，或者其他所有看起来有商业价值的东西都是 queue 1. 
  - queue 2: somatic cells，differentiation (mammal), differentiation (non-mammal, 但是仅限于 nature, cell, science 上关于脊椎动物的研究。对于非 CNS 的 non-mammal 文章，脊椎动物去queue 4，无脊椎动物去 queue 5), 等等其他不是很重要的东西。 
  - queue 3: 作者自己产生了新数据的方法学研究（方法学主要包括测序方法的研究和数据分析算法的研究）。
  - queue 4-5: 其他各种不重要的东西，比如关于线虫的研究可以是 queue 5。
  - 另：每篇文章可以有多个topic，比如 (cancer, cancer immunology), (eye, neuroscience), 等等组合。

- 注：被discarded的文章queue不需要填写，只有可以处理的文章才需要填写queue和topic等

- featurePublication: cell atlas, cell landscape, therapy, therapy resistance, testing or prediction 等等很有医学或药物研究、检测用处的，很有参考性 (广泛测序的样本) 或很有商业价值相关文章，填写 TRUE/FALSE。

- isDiscarded: TRUE/FALSE，不处理的文章，包括：无自己的数据，fastq，数据未公开，无权限下载，review等。

- discardedReason: 填写数据不能使用的原因，如上. 

- others: 
  - 如果某数据现在未公开但是将在未来公开则需填写此项，e.g. GSE12345 available on 2020.06.01。
  - 不是文本格式或者mtx格式的数据，需要在此注明，如：rds等。
  - 文章如果没有权限打开，也需要注明在此。
  -  细胞数少于100个，也需注明
 
- 其他列
  - requester：指的是数据要求来源，2为研究院，其他要求可以填写具体的人或者主题等

- 注
  - 被discarded的文章只需填写discardedReason即可，其他列可不用填写，requester需要填写（如果有的话）
  - 筛选列表的时候，需要看一眼文件大小，表达文件小于5m的，需要查看细胞数，少于100的先不要发放安排，注明others里面即可（重要！！！）

## <span id="head5">一审 </span>
### <span id="head6">一审流程： </span>
1. 一审人员在确定每周要发包的数据集有哪些之后，需要给每个数据集分part，并保证每个数据集下面只有相应的part需要用的GEO数据信息，并写出一部分unstructuredData的内容在数据集文件夹下的descriptio.txt中。
2. 之后由标注实习生标注的时候把相应内容黏贴到数据集里，防止格式上的差异。
3. 一审负责人记录好每周一下发一审的数据集的pmid和GEO编号生成表格，并把表格交给二审负责人之后由二审负责人每周五调配下发标注任务。
4. 注意一审质量，会有无规律一审质检。

### <span id="head7">一审内容（description.txt的整理）： </span>
#### 1. 查看数据来源：
- 文献data availability or supplementary files 部分里附加数据的检查，还需注意查看文章附录的聚类图。所有附件或链接均需打开查看可用信息。
- 除了 data availability 和 supplementary files 以外，需要特别查看 code availability 里面有没有 GitHub 或者其他可能有数据的网站链接，里面有时会有诸如 cluster 信息、tSNE、UMAP 坐标等等的东西，请进行下载，并加入 downloaded data 文件夹。对于可能有划分 part 疑问的文章请联系管理员确认
- GEO网站数据经常有一系列GSE编号的数据集，注意查看不要漏掉。

#### 2. Part 划分方法：
- 最主要根据文章中的聚类分析来进行分part，不管分了几次聚类分析，只要cluster和tSNE/UMAP等的相关信息齐全且cell type 信息不重复，就可以算是一个part。
  - 注意区分作者给的图到底是同一个 tSNE 遮盖部分细胞后分别显示控制组和实验组，还是真正的分别聚类。(比如总聚类之后，作者把细胞又按照处理时间的不同，分成了2周的细胞，4周的细胞再聚类，其实细胞类型完全重复，不需要再把4周或2周的分part)。一般如果作者没有特别声明，且两个图中同类型细胞的位置相差无几，那么它们大概率是遮盖部分细胞显示，不需要分。(调参工作复杂漫长，一般在两个不同图的调参中很难保持各类型细胞的绝对位置。)

- 判断是否可以把某一个聚类图作为一个 part 的方法：
  - supplementary files 里面的 reclustering 的 tSNE、UMAP 图，如果没有给出 cluster name 和 marker genes，就不把它们单分成一个 part。比如有的作者为了让自己的数据看起来很丰富，他把一个大聚类里的 T cell 单挑出来 reclustering，又细分出了 cluster 1、cluster 2、cluster 3... 这种只有 cluster ID 的东西，同时又没有在附件里给 cluster 信息、图的坐标或者 marker genes，还看起来没什么价值，那么我们就不把这个再聚类作为一个独立的 part。也就是说，如果几个part来自于一个总的part，作者做了再聚类，作为一个附加的分析，但是又没给subcluster的话，就不要再拆开单独分出来part了。但是如果作者把来自很多 tissue 的 T cell 在附件里的再聚类，同时这篇文章又在研究免疫，那么即使少信息，也要作为一个 part。也就是说，附录里的图如果再聚类对文章主题有价值，就可以要，如果没什么价值，可以省去。但需要在 part description 里写明省去该部分 (聚类) 的原因，以免后续审查时对 part 划分产生歧义。

  - 不过请注意，文章正文部分的所有再聚类图且cell type信息不重复的即使少信息也算作一个新 part (除非因为没有 cluster 信息或其他原因无法挑选细胞或 sample，此类情况同样需要在 part description 中备注)。附件里的整体聚类图（整体聚类图，即对样本的聚类，而不是对某一类或几小类细胞的再聚类）即使少信息也可以算作一个part。

- 各 part 使用细胞的挑选：
各 part 使用细胞与文章保持一致，即 cell type 和 cell number 均要保持一致。如果存在我们下载的数据和作者回复 cluster、tSNE、UMAP 信息的邮件中的数据有差异的情况，或者几个相似文件都有相关细胞，但它们之间又有些许差异的情况，那么首先要对比几个数据间 cell number 是否一致，如果不一致，要查几个数据间 cellID 是否一样。如果发现 cellID 存在差异，请尽量使用细胞数和文章中使用的细胞数一致的数据。如果所有数据的 cell number 都和文章不一致，那么使用作者 data availability 里提到的 accession number 所使用的数据生成矩阵，并尽量根据 cluster 信息挑选细胞使其和文章最为接近。生成矩阵后，使用 cellID 完善 cluster 信息，并把没有对应 cluster 的 cell 补上 cluster name “notAvailable”。

- 如果实在不知道该不该分part，需要询问管理员寻求建议。
- 划分 part 后，在数据集文件夹(../GSE*****/)下新建一个description.txt文档,写入每个part对应的 description，subDataset，和 correspondingFigure等信息。

#### 3. 如果有分part（特别是同一个cellID在不同part中出现时），需要在每个study的part_1/processed_data/README.json文件里面加一个字段，relationship来描述这个study中各个part之间的关系，如："relationship": "part_2是part_1的子集，part_5是part_3/4中部分细胞的并集"等的描述。

#### 4. 填写 description 文件，内容及格式如下（一审人员需要把名字写在description.txt里面）：
- 特别注意填写每一项时不要在冒号后面加空格，各项填写不能使用任何非英文字符，但是可以用中文在每一项之外备注。各 part 需要描述清楚应该使用的数据。如果是 GSE 数据，可以清晰地根据 GSM info 得知各 sample 的确切信息，比如使用模版 script.ipynb 中的 sample = my_builder.sample_info(GSE = ‘') 查看各 sample 基本信息。part description 中要写清楚每个 part 对应文件里的 xxx 细胞，或者要使用使用了 xxx 测序方法的文件，或者直接写出要使用的文件名。可以不把数据/文件拆分放到相应 part 的 downloaded data，但需要描述清楚应该使什么文件/数据。注意所有给标注同学提供的字段和正式标注要求的 controlled vocabulary 一致



- title:注意粘贴的时候在最后不能有”.”
- PMID:
- accessionNumber:
- subDataset: 如果有不只一个part，则根据part_n填为SubDataset-n；只有一个part不填。注意！不要填写part_n
- description:The original article contains N subDatasets, which are different by species/library preparation method/tissues/cells/protocols (放用于区分part的关键词). This subDataset is based on human/mouse data/xxx tissue/xxx cells/xxx method (填写part间的区别信息).

- part_n 仅一个part不需要填写 subDataset 和 description
- correspondingFigure:填写每个part对应的聚类图。需要注意格式。如：1-a(代表Figure 1.a),supplementary/extended files 里的相关图命名格式写 s1-a/extended1-a，没有对应的图填notAvailable

- tissue:填写

- 以下三项如果是 TRUE 则需要注明要使用的相应文件名。附件可以自行下载后上传，或者使用 linux 命令 nohup wget xxxx(网址链接) > log.txt & 后台下载到 downloaded data 文件夹，生成的 log.txt 日志请检查是否显示 100% 下载完成，确认下载无误请删去 log.txt。如有下载问题请联系我们。非后台下载：cd 到 downloaded data 文件夹直接使用 wget xxxx(链接) 会自动显示下载百分比。
  - clusterAvailability:
  - tSNEAvailability:
  - UMAPAvailability:
- 当数据不是GEO来源的时候，需要填写dataURL:

## <span id="head8">二审： </span>
负责人：张萌栩 
#### 二审基本原则：检查数据集中每一项填写的内容是否有问题。
#### 数据集状态更改原则：
	1）标注和二审修改中间都不需要更改状态，
	2）直到二审结束进入三审时，需要把状态更改成Feedback
	3）如果在三审中间又发现有错误，会把状态更改为InProgress（实习生修改好后三审的人会直接关掉），所以大家不要把二审修改的也改成这个状态了。
	4）若没有其他错误了就会关掉任务状态相应改为Closed

### <span id="head9">二审 修改回收步骤： </span>
负责人分配任务，
- 1）	二审目前由full-time员工指派，进行二审的实习生会被分配一些数据集，并在redmine的相应数据集下被设置成watcher，被设置成watcher之后关于任务的所有的变动都会收到邮件提醒，二审人员接到任务后自行去user文件夹下寻找数据集进行审核，请不要把inspection.ipynb留在code文件夹里。

- 2）report一般会在redmine上，就需要在report和数据集的基础上进行审核，如果有错误，记录在redmine上，然后返回实习生修改。除metadata的错误可由审查人员直接在原文件中自行改动之外，其余错误均需按照以下步骤！

- 3）	当修改人在redmine上反馈修改完成之后，审查人去该目录下进行二次检查。除了原有问题之外，需重点看以下几点：
    - 如果是矩阵需要改动，需检查其相应的自动生成函数是否都运行了（可根据文件更新时间进行判断），包括：tsne, cluster, auto_calculation, downsample（downsample这个只有回溯时会有）等；
    - metadata里面的research topic，clusterAvailability以及tSNEAvailability需进行二次核查，tissue，journal，libraryPreparationMethod需要确保格式正确

- 4）	如果没有错误，或者修改好了没有其他错误了就可以把数据集放到3rd_inspection这个文件夹里面并把redmine上的状态改成Feedback状态：
针对在node02服务器上修改的人：将数据集打包压缩(如果数据集较小可不打包压缩，但还是建议先打包压缩)，并scp回到阿里云，拷贝到路径：/home/biodb/data/3rd_inspection/，如果太大，可以联系管理员单独回收；针对在阿里云服务器上修改的人：将数据集move到路径：/home/biodb/data/3rd_inspection/。在数据改完之后均需要放在以上这个路径中。

- 5）	确认数据集已拷贝至指定路径后，需要删除原来的修改人目录中的数据（不要留有冗余数据）。

- 6）	在redmine上更改任务情况的状态为Feedback，审核人员要及时查看自己负责的审核任务是否有更新，及时审核修改。

- 7）	最后由三审人员在指定3rd_inspection文件夹下做最后审查。小错误自己改改就好的，可以在直接改完后移动到correct文件夹下。

- 8）	如果有优秀的实习生，并且其本人有意愿，可以让他们接触审核工作，帮忙分担工作压力，但是质量控制要把握好。

### <span id="head10">补充教程： </span>
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


## <span id="head11">三审： </span>
负责人：陈淳、天然（暂定）
## 只有三审人员可以在redmine上进行任务的关闭，即把任务状态更改为closed。
### 三审 修改回收步骤：

- 1）	再进行一次二审的操作，不过可以大体浏览。发现错误后在renmine上记录，同时返回实习生修改。(请注意记录二审的漏检率，用作汇报时证明三道审核制度下的优势)

- 2）	完全没有错误了之后，需要把README.json中的notPassed改为passed,并保存。

- 3）	在redmine网站上close相应的任务，并把数据集移动到阿里云服务器的/home/biodb/data/3rd_inspection/correct文件夹下。

- 4）	最后，负责人会把更改好的数据集转移到node01服务器上。

### 审核的汇总表格流程
周期：每周更新一次数据集回收情况
流程
1. 每月生成一张新的dataset_inspection.xlsx表格记录整个月的数据集标注情况，
2．每周五下发数据集时，由一审负责人更新excel表格中数据集编号和title信息。
3. 收包时由二审负责人更新完成的信息到excel表格中，要填写标注审核的人员的信息。二审负责人主要负责标注流程，质量等的把控。
4. 除此之外，管理员需每周查看两次各个实习生完成的数据集数量，及时了解实习生的情况。
下发数据及之后长时间不做怎么办？
在每周回收数据集时，会发现是否有本周下发的数据集没能close，这时需要审核没做完的数据集是因为什么原因。
- 1）	数据集过于复杂（可以适当延长回收日期）
- 2）	实习生没有做，并且没有及时通知（需询问是何原因，是否还有意愿继续做数据集？）如果没办法完成数据集，及时换人。
