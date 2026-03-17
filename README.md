# 深度学习常见功能库
主要基于pytroch库

### eval,train,no_grad
```bash
model.eavl()把模型设置成推理模式，此时在训练模式中进行dropout，BN等操作会还原
一般配合with torch.no_grad():使用。

model.eavl()在蒸馏，微调，推理，测试，保存模型时候常用。模板为：

teacher_model.eval()
with torch.no_grad():  # 禁止梯度计算
    teacher_logits = teacher_model(input_ids)

with torch.no_grad()操作只是不算梯度了，即使没有这个操作也不会更新权重
只要不计算loss以及backward就不会更新权重
optim.zero_grad()
loss.backward()
optim.step()
with torch.no_grad()只是不算梯度节省内存

一般model.eavl()后还需训练要开启model.train()

记住一句话：
teacher_model.eval () = 保证权重不被改变
with torch.no_grad () = 禁止计算梯度，省显存、提速
```

## with
```bash
with xx：的功能为可以自动关闭，比如：
with torch.no_grad():
    xxx
在执行完xxx语句后会自动关闭，也就是关闭torch.no_grad()，开始计算梯度
如果没有with则后续一直都是不计算梯度，或者是要自己手动打开
```
