Azure Machine Learning - ハンズオン MNISTで手書き文字認識
=============

## 機械学習とは

## MNISTデータセットとは
国立標準技術研究所の混合データ セット (MNIST データ セット) は、さまざまな IR アルゴリズムを比較する際のベンチマークとして機能させるように、IR の研究者によって作成されました。基本的な考え方としては、テストする IR アルゴリズムまたはソフトウェア システムがある場合、MNIST データ セットに対してアルゴリズムまたはシステムを実行し、他のシステムについて以前発行された結果と比較します。

データ セットには計 70,000 枚の画像が含まれており、そのうち 60,000 枚は学習用画像 (IR モデルの作成に使用) で 10,000 枚は判別用画像 (モデルの精度の評価に使用) です。各 MNIST 画像は、1 つの手書き数字をデジタル化したものです。サイズはそれぞれ 28 x 28 ピクセルです。各ピクセル値は 0 (白) ～ 255 (黒) の値で、中間のピクセル値は灰色の網かけを表します。図 2 に示すのは、学習用セットの最初の画像 8 枚です。各画像に対応した実際の数値を識別するのは、人間には簡単ですが、コンピューターにとっては至難の業です。

## Azure Machine Learningとは
Microsoftが提供するクラウドサービスAzureの機能の一つで、ブラウザのみで機械学習のモデル作成、検証、デプロイまでが完結するサービスです。


## 使い方
### Azure Machine Learningの使い方

#### Microsoft Azure Machine Learning Studio にサインイン
https://studio.azureml.net
にアクセスすると
Microsoft Azure Machine Learning StudioのHome画面が表示されます。
![home](README.img/azureml_001-home.png)

水色の[Sign In]のボタンを押すとログインフォームが表示されます。


![loginform](README.img/azureml_002-loginform.png)

 ログインフォームにはAzureアカウントのメールアドレスを入力します。

![password](README.img/azureml_003-password.png)
入力したアカウントのパスワードを入力します。



#### WORKSPACEの作成
ログインが完了すると、以下のような画面になり、 my experimentsというボタンが現れます。

![login後](README.img/azureml_004-HomeAfterLogin.png)

はじめて、Microsoft Azure Machine Learning Portalにログインすると、自動的にFree-Workspaceというワークスペースが作成されます。

ワークスペースと言うのは、Azure Machine Learningの中で色々なモデル、データ・セットをまとめたプロジェクトのようなものと思って下さい。


ここに、Experimentsというものを作り機械学習のモデルを作って行きます。


#### Experimentsの作成

左下の「NEW」から「Blank Experiment」を選択s

![blank](README.img/azureml-blank.png)
 
#### 機械学習のモデルを作成する。

Saved Datasets / MNIST Train 60k 28x28 dense をドラッグ＆ドロップ

![60000](README.img/azureml-60000.png)

Machine Learning / Train / Train Model をドラッグ＆ドロップ

![train](README.img/azureml-train.png)

MNIST Train 60k 28x28 denseの下の点とTrain Modelの右上を線でつなげる

![60k-train](README.img/azureml-60k-train.png)

Machine Learning / Initialize Model / Classification / の

+ Multiclass Decision Forest
+ Multiclass Decision Jungle
+ Multiclass Logistic Regression
+ Multiclass Neural Network
 
上記4つの中から好きな物を選んでドラッグ＆ドロップ
Multiclass〜の下の点とTrain Modelの左上を線でつなげる

![60k-train](README.img/azureml-multi.png)

Train Modelをクリックし、右に出た「Launch column selector」を選択

![launch](README.img/azureml-launch.png)

空欄のところをクリックすると一番上に「Label」があるのでこれを選択  
`>`をクリックして`SELECTED COLUMNS`に移動  
`✔`で閉じる︎

![label](README.img/azureml-label.png)

Machine Learning / Initialize Model / Score / Score Model をドラッグ＆ドロップ
Train Modelの下の点とScore Modelの左上を線でつなげる

![score](README.img/azureml-score.png)

Saved Datasets / MNIST Test 10k 28x28 dense をドラッグ＆ドロップ
MNIST Test 10k 28x28 denseの下の点とScore Modelの右上を線でつなげる

![10k](README.img/azureml-10k.png)

Machine Learning / Evaluate / Evaluate Model をドラッグ＆ドロップ
Score Modelの下の点とEvaluate Modelの上の点どちらかを線でつなげる

![eva](README.img/azureml-eva.png)

下の「RUN」ボタンをクリック
RUNが終了したら（Evaluate Modelまでチェックマークがついたら）Evaluate Modelの下の点をクリック
Visualizeを選択すると結果が表示される

