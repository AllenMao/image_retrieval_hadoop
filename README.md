### 1. ��������

-��Hadoop2.x�У�HDFSĬ�Ϸֿ��СΪ128M�����ֱ�ӽ�һ����ͼ���ϴ���HDFS�У��ͻᵼ�¿ռ��˷ѣ�һ��ͼ���ռ��һ���飩������Ҫ����namenode�������ϴ��ļ�������һ��Ԫ���ݽ��м�¼��e.g. һ��ͼ���Ӧһ��Ԫ���ݣ���ÿ��Ԫ���ݵĴ�СΪ150�ֽڡ������20M���ļ��� ÿһ���ļ���Ӧһ��block����ô�ͽ�Ҫ����namenode 3G���ڴ���������Щ��¼��Ϣ�������ģ�ٴ�һЩ����ô���ᳬ���ֽ׶μ����Ӳ����������ļ��ޡ���û��ʲô�õķ�ʽ���ﵽ������Ҫ�Ľ����

-���ǿ϶��ģ����С�ļ��ķ����У�Sequence File

### 2. Sequence File

-ͨ�����ڡ�the small files problem���Ļ�Ӧ���ǣ�ʹ��SequenceFile�����ַ�����˵��ʹ��filename��Ϊkey������file contents��Ϊvalue��ʵ�������ַ�ʽ�ǳ����á������10000��100KB���ļ�������дһ������������ЩС�ļ�д�뵽һ�������� SequenceFile��ȥ��Ȼ��Ϳ�����һ��streaming fashion(directly or using mapreduce)����ʹ�����sequenceFile�������е��������ѧϰ�г�����MNIST���ݼ���

### 3. ����ͼ��������ȡ

-��ȻHadoop�Ѿ�Ϊ�����ṩ����Щ�ӿڣ���дMapReduce����ͺܼ��ˡ���Map�׶Σ���Ҫ�����Ƕ�ȡͼ�񣬲�ͨ��д�õ�������ȡ�㷨�õ�������������<filename, feature_vector>���д洢����Reduce����������������Ϊ0����ΪMap�׶��Ѿ��ﵽ���ǵ�����


### 4. ����ͼ�����

-����Ҫ����������ͼ��ת��Sequence File����Map�׶Σ���Ҫ���������ͼ���������ȡ��ƥ��ͼ����е�ͼ����<filename, img1_dist1>�������Reduce�׶Σ����е�Map�����������ܵ�һ��Reduce�У���Ȼ��Ҳ�������Reduce���������ҪдPartition�ˣ�����ͬһ���ؼ��֣�������ͼ�񣬵ļ��Ͻ������򣬲�����topk��ͼ�����ơ�<filename, img1_img2_..._imgk>����ʽ��������ս�������HDFS�С�

### 5. ͼ���ѯ

-�õ�����ͼ��ļ�����������֪��ĳһ�Ŵ�����ͼ��Ľ��������ֻ��Ҫͨ��hdfs�Ľӿں�������ȡָ���ļ���ͼ�������м�¼���Ϳ��Եõ���Ӧ��topk��ͼ�����ơ�


-���в��㣬��ӭ����^-^��