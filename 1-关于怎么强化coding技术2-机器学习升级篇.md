# Start





# Body

## 机器学习相关

### 一、脱离jupyter notebook 进行算法训练



### 二、整个相关流程

① 前台用户的数据保存到数据库，未来管理员可以导出这部分数据，然后用于机器学习的训练

② 后台管理员训练的时候，自己上传数据，训练完成会通知训练完成，并存储路径到数据库

③ 后台管理员可以对当前有的模型进行管理（改查删）



### 三、我当前需要处理的

#### 3.1、先对要拿来训练的数据样本进行标注并存储到数据库

> **`首先第一个模型是通过电压比率以及权重判定电路的五种健康状态`**





```
# 将数值预测转换为文本标签
def inverse_transform_labels(self, le, y_pred):
    return le.inverse_transform(y_pred)

# 在测试加载模型的代码中
# 加载 LabelEncoder
le = service_machine_learn.load_label_encoder('BackSupport\resource\machine_learn_model_save\label_encoder.pkl')

# 传入模型和数据，进行预测
predictions_numeric = service_machine_learn.predict(model, data_list_python_to_machine)
# 使用 LabelEncoder 将数值预测转换回文本标签
predictions_labels = service_machine_learn.inverse_transform_labels(le, predictions_numeric)
print("预测结果：", predictions_labels)
```







## 集成学习相关







# Question





# Reference



