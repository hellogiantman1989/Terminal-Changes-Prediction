# Terminal-Changes-Prediction
基于某城市移动终端用户的运营商数据预测未来三月内用户是否会终端变迁(用户从当前使用的手机品牌更换为其他手机品牌)。
应用xgboost算法和随机森林算法组合成多学习器预测模型。
根据比赛数据所给信息，此赛题属于无监督学习类型，无监督学习分为两种 情况，第一从所给数据不能识别出正负样本，
此种情况一般使用聚类的方法进行分析，第二从所给数据能够识别出正负样本，则使用分类的方法进行研究，本方
案通过判断用户手机型号是否更换将用户划分为正负样本。比赛要求对 2015 年 1-12 月的数据进行分析、并预测 
2016 年 1、2、3 月份内是否会换手机。针对需 要解决的问题和数据特征，我们主要从五个方面进行处理：数据预处理，正负样本判定，
特征工程，数据不平衡，以及训练集测试集构造。
首先，由于数据无法得出正负样本，本方案采用严格匹配每月用户的手机型号来区分正负。数据中大多数都是类别型特征，
很多算法(如 xgboost,逻辑回归， SVM)只能处理数值型特征，这样需要对类别型特征进行编码转化为数值型特征。
其次，根据比赛的数据，考虑到时间和换手机的次数对预测有影响，生成了用户 换手机的时间间隔特征和换手机次数特征。
然后，针对正负样本不平衡问题，采 用了增加样本的方法，使之训练模型的正负样本达到平衡。在训练模型时，对模型参
数加入了小范围的随机扰动，从而得到多个具有一定差异性的模型，以便对模型进行融合。 通过以上处理，我们使用xgboost 算法
进行模型的构造，此算法训练模型速 度很快，精度高，是 kaggle 比赛上数据大神们必用算法之一，我们使用了单模型， 多模型融合来实现最终的结果。 
1.将原始数据解压到 data 目录下，并将文件名改为时间格式，如 201501 等 等。
2.类别处理   运行-category_process 目录下，prodata.py 对类别进行处理并离散化， merge_num.py 对离散化的数据整合成一个数据。
3.正负样本处理   运行-label_process 目录下，processData.py 对数据型号进行严格匹配， 得出正负样本，processlabel.py 对 10，11 间型号大小写进行严格匹配，最终 得出所有正负样本。label.py 对每月的正负样本进行整合。 
4.特征处理，可视化    运行-model_process 目录下，xgb_para1.py 分析手机品牌和型号， Threechange.py 统计手机的转化型号并可视化，changebrand.py 分析手机品牌的 换机概率，label.py 统计手机型号的转换。
5.模型    运行-model_xgb 目录下，adddata.py 构造训练集数据，testdata.py 构造测 试集数据，xgb_model.py 训练 xgboost 模型，avg_preds.py 模型的融合。 
