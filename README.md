# Customer Analysis JD.com

## Understand the data fields
Separate all fields into 3 groups: **User, Purchase Behavior, Product/Merchant**
![image](https://github.com/cassiezy/Customer_Analysis_JD.com/blob/master/Readme/2_Field.png)

# What：用户的购买趋势是怎样的？
+ 选择什么变量？
  - 购买行为：type
  - 行为时间：action_date
+ 呈现怎样的数据关系？
  - 趋势关系
+ 可以选择怎样的图表？
  - 折线图
  - 热力图
  
![image](https://github.com/cassiezy/Customer_Analysis_JD.com/blob/master/User_Purchase_Analysis.png)
![image](https://github.com/cassiezy/Customer_Analysis_JD.com/blob/master/Readme/4_user_purchase.png)

# Why：影响用户购买行为的因素都有哪些？
+ 选择什么变量？
  - 购买行为：type
+ 影响因素可思考维度：
  - 用户维度：年龄，性别，城市等维度 
  - 商家维度：商家评分/粉丝数/商家类别等维度
  - 产品维度：
  - 漏斗分析：从页面访问->存购物车->下单->关注，可以结合多者之间的转化关系得出订单量和页面访问之间的转化关系（加分项）
+ 呈现怎样的数据关系？
  - 比较关系
+ 可以选择怎样的图表？
  - 柱状图
  - 环形图
![image](https://github.com/cassiezy/Customer_Analysis_JD.com/blob/master/Readme/6_funnel%20analysis.png)
![image](https://github.com/cassiezy/Customer_Analysis_JD.com/blob/master/User_Analysis.png)

## 影响用户购买行为的因素 – 用户维度

从用户角度来看，影响用户购买行为的因素有：**性别，年龄，会员等级，城市等级**

购买行为较多的用户特征为：**男性，5/6年龄组，1/5/6/7会员等级，4/3/5/1城市等级**

另外，平台应深入挖掘一下年龄组3和会员等级2/3/4的用户为何购买行为非常少。

## 影响用户购买行为的因素 – 商家维度
![image](https://github.com/cassiezy/Customer_Analysis_JD.com/blob/master/Merchant_Analysis.png)

从商家角度来看，影响用户购买行为的因素可能有：**店铺主营类别，商家评分，粉丝数，开店时间**

通过分析发现：
1. 虽然电子产品的浏览/关注/加购/点评数量都是最高的，但订单数量却很少。订单数量最多的是美妆，食品，服装和家电。看起来似乎更像是女性用户会购买的产品。然而事实上在京东购物的男性用户更多。（可以深挖一下原因，比如买礼物？）
2. 并不是店铺评分越高，订单越多。订单量多的店铺集中在9.4分上下。可能是因为高分店铺数量其实并不多。
3. 数据集是2018年2月至4月18日的，发现于2015-2017年开店的店铺订单量较高
4. 并非粉丝越多，订单越多。

## 影响用户购买行为的因素 – 产品维度
![image](https://github.com/cassiezy/Customer_Analysis_JD.com/blob/master/Product_Analysis.png)

从用户角度来看，影响用户购买行为的因素有：**产品品牌，产品类别，产品上市日期**

可以在仪表盘中查看，不同店铺类别最热销的产品类别，以及不同产品类别最热销的品牌，也可以查看不同品牌最热销的产品类别。比如，大衣卖得最好的品牌是H&M, HLA, Uniqlo, Baleno。
还可以发现，总地来说，新上市地产品销量更高。


# How：京东的业务部门可以怎么做，提升订单量？
## 1. 聚类分析
+ **目的**：进行客群分析，找到目标客群

+ **模型选择**：K-means Clustering Model 
	      （经过试验，选择k=3）

+ **变量选择**：会员级别，城市级别，性别，年龄组
如果有三方数据，可以再加入消费者收入，教育，爱好，使用京东的RFM数据等等。

**聚类结果：**

![image](https://github.com/cassiezy/Customer_Analysis_JD.com/blob/master/Readme/10_clustering_result.png)

由于数据限制，本次客群聚类的结果并不是很好，但仍可以看出Cluster 1 的客群是主力客群，更容易产生购买行为。其性别为男，年龄组5/6，会员等级为7，城市等级为4。京东可以target在这类人群，以提高订单量。

## 2. 逻辑回归分析
+ **目的**：预测用户是否会产生购买行为，以判断是否要推送营销信息

+ **模型选择**：Logistic Regression

+ **变量选择**：会员级别，城市级别，性别，年龄组，历史购买/浏览/加购/关注/评论数据
如果有三方数据，可以再加入消费者收入，教育，爱好，使用京东的RFM数据等等。

实际研究过程可以选择某个品牌来进行，用逻辑回归找出最有可能购买该品牌产品的用户，向其发送相应的营销广告。

## 3. 线性回归分析
+ **目的**：预测目标用户的购买金额

+ **模型选择**：Linear Regression

+ **变量选择**：
  - Y: 订单金额
  - X: 会员级别，城市级别，性别，年龄组，历史购买金额/浏览/加购/关注/评论数据
       如果有三方数据，可以再加入消费者收入，教育，爱好，使用京东的RFM数据等等。

实际研究过程可以选择某个产品类别来进行，用线性回归预测消费者可能下单的金额。

本数据集中缺少销售额数据，故无法进行线性回归分析。
