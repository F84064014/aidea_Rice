* TODO:
    * 重新調整訓練資料21天的大小(當初都切250)
    * 嘗試加入隨機調整亮度、對比度的資料訓練(亮點的判斷效果差)
    * 想辦法增加模型的準確度(不知道 希望可以)
    * miniRiceField_2 使用transform資料做transfer learning => precision高 recall低

* firstVGxy_clear2.zip
    * 0.9280611
    * 基於clear的結果再做一次(大約少了40個)

* firstVGxy_clear.zip
    * 0.9278924
    * 將太過相近的兩個點之中點結合為新的點 (threshold=20)

* firstVGxy.zip
    * 0.9200131
    * 使用 full_pred_vni_rf32_XX.4.zip 與 xmid ymid融合

* firstVG.zip
    * 0.922332
    * 使用 full_pred_vni_rf32_XX.4.zip 與 xmid 作融合

* full_pred_vni_rf32_XX.4.zip
    * 0.9260716
    * 使用ricefield3

* Merge6.zip
    * 0.9222249
    * dir1 = r'full_pred_vni_rf22_48X.4'
    * dir2 = r'full_pred_vni_rf22_XX.4'

* full_pred_vni_rf22_XX_214.4.zip
    * 0.9024461
    * 21天的test用400

* full_pred_vni_rf22_XX.4.zip
    * 0.9203362
    * 都用最大的model

* full_pred_vni_rf22_48X.45.zip
    * 0.0.9179553
    * conf 0.45
    * 48天使用最大的model + miniRiceField2

* Merge5_inv.zip
    * 0.9091614
    * inverse of Merge5

* Merge5.zip
    * 0.9180895
    * dir1 = r'full_pred_vni_rf22_48X.4'
    * dir2 = r'full_pred_vague_norep4_intersect'

---
* full_pred_vni_rf22_48X.4.zip(1st best)
    * 0.9209981
    * conf 0.4
    * 48天使用最大的model + miniRiceField2
---

* Merge4.zip
    * 0.9178281
    * dir1 = r'full_pred_vni_rf22'
    * dir2 = r'full_pred_vague_norep4_intersect'

* Merge3.zip
    * 0.9183411
    * dir1 = r'full_pred_vni_+8_rf2'
    * dir2 = r'full_pred_vague_norep4_intersect'

* full_pred_vni_rf22.zip
    * 0.9022193
    * 48 apply rf2 model

* Merge2.zip
    * 0.9153293
    * dir1 = r'full_pred_vni_+8_rf2/'
    * dir2 = r'Merge1'

---
* Merge1.zip (2nd)
    * 0.9192960
    * 將full_pred_vni_rf2(0.945;0.877) 和 full_pred_vague_norep4_intersect.zip(0.923;0.907)
    * 以full_pred_vni_rf2為基準 若sqrt(360)距離內有重複的直接以基準的答案表示
    * 個別沒有重複的全部都加入
---
---
* full_pred_vni_rf2.4.zip (3rd)
    * 0.9147970
    * 下修信心至0.4

* full_pred_vni_rf2.zip
    * 0.9053895
    * extra zone = 0
---

* full_pred_vni_+8_rf2.zip
    * 0.9051123
    * 修正21days在miniricefield的大小從(250,250)=>(256, 288)
    * 將原本的訓練資料集做隨機的亮度、上下顛倒、鏡射等等變換
    * 修正yolo邊框大小、48天邊框不變
    * 21天若標記數量>1000 邊框=30 否則=45
    * 以transfer learning的方式續原本的參數後繼續訓練
    * 95% precision(目前最佳)
    * 87% recall(低)

* full_pred_vni_+8c045.zip
    * 0.9115856
    * 下修信心至0.45

* full_pred_vni_+8c04.zip
    * 0.9080200
    * 不改21天radius，下修信心至0.4

* full_pred_vni_a+8.zip
    * 0.9085405
    * 只修正pair radius至5

* full_pred_vague_norep6_intersect_adaptiver-15.zip
    * 0.9080001
    * 嘗試將21天的zone width修正至10, pair radius修正至5

---
* full_pred_vague_norep4_intersect.zip (best without much change)
    * 0.9127589
    * 修正21天的zone width持續加大的問題(單純抓到bug)
---

* full_pred_vague_norep_intersect.zip
    * 0.9053111
    * 將兩個邊界+-zone width的交集區域內的所有標記座標平均做為新的點(無論如何只要找到就平均)

* full_pred_vague_norep.zip
    * 0.9013193
    * 過濾重複標記的資料點(理論上不應該有，可能為演算法錯誤所導致的)

* full_predconf0.5_vague.zip
    * 0.8886576
    * 將每個分割圖片合併時的邊界點做結合(距離小於40pixels且都在邊界的範圍內及視為同一點)

* full_predconf0.5
    * 0.8639533
    * 設置條件過濾所有信心在0.5以下的標記

* full_pred
    * 0.8068053
    * 將圖片分割成數塊 (21天皆為(2304, 1728), 48天皆為(3000,2000))
    * 圖片大小固定=> 21每張大小(256,288) 48天每張大小(250,250) 都可以整除
    * yolov5 將21天和48天分開訓練 --img 200 (raw data)
