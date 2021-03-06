## RSS Positioning
#### 無線網路定位方法實作
![Python](https://img.shields.io/badge/Python-blue.svg?)


- 動機
  - 實作 LBS 課程中，使用 RSS 訊號地圖的定位方法。
  
- 目標：
  - 以R語言撰寫
  - 實作 1NN、3NN、5NN 比對方法，並計算定位錯誤率。

- 前置步驟：
  > 1. 從網路上下載 UJIIndoorLoc dataset，免除 offline 資料收集步驟  
    http://indoorlocplatform.uji.es/databases/get/1/  
    https://www.kaggle.com/giantuji/UjiIndoorLoc
    
    - TrainingData.csv: 用來訓練之 radio database。
    - ValidationData.csv: 用來驗證效果之 radio database。
 
 - 程式流程  
   1. 撰寫程式從 TrainingData.csv 讀入 radio database，以自訂的資料結構儲存。  
   2. 採用 Euclidean distance 作為 distance 計算之演算法，撰寫對應之程式。  
   某筆資料中未偵測到的 AP 訊號可定為 100 或是-104。  
   3. 讀入 ValiationData.csv。  
   - 一筆資料做一次測試，將新的 fingerprint 與 radio database 的每項計算 distance，以距離最近的 fingerprint 其代表的位置作為預估的位置，並計算真實座標與預估座標的誤差。  
   最後計算 ValidationData 中的各自距離誤差與平均值，繪製成直方圖。  
   - 改採用 KNN (K = 3 或 5)的方法，挑選最近 K 筆資料將其 K 個座標值平均作為預估位置，並計算 ValidationData 中距離誤差與平均值，並繪製成直方圖。
 - 額外實驗
   - 在計算平均時，改成參考網址中權重計算的作法。
 
- 實驗結果  
  顯示 1NN、3NN、5NN 之誤差平均值與直方圖，
  - 1NN - 以距離最近的 fingerprint 其代表的位置作為預估的位置  
    <p align="left">
      <img src="https://github.com/ZhangChiYan/Introduction-to-Wireless-Internet/blob/master/md_img/1.jpg" />
    </p>
  - 3NN - 將其 3 個座標值”平均”作為預估位置
    <p align="left">
      <img src="https://github.com/ZhangChiYan/Introduction-to-Wireless-Internet/blob/master/md_img/2.jpg" />
    </p>
  - 3NN - 參考網址中權重計算的作法(weight)
    <p align="left">
      <img src="https://github.com/ZhangChiYan/Introduction-to-Wireless-Internet/blob/master/md_img/3.jpg" />
    </p>
  - 5NN - 將其 5 個座標值”平均”作為預估位置
    <p align="left">
      <img src="https://github.com/ZhangChiYan/Introduction-to-Wireless-Internet/blob/master/md_img/4.jpg" />
    </p>
  - 5NN - 參考網址中權重計算的作法(weight)
    <p align="left">
      <img src="https://github.com/ZhangChiYan/Introduction-to-Wireless-Internet/blob/master/md_img/5.jpg" />
    </p>

- 結果驗證  
  若要驗證實作出的結果是否正確，可與下方網址中的結果作比較
  - 結果參考網址：http://indoorlocplatform.uji.es/dashboard/ujiindoorloc/
