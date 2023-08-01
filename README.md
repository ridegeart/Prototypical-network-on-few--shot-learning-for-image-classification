# Prototypical-network-on-few--shot-learning-for-image-classification
A custom dataset implement for [easy-few-shot-learning]. Dataset from AI CUP 2022 秋季競賽，[農地作物現況調查影像辨識競賽-秋季賽：AI作物影像判釋]。

## Load Data
主辦給的資料集，共有34個類，每個類有2041張照片，為了符合easyfsl使用的訓練資料格式，重新整理各類圖片。
1. 資料夾名稱：編號0-33。
2. 照片名稱：每個類裡的每張照片由a_b命名，a代表類別，b代表第幾張圖片(0-2040)。
3. 資料集大小：超過 170G。

## Training Setting
example code : [my_first_few_shot_classifier.ipynb]
  
### DataLoader
1. PyTorch 自帶的 DataLoader 讀取單個 batch 的圖像，而不考慮 query set 還是 support set (from Meta Learning)。
2. 在給定的類別數間均勻分佈的圖像：Custom DataLoader TaskSampler，從數據集中採樣 n_way 類，然後為每個類採樣 n_shot、n_query 圖像（每批中總共 n_way * (n_shot n_query) 圖像）。
3. 將資料分成query set和support set：自定義的 collate 函數來替換內置的 PyTorch collate_fn。
### Training Strategy
1. Loss : cross entropy
3. Optimizer : Adam

[easy-few-shot-learning]: https://github.com/sicara/easy-few-shot-learning
[農地作物現況調查影像辨識競賽-秋季賽：AI作物影像判釋]:https://aidea-web.tw/topic/5f632f38-7213-4d4d-bea3-117ff13c1afb
[my_first_few_shot_classifier.ipynb]:https://github.com/sicara/easy-few-shot-learning/blob/master/notebooks/my_first_few_shot_classifier.ipynb
