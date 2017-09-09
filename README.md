# XiaoZhu_demo

# 第一部分： 爬取数据<br>
## 爬取范围：<br>
小猪短租房网站的 北京、上海、广州、深圳、长沙、武汉、成都、重庆等八座城市的数据。<br>
## 爬取方法：<br>
1. 首先找出主页列表页的url地址，将该页面的html解析出详情页的url地址和下一页的url地址。将地址保存为一个队列，防止重复爬取。<br/>
2. 在多线程主程序中添加一个参数max_depth，确定爬虫的深度。防止"爬虫陷阱"。找出列表页和详情页的url不同，利用re模块正则表达式找出需要保存在mongodb数据中的url.调用一个回调函数用BeautifulSoup模块进行解析数据。<br>
3. 利用threading模块展开多个线程，提高爬虫效率。默认5个线程。<br>
4. 下载页面的模块设置减速器，即相同域名的访问要间隔一定时间。<br>
## 爬取结果:<br>
爬取得到的数据存储在mongodb数据库中,经过转化后存为[xiaozhu.csv](./xiaozhu.csv)<br>

# 第二部分： 清洗数据<br>
1. 导入常用的python库, 如pandas、numpy、scipy、matplotlib、seaborn等。<br/>
2. 将采集到的房子的面积area转化为数值型变量。从每个地址中分离出所在的区,形成district变量。<br/>
3. 采集到的房子的布局变量layout的形式为"x室x厅x卫x厨x阳台"。将其数值加起来构成一个新的变量即房间数目rooms,再删除layout变量<br>
4. 将某些采集到的如表示'适宜居住x人"的变量sumpeople和床的数量'共x张'的变量beds, 将其清洗得到数值型数据。<br>

# 第三部分： 分析数据<br>
## 总体数据的结构分析：<br>
1. 分析原始数据的结构。共采集到2399条数据, 变量有12列。共有数值型变量两个。其他的都是类别型变量。<br>
2. 对数据进行<strong>缺失值分析</strong>。发现只有变量rate即各个城市短租房的评分存在缺失值。通过直方图按城市分析这个变量缺失值的分布。发现长沙的缺失值最多。<br>
3. 对数据进行<strong>异常值分析</strong>。这里把日租金rent_cost_day作为目标变量, 把房东性别sex_landlord、适宜居住人数sumpeople、床的数量beds、
房间数量rooms作为类别型变量。画出目标变量rent_cost_day分布的箱线图。以及目标变量关于各个类别变量分布的箱线图。我们保留保留那些日租金与所有日租金的均值的差的绝对值小于或等于3倍所有日租金的标准差的数据。这样除去异常值之后的数据集还有2361条。<br>
##  数值型变量分析:<br>
4.对数据进行<strong>相关性分析</strong>， 研究目标变量如何被数值型变量影响。同时画出数值型变量之间的相关系数图。<br>
5.对8个城市的日租金的总体分布进行分析。发现北京的平均日租金最高, 重庆最低。可以猜测日租金的高低可能与经济发展水平与消费水平以及物价有关系。对除去异常值后的数据集的目标变量日租金进行对数转化后，绘制概率分布图。发现较好地符合正态分布。 对8个城市按区描绘日租金的散点图。并用折现连接起来。<br>
6. 对另一个数值型变量房子的面积即area也进行如上述相同的分析与描绘。<br>
## 类别型变量分析:<br>
7. 通过分析八座城市的房东性别sex_landlord的比例分析。发现女性房东的比例几乎是男性房东比例的两倍。<br>
8. 观察分析八座城市的各个区发布短租房信息的数量来获取关于短租房市场比较繁荣的区域。

# 详细的分析过程与描述:[小猪短租房详细分析](./小猪短租房分析.ipynb)

