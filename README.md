## jetpack-installation  
### 前提条件  
NVIDIA Jetson Developer Kit 向けの初期設定方法です。  
メーカーが異なる本番機端末では、本手順とは、別の手順を用いてセットアップします。  

### 事前準備  

以下、準備するものです。  
 
・NVIDIA Jetson 端末  
・ホストサーバー  
・ホストサーバー上にインストールされたUbuntu OS    
・ディスプレイ（ホストサーバー用）  
・HDMI ケーブル（ホストサーバーとディスプレイを繋ぐため）  
・USB ハブ（Jetson とホストサーバーを繋ぐため、マウスとキーボード類をホストサーバーと繋ぐため）   

JetsonへのJetpackを利用したUbuntu 等のインストール状況は、ホストサーバー上で、インストールの状況を確認することができます。    
 
### インストール手順  
#### 1.ホストサーバーでのNVIDIA SDK Managerのダウンロード・セットアップ・起動　　  
  以下URLは、上述のJetson Download CenterページのNVIDIA SDK Managerのリンクになります。ubuntu上でterminalを立ち上げ、以下のコマンドを実行してSDK Managerをダウンロードします。    
 
```  
wget https://developer.nvidia.com/embedded/dlc/nv-sdk-manager  
```  

ダウンロードされたnv-sdk-managerファイルは、debパッケージとなっており、以下のコマンドでインストールします。  
 
```  
sudo dpkg -i ./nv-sdk-manager  
```  

ライブラリが不足するケースがあるため、その場合、  
以下のコマンド等で、不足するライブラリをインストールします。  

```  
sudo apt install libgconf-2-4 libcanberra-gtk-module  
```  

   　　
ホストサーバーでNVIDIA SDK Managerを起動します。  
たとえば、画面左下のアプリボタンをタップすると各アプリを検索することができ、NVIDIA SDK Managerを表示することができます。　　

#### 2.Jetson端末のセットアップ   
2-0. JetsonとホストサーバーをUSBで接続します。そして、Jetsonを「Force Recovery Mode」で起動します。  
 
2-1. ホストサーバーににおいて、ホストサーバーがusbで正しくJetsonと接続されていることの確認（以下の通りコマンド入力）
``` 
lsusb
```   
「NVIDIA Corp.」 が表示されることを確認します。  　　
 
2-2. ホストサーバーでのSDK Managerの起動とパラメータの選択（Ubuntu GUI から該当アプリケーションの検索等をして実行）   
SDK Manager の 画面上で　「Jetson」、「〜」、「〜」、「〜」、にチェックを入れ最新のversionを選択します。数字が最も大きいVersionが最新となっているため、数字が最大のVersionを選択し、continueをタップします。    　　
  
2-3. SDK ManagerによるJetson端末へのJetpackのインストール  
SDK Managerで「インストールの同意」にチェックを入れ、「continue」をタップします。  
全てのインストール工程が終了するまでに、少し時間がかかりますので待ちます。各工程が終了すると、statusがInstalledになります。「Flash Jetson OS」までの該当項目のstatusがInstalledになったことを確認します。   　　 
 
2-4. Jetsonの起動（自動）    
ホストサーバーで“SDK Manager is about to install SDK components on your Jetson ####(####はJetsonの機種名)”というポップアップがでたら、自動でJetson端末が立ち上がります。         

2-5. JetsonにおけるUbuntuの初期設定     
     言語 は English、keyboard は 日本語 に設定します。   
     タイムゾーン 東京 に設定します。   
     あなたの名前：XXXXXX   
     コンピュータの名前：{予め決めたJetson端末固有の名前 eg.orionなど}    
     ユーザー名：XXXXXX   
     パスワード：XXXXXXXXXXX     
 
2-6. Jetsonにおけるubuntuへのログイン     
     JetsonのUbuntu上で先ほど作成したアカウントでログインします。        

2-7. Jetsonのパワーモードの設定（参考）    
     必要に応じて、Jesonのパワーモードの設定を変更します。Ubuntu Desktop右上にあるNVIDIAのマークが表示されている部分をタップし、“Power mode”を選択後、例えばAGX Xavierであれば、”MODE 30W ALL”を選択します。
    
2-8. JetsonのIPアドレスの確認（参考）    
     JetsonのUbuntu Desktop左上にある緑のアイコン“Search your computer”をタップし、”terminal”と検索してterminalを開きます。Terminal上で以下のコマンドを実行し、IPアドレスを確認します。  
     
2-9. JetsonのFanの設定（参考）  
     下記コマンドで、Jetson端末のファンを回し、回転数を指定します。  
     「255」の部分で回転数を指定します。0（最小値）～ 255（最大値）の間の数値を入れてください。  
```
sudo sh -c 'echo 255 > /sys/devices/pwm-fan/target_pwm'
```