![visual](README.img/azureml-visual.png)

#### Web APIとして公開する準備

Web Service / Input と
Web Service / Output をドラッグ＆ドロップ

Inputの下の点とScore Modelの右上を線でつなげる  
Outputの上の点とScore Modelの下を線でつなげる  
下の方にあるフラスコマーク「Click to Swich to web service view」をクリック

![webservice-view](README.img/azureml-webservice-view.png)

（クリックすると、画像のように地球マークになる）

![webservice](README.img/azureml-webservice.png)

再度`RUN`をし、完了したら
下の「SET UP WEB SERVICE」の`Predictive Web Service [Recommended]`を選択

![setup web service button](README.img/azureml-setup-webservice-button.png)

もう一度`RUN`し、完了すると表示が`Training experiment`と`Predictive experiment`タブに分かれる

![experiment-tab](README.img/azureml-experiment-tab.png)

`Predictive experiment`タブを選択  
下の`DEPLOY WEB SERVICE`の`Deploy Web Service [Classic]`を選択

![deploy-webservice-button](README.img/azureml-deploy-webservice-button.png)
		
### Web API		
しばらくすると、下のような画面が開きます。
![Webservice Dashboard](README.img/azureml-webservice-dashboard.png)


この画面では、今作成したWeb APIの仕様を確認したり、テストしたりすることができます。

APIの仕様を確認すると、どのようなエンドポイントにアクセスし、
どのようなパラメータがあり、どのようなレスポンスが帰ってくるのかを確認する事ができます。


もし自分のアプリケーションに機械学習の機能を取り込むのであれば、このドキュメントを見ることになります。

ドキュメントの最後には、R, Python, C#でのサンプルコードも載っているので、参考にすることができます。

#### Web APIのテスト
WebAPIのテストもブラウザから簡単に行う事ができます。

`Default Endpoint`の`TEST`ボタンをクリックする事で、テスト用のフォームが開きます。
![テストダイアログ](README.img/azureml-test-form.png)

入力として必要な項目を入力し、チェックマークをクリックすると、APIに問い合わせをします。


## MNIST 確認用フォームの使い方

### AzureMLの情報を入力する

![AzureML MNIST 確認フォーム](README.img/azureml-mnist-form.png)
このようなページが開きます。

AzureMLのWeb Serviceから、POST先のURLととAPI KEYを入手します。

- API Key
![API Key](README.img/azureml-apikey.png)
- エンドポイント
![エンドポイント](README.img/azureml-endpoint.png)

上記二つの情報を確認フォームの0.Azure MLのAPI情報に入力
![Azure ML Web API の情報入力](README.img/azureml-APIInfomation.png)

### 手書きの文字を認識する。

- ペイント等で文字を書きます。
- 書いた文字をアップロードします。

![画像をアップロード](README.img/azureml-upload.png)

- アップロードされた画像はリサイズされます。
![画像のリサイズ](README.img/azureml-resize.png)

- 文字認識完了
![画像の認識](README.img/azureml-detect.png)


---

## MNIST 確認フォームのインストール
### インストール

#### VM

新しく仮想マシンを立ち上げ、SSHでログイン

```sh
$ sudo yum -y install httpd php php-mbstring php-gd git
$ git clone https://github.com/tottok-ug/azure-ml-mnist-test-web-ui.git
```


PHPの動くWebサーバのドキュメントルートに

public/配下の

+ img/
+ js/
+ css/
+ detect.php
+ index.html
+ upload.php

を入れておく。

#### docker

##### Requirements
[docker](https://docs.docker.com/engine/installation/)

##### To Use
```sh
./docker_run.sh
open http://localhost
```



## さいごに
この資料はAzure Machine Learningを使用して、機械学習を体験するためのハンズオン資料になります。

今日このハンズオンを受け、どこかでこのハンズオンを実施したいと思ったら、
資料および、確認用フォームのソースコードはgithubで公開されているので、使用してください。

https://github.com/tottok-ug/azure-ml-mnist-test-web-ui 

### 使用の条件

この資料を使うための条件は一つです。

1. 資料の鮮度を保つ事。

2017年11月現在 Azure Machine Learningはアップデートが頻繁にされており、資料と現状で操作や諸々の文言等差異が発生している可能性があります。

こちらについては、使用する前には必ず一度はご自身でお試しいただき、現状と資料との差異を確認してください。
もし、資料との差異が存在した場合には、修正しPullRequestを送ってください。



Version. 2017-11-24
