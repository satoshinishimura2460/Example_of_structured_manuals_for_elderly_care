# Example_of_structured_manuals_for_elderly_care
介護の構造化マニュアルの例

## 構造化マニュアルとは
達成したい目的に向けて必要な行為とその関係を整理し、線や四角などの図形を用いて表現した業務手順書である。
例えば
<行為>：〔角の取れた長方形〕〔名詞+動詞〕の形式で記述する
<実行する人>：〔橙色の四角〕 配置：<行為>の左上
<目的が達成されるという関係>：〔縦線〕 配置：<行為>と<行為>の間
などの図形で表現する

## 介護における構造化マニュアルの例
右表に示す8種類の介護行為について，どの介護現場でも共通して頻出する行為をまとめ，構造化マニュアルとして記述したものである．  
英語名をExample of structured manuals for elderly careとする．  
公開するデータセット：  
* 介護における構造化マニュアルの例の一部（PDF）  
* 介護における構造化マニュアルの例（RDF）  

## 介護における構造化マニュアルの例（PDF）
介護における構造化マニュアルの例を図形表現で示したもの．
下図に一部を示す．

## 介護における構造化マニュアルの例（RDF）
介護における構造化マニュアルの例をResource Description Frameworkに則って記述したものである．
下図に一部を示す．

## データセットの作成過程（沿革）
[1][2]をもとに介護における構造化マニュアルの例を作成開始した．・・・A  
Aをもとに，医療法人社団aとの議論を通して，表現の改訂を行った．  
社会福祉法人bとの議論を通して，[3][4]を紹介された．  
Aと[3][4][5]及び当チームの介護専門家の経験をもとに，介護における構造化マニュアルの例の作成と改訂を行った．・・・B  
  排泄介助，入浴介助，食事介助，更衣介助，口腔ケア，移動介助，移乗介助，体位変換  
改訂した表現に合わせてBを改訂した．・・・C  
公開するデータセットはCである．  

参考文献

  [1] 平舘綾子: ホームヘルパー講座2級課程テキスト1福祉・介護の知識と方法, ニチイ学館(2012)，  
  [2] 平舘綾子: ホームヘルパー講座2級課程テキスト2介護の実際, ニチイ学館(2012)  
  [3] 大田仁史, 三好春樹: 完全図解　新しい介護, 講談社, 東田 勉(編集), (2014)  
  [4] 初任者研修テキストブック編集委員会(編集), 介護職員初任者研修テキスト,ミネルヴァ書房, (2016)  
  [5]社団法人日本介護福祉士養成施設協会, 介護福祉国家試験・実技試験免除のための介護技術講習テキスト, (2005)  

## データセットの作成過程（文献との関係）
参考文献に書かれたテキストから，行為と認定出来る箇所を抽出する．
抽出した箇所を，「名詞を動詞する」となるように短文に変換する．
変換された短文を行為ノードとして矩形で囲み，他の行為との関係を記述する．
抽出された行為ノードに対して，関連するリスクや詳細情報についての文章を抜き出す．
抜き出した文章を短文にし，矩形で囲み，当該行為ノードとの関係を記述する．
設定された目的に対して，参考文献に書かれた行為に関するテキストが不十分な場合は，介護の専門家が自分の知識に基づいて行為，リスク，詳細情報を追加する．

## 今後の更新予定
* 内容の更新
	* 必要に応じて不備のある内容を更新する．
	* その際には，行為ノードを始めとする全ての情報の追加，削除，変更を行う．
		* IRIの変更もあり得る．
		* データセットに対してバージョン番号を割り振る．
* スキーマの更新
	* 検索性の向上，より多くの内容を表現するために，スキーマを更新する．
	* その際には，Property, Classを追加，削除，変更を行う．

## （参考）SPARQLクエリ例
```
///ルートノード検索///  
  
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>  
PREFIX owl: <http://www.w3.org/2002/07/owl#>  
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>  
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>  
PREFIX sm: <http://coto.pj.aist.go.jp/ontologies/structured-manual/>  
PREFIX ont: <http://coto.pj.aist.go.jp/ontologies/structured-manual#>  
PREFIX act: <http://coto.pj.aist.go.jp/ontologies/structured-manual/Action/>  
  
SELECT * WHERE {  
  ?s a ont:Action.  
  
  filter not exists {  
    ?s ont:Achieve ?text.  
  }  
}  
  
  
///ある文字列(移乗)を含む行為の一覧///  
  
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>  
PREFIX owl: <http://www.w3.org/2002/07/owl#>  
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>  
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>  
PREFIX sm: <http://coto.pj.aist.go.jp/ontologies/structured-manual/>  
PREFIX ont: <http://coto.pj.aist.go.jp/ontologies/structured-manual#>  
PREFIX act: <http://coto.pj.aist.go.jp/ontologies/structured-manual/Action/>  
  
SELECT ?label WHERE {  
  ?action a ont:Action.  
  ?action rdfs:label ?label.  
  
  filter regex(?label, "移乗")  
}  
  
///順序関係がある方法とその方法で達成する目的///  
  
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>  
PREFIX owl: <http://www.w3.org/2002/07/owl#>  
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>  
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>  
PREFIX smp: <http://coto.pj.aist.go.jp/ontologies/structured-manual#>  
  
SELECT ?GoalLabel ?WayLabel  
	WHERE {  
		?Action a smp:Action.  
		?Action smp:Achieve ?Way.  
		?Way smp:Order ?Next.  
		?Action rdfs:label ?GoalLabel.  
		?Way rdfs:label ?WayLabel.  
		?Next rdfs:label ?NextLabel.  
}  
  
///利用者のする行為///  
  
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>  
PREFIX owl: <http://www.w3.org/2002/07/owl#>  
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>  
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>  
PREFIX smp: <http://coto.pj.aist.go.jp/ontologies/structured-manual#>  
  
SELECT ?ActionLabel  
	WHERE {  
		?Action a smp:Action.  
		?Action smp:hasActor ?Actor.  
		?Action rdfs:label ?ActionLabel.  
  
		filter regex(?Actor, "利用者")  
}  
```
