

根据你贴图中的 README.md 和 Result_Norm.md（它们现在都在根目录），我帮你总结一下：

⸻

✅ 训练模型

你可以用以下命令训练：

python python/main.py \
  --dataset=ml-1m \
  --train_dir=default \
  --maxlen=200 \
  --dropout_rate=0.2 \
  --device=cuda

各参数说明：
	•	--dataset=ml-1m：使用的数据集在 python/data/ml-1m.txt
	•	--train_dir=default：保存模型的位置
	•	--maxlen=200：每个用户最多保留最近 200 条行为
	•	--dropout_rate=0.2：Dropout 比例
	•	--device=cuda：使用 GPU 训练（如果没有 GPU 改成 cpu）

⸻

✅ 测试 / 只进行推理

如果你已经训练好模型，并且存储了权重（比如在 ml-1m_default/ 文件夹中），可以用如下命令进行测试：

python python/main.py \
  --device=cuda \
  --dataset=ml-1m \
  --train_dir=default \
  --state_dict_path='ml-1m_default/SASRec.epoch=1000.lr=0.001.layer=2.head=1.hidden=50.maxlen=200.pth' \
  --inference_only=true \
  --maxlen=200

注意：
	•	--state_dict_path 必须指向训练保存的模型参数文件
	•	--inference_only=true 表示只推理不训练

⸻

📁 说明你现在的目录结构
	•	python/data/*.txt：包括 ml-1m, Beauty, Steam 等预处理后数据（每个用户一行，项目 ID 序列）
	•	python/model.py：模型结构定义（SASRec）
	•	python/utils.py：数据读取、采样等辅助函数
	•	python/main.py：训练 / 推理入口
	•	ml-1m_default/：运行时保存模型参数和结果

⸻

🚀 建议操作步骤
	1.	安装依赖（推荐使用 Python 3.8+ 和 PyTorch >= 1.6）
	2.	准备好 python/data/ml-1m.txt，用原始数据预处理也行（格式是 user-id 的序列记录）
	3.	执行训练命令开始训练
	4.	执行推理命令评估效果（会输出 NDCG@10 / HR@10）

⸻

如需我帮你看 main.py 的训练流程、参数解释，或告诉你怎么自定义数据集，都可以继续问。你要是给我贴下 ml-1m.txt 文件格式的一两行，我还能给你举个采样 / mask 的例子。