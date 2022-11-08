# PM2.5

這是一個利用Open Data做PM2.5預測的練習，將使用新竹地區2021年10~12月之空氣品質資料，進行時間序列分析&迴歸預測pm2.5值。


【Dataset】
空氣品質監測目的包括瞭解空氣污染來源、污染物傳輸特性及形成原因，以供空氣污染防制參考，同時瞭解民眾暴露在空氣污染物的情形，提供預警訊息。本資料集(如附檔)包含AMB_TEMP, CH4, CO, NMHC, NO, NO2, NOx, O3, PM10, PM2.5, RAINFALL, RH, SO2, THC, WD_HR, WIND_DIREC, WIND_SPEED, WS_HR 共18種屬性(汙染物)之逐時資料。
(資料來源: https://airtw.epa.gov.tw/CHT/Query/His_Data.aspx)

【Model】
PM2.5為連續之數值資料，故用回歸模型做預測，使用兩種模型 Linear Regression 和 XGBoost 建模並計算MAE
- 多元線性回歸模型：由於PM2.5的值是時間序列資料，可以用過去的資訊大致預測起伏，所以線性回歸效果較好，MAE平均絕對誤差較小。 
- XGBoost模型：結合了Bagging與Boosting的優點，與Bagging都是以Bootstrap的方式隨機抽取訓練樣本，但是樹之間是有相關性的；同Boosting，會針對前面model的錯誤去學習，但是又能透過正規化去改善overfitting問題。


使用10和11月資料當作訓練集，12月之資料當作測試集，將前六小時的汙染物數據做為特徵，未來第一個小時/未來第六個小時的pm2.5數據為預測目標
