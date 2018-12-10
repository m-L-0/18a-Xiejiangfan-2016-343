<h1>Clustering Schoolwork</h1>
<h2>一、程序简介</h2>
谱聚类对鸢尾花数据集进行处理，绘图，并输出正确率。
<h2>二、函数说明（Spectum类中）</h2>
<p>1.normalization  功能：把数据集预处理。</p>
<p>2.ou_dis         功能：求两节点欧氏距离 </p>
<p>3.calEucliDistanceMatrix  功能：构建相似矩阵W</p>
<p>4.calLaplacianMatrix      功能：标准化拉普拉斯矩阵L，包括求度数矩阵D</p>
<p>5.getEigVec      功能：求拉普拉斯矩阵L的特征值和特征向量</p>
<p>6.Draw1          功能：画原始数据集</p>
<p>7.Draw           功能：画谱聚类后的数据集</p>
<h2>三、任务列表</h2>
1.鸢尾花数据集图
<p>(https://github.com/m-L-0/18a-Xiejiangfan-2016-343/blob/master/Cluster/deal_data.png)</p>
<p>2.阈值 0.76 0.70   同类别样本大于0.76是黑色实线，大于0.70是灰色实线；不同类样本大于0.76是灰色虚线，大于0.70是浅灰色虚线。</p>
<p>3.带权值邻接矩阵</p>
   #构建相似矩阵
    def calEuclidDistanceMatrix(self):
        Data = self.data
        N = len(self.data)
        self.W = np.zeros((N, N))
        for i in range(N):
            for j in range(i,N):
                self.W[j][i] = self.W[i][j] = np.exp(-np.sum(np.square(self.data[i] - self.data[j])) / (2 * pow(self.gamma, 2))) #高斯核函数
        a = np.ones(150)
        b = diag(a) 
        self.W = self.W - b #W矩阵对角线元素为零
<p>4.使用kmeans进行聚类</p>
  <p>clf = KMeans(n_clusters=3,algorithm='auto')</p>
  <p>bel_pred = clf.fit_predict(V) #label_pred = clf.labels_ 相同效果</p>
<p>5.聚类结果图示</p></p>
 <p>(https://github.com/m-L-0/18a-Xiejiangfan-2016-343/blob/master/Cluster/data.png)</p>
<p>6.分簇正确率 0.72</p>
  <p>28%的错误率在于有两类数据很接近，算法不能很好的分出来混入一簇中的其他样本，就归为己类。导致错误率挺高。</p>
