# 交通赛 #
## 简介 ##
- 分析成都市20天的出租车GPS数据，预测给定GPS轨迹的时间
- 第一次参加[大数据比赛](http://www.pkbigdata.com/)，第一次在团队中负责编程，第一次尝试使用python语言和新接触的API实现算法

## 算法 ##
- 训练集的数据信息[出租车id,纬度，经度，载客信息，时刻]
- 预测集信息[路径id,出租车id, 纬度，经度,载客状态,时间点]
- 使用到的第三方包有pandas,sklearn



1. 初始处理数据：原始数据排序并且增加加两列：瞬时速度、地区号，结果写入新的文件"天数temp.txt"
2. 计算个人平均速度[出租车id][时段]
3. 计算路段平均速度[地区号][时段]
4. 训练SVM，由X=[路段平均速度，个人平均速度，载客信息]，Y=瞬时速度训练得到
5. 预测轨迹上每一点的瞬时速度，积分求时间

## 疑问 ##
- 就算只是用一天的数据做预测集，在集群上三天也跑不完，从分割出来的小数据运行结果来看主要是卡在SVM的训练和预测上，SVM算法有何突破性的改进方法？
- 如何获取路段信息（非专业途径）？
- 在缺乏路段信息的情况下，如何使用类似于聚类的算法找到路段信息，使得预测结果更加准确？
