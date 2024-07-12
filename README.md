## 課堂作業：比較不同參數使用在GAN的訓練結果
### 使用Keras中 MNIST資料集作為樣本
![image](https://github.com/user-attachments/assets/700b252f-1bb0-4a9b-8047-e07d25e9d43f)

### 架構
**Discriminator**：從真實照片中取樣，對比從Generator生成的照片取樣中的差異，計算損失函數的值 (損失函數值越大，表示Discriminator越分不清真假)，回頭修正Discriminator和Generator

**Generator**：從隨機雜訊向量產生的圖片作圖，計算損失函數的值 (損失函數值越小，表示Generator生成越真實的照片) ，回頭訓練Generator (此時Discriminator不修正參數)

**參數意義**

  iterations = 訓練次數

  batch_size = 每次取樣進行訓練的個數

  Dense_dim = 每層神經元的輸出維度

  z_dim = 輸入進Generator雜訊向量的維度

  sample_interval = 每次取樣繪圖的次數

### Exp1. 比較不同輸入維度對訓練結果的差異 z_dim=50,100,150
![image](https://github.com/user-attachments/assets/1daf4bd9-a6c5-4f8f-9271-183675248a76)
![image](https://github.com/user-attachments/assets/395b52e3-1930-421c-9e82-adcfde85ed70)
![image](https://github.com/user-attachments/assets/8ae2e6d2-a7fd-43e3-8ae5-030d27c890ab)
1. 三種 z_dim 之下，accuracy 值下降， Discriminator loss 值則是上升趨勢，表示隨著訓練次數增加，對 Discriminator 而言，越無法區分真實和假圖的差異；而 Generator loss 值則呈現下降趨勢，表示其生成圖片越趨真實。
2. 以 accuracy 和 loss 值的變化穩定度而言，z_dim=150 時最為穩定，其餘兩者變化較劇烈。
3. 以 Generator loss 值而言，z_dim= 100 或 150 時訓練效果優於 z_dim=50 (值較低)。
4. 以 Generator 繪製隨機數字圖片而言，三種 z_dim 訓練的結果差異不大。
---
### Exp2. 比較神經元的輸出維度對訓練結果的差異 Dense_dim=64,128,256 
![image](https://github.com/user-attachments/assets/a306f2d5-df07-4e38-b7e1-9d40b65c028b)
![image](https://github.com/user-attachments/assets/35fb2d17-ee92-4644-b916-dc40c26c2b39)
![image](https://github.com/user-attachments/assets/999ce414-6f38-4031-857b-2a03905c39fa)
1. 以 Generator loss 值的變化穩定度而言，在訓練後期，dense_dim=256 時最為穩定，其餘兩者變化較劇烈。
2. 以 Generator loss 值而言，dense_dim 越高，訓練效果越好。其中 accuracy 低且 Discriminator loss 值高，而 Generator loss 值隨時間下降的幅度越大。
3. 以 Generator 繪製出的數字圖片而言， dense_dim 越高，圖片較接近真實
---
### Exp3. 若訓練次數高，是否會有比較好的訓練效果? iterations=200000 (sample_interval=10000)
![image](https://github.com/user-attachments/assets/a415882f-05ff-43eb-9c5e-a0c9b1eb279b)
![image](https://github.com/user-attachments/assets/2533d519-c0c5-4856-abf7-45c2bf1a4eec)
1. 以 accuracy 值和 Discriminator loss 值而言，在訓練次數20000次時訓練效果為最佳，之後反而變差；以Generator loss 而言，訓練效果在50000次之後效果最佳。
2. 以 loss 值和兩種 accuracy值而言，訓練效果約在50000次時達到穩定狀態 (即 loss 值和 accuracy 值不明顯變動)，在130000次之後反而小幅度上下變化。
3. 以 Generator 繪製隨機的數字圖片而言，訓練次數超過 50000 次之後，繪製的圖片較無雜點且邊緣清晰。
