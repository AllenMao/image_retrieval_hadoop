### 1. 问题描述

-在Hadoop2.x中，HDFS默认分块大小为128M。如果直接将一张张图像上传到HDFS中，就会导致空间浪费（一张图像会占用一个块），最重要的是namenode对所有上传文件都会用一个元数据进行记录（e.g. 一张图像对应一个元数据），每条元数据的大小为150字节。如果有20M个文件， 每一个文件对应一个block，那么就将要消耗namenode 3G的内存来保存这些记录信息。如果规模再大一些，那么将会超出现阶段计算机硬件所能满足的极限。有没有什么好的方式，达到我们想要的结果？

-答案是肯定的，解决小文件的方法有：Sequence File

### 2. Sequence File

-通常对于”the small files problem”的回应会是：使用SequenceFile。这种方法是说，使用filename作为key，并且file contents作为value。实践中这种方式非常管用。如果有10000个100KB的文件，可以写一个程序来将这些小文件写入到一个单独的 SequenceFile中去，然后就可以在一个streaming fashion(directly or using mapreduce)中来使用这个sequenceFile。这里有点类似深度学习中常见的MNIST数据集。

### 3. 批量图像特征提取

-当然Hadoop已经为我们提供了这些接口，书写MapReduce程序就很简单了。在Map阶段，主要工作是读取图像，并通过写好的特征提取算法得到特征向量，以<filename, feature_vector>进行存储。在Reduce任务数量可以设置为0，因为Map阶段已经达到我们的需求。


### 4. 批量图像检索

-将需要检索的批量图像转成Sequence File。在Map阶段，主要负责待检索图像的特征提取，匹配图像库中的图像，以<filename, img1_dist1>输出。在Reduce阶段，所有的Map的输出都会汇总到一个Reduce中（当然，也允许多个Reduce，这个就需要写Partition了），对同一个关键字，即检索图像，的集合进行排序，并返回topk张图像名称。<filename, img1_img2_..._imgk>的形式输出的最终结果存放在HDFS中。

### 5. 图像查询

-得到批量图像的检索结果后，如何知道某一张待检索图像的结果，我们只需要通过hdfs的接口函数，获取指定的检索图像所在行记录，就可以得到对应的topk张图像名称。


-如有不足，欢迎批评^-^。
