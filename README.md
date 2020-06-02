# 計算機程式期末專案 - 人臉情緒辨識
<br/><br/><br/><br/>
組員名單：<br/>
108701037 應數一 黃馨霈 (加強CNN模型訓練結果)<br/>
108701039 應數一 許芝寧 (加強CNN模型訓練結果)<br/>
105304015 統計四 張智鈞 (建立GAN模型及訓練、合照影片的延伸應用、報告整理)<br/>
105304054 統計四 蕭貫博 (建立CNN模型及最終訓練、報告結論分析、報告整理)
<br/><br/>
### 一、專案主題與研究動機

我們這組的專案主題是人臉情緒辨識。

在過去，人類只能透過自己的經驗來辨認不同的表情，來判斷個別的情緒反應，同時判斷可能會產生錯誤，也難以對大量人群快速進行判斷。

而現今在圖像辨識及人工智慧的發展下，我們能夠利用機器來判斷一個人的情緒反應，能夠節省人力，也有更多可能的延伸應用，例如演講會談中對於觀眾的即時情緒調查。

此次專案內容會先建立起合照、獨照、影片中的個別人臉擷取模型，另外也利用GAN生成對抗網路來嘗試生成更多人臉的圖片。
<br/><br/>
### 二、資料來源

https://www.kaggle.com/c/challenges-in-representation-learning-facial-expression-recognition-challenge/data

利用kaggle網站中fer2013資料集，共含35,887張人臉圖片及對應的情緒標籤來做為訓練資料。

預設情緒標籤：
  - 0=Angry
  - 1=Disgust
  - 2=Fear
  - 3=Happy
  - 4=Sad
  - 5=Surprise
  - 6=Neutral
  
分類我們把資料較少的屬性及不明顯差異如disgust/surprise/neutral去除
<br/><br/>
### 三、需求套件
panda(資料處理)/ os(路徑/儲存控制)/ Image(處理圖片)/     openCV(處理圖片/影片及人臉偵測套件)/ tensorflow_keras(深度學習模型建立/訓練)
<br/><br/>
### 四、實作

##### CNN


情緒辨識模型我們採用CNN來達到較佳效果，使用fer2013資料集，模型中採用四個CNN的
Conv2D及maxpolling並加入dropout來強化訓練效果也避免overfitting，訓練過程learning rate使用0.001，loss funtion採用crossentropy並一共訓練四十次，最後情緒辨識模型訓練完畢準確率有超過70%。
##### GAN

生成人臉的想法我們利用fer2013的資料來嘗試自動生成人臉，生成器與判別器採用卷積神經網路訓練得到初步結果，並且generator利用upsampling複製抽樣的方式，慢慢增加維度以符合原始資料也有利用dropout來加強訓練。
雖然生成的照片可以看出是人臉，但難以辨認其情緒，原先本來有打算利用GAN來增加資料量，但是結果再加入GAN生成的照片對CNN情緒辨識模型準確率沒有顯著提升。

##### 合照/影片應用

在人臉擷取模型我們利用opencv中「haarcascade_frontalface_default.xml」這個人臉分類器來偵測出合照中的個別人臉並切分開來儲存，影片也是同樣概念，而在測試過後確實能夠精準偵測個別人臉，並且再套入CNN人臉情緒辨認模型，可以精準的辨認出大部分的情緒。

<br/><br/>
### 五、各模型程式碼與結果呈現

###### CNN
![CNN](https://github.com/patr8609/face/blob/master/readme_graph/cnn.jpg)
![CNN1](https://github.com/patr8609/face/blob/master/readme_graph/cnn1.jpg)
###### generator
![gen](https://github.com/patr8609/face/blob/master/readme_graph/gen.jpg)
###### discriminator
![dis](https://github.com/patr8609/face/blob/master/readme_graph/dis.jpg)
<br/>
![gan](https://github.com/patr8609/face/blob/master/readme_graph/gan.jpg)
<br/>
###### 合照應用
![1](https://github.com/patr8609/face/blob/master/readme_graph/1.jpg)
![pic1](https://github.com/patr8609/face/blob/master/readme_graph/pic1.jpg)
![pic1p](https://github.com/patr8609/face/blob/master/readme_graph/pic1p.jpg)
<br/>
![2](https://github.com/patr8609/face/blob/master/readme_graph/2.jpg)
![pic](https://github.com/patr8609/face/blob/master/readme_graph/pic2.jpg)
![pic2p](https://github.com/patr8609/face/blob/master/readme_graph/pic2p.jpg)
<br/>
###### 影片應用
![output2](https://github.com/patr8609/face/blob/master/readme_graph/output2.gif)
<br/>
![final_output](https://github.com/patr8609/face/blob/master/readme_graph/final_output.gif)
<br/>
![final_output(1)](https://github.com/patr8609/face/blob/master/readme_graph/final_output%20(1).gif)
<br/><br/>
### 六、總結與展望

總結：模型成果能快速辨別各類照片或影片中之個別人臉情緒
展望：能更優化GAN模型以產生更多有效訓練資料，以加強情緒辨認的結果，能夠配合這些模型做出更多人臉相關的有趣應用(ex:辨別性別/年齡/影片AI換臉...)
<br/><br/>
### 七、參考資料

https://www.freecodecamp.org/news/facial-emotion-recognition-develop-a-c-n-n-and-break-into-kaggle-top-10-f618c024faa7/<br/>
https://github.com/jeffheaton/t81_558_deep_learning/blob/4543275232ed555b8f99277d18bf55b227f469db/t81_558_class_07_2_Keras_gan.ipynb<br/>
https://towardsdatascience.com/face-detection-in-2-minutes-using-opencv-python-90f89d7c0f81




