# suumo_scraping
## データソースURL
### 新大阪
https://suumo.jp/jj/bukken/ichiran/JJ010FJ001/?ar=060&bs=011&ra=060027&jspIdFlg=patternEki&rn=2000&rnek=200019130&kb=1&kt=9999999&mb=0&mt=9999999&ekTjCd=&ekTjNm=&tj=0&cnb=0&cn=9999999
### 大阪全域
https://suumo.jp/jj/bukken/ichiran/JJ012FC001/?ar=060&bs=011&cn=9999999&cnb=0&ekTjCd=&ekTjNm=&et=9999999&fw2=&kb=1&kt=9999999&mb=0&md=2&md=3&md=4&mt=9999999&sc=27102&sc=27103&sc=27104&sc=27106&sc=27107&sc=27108&sc=27109&sc=27111&sc=27113&sc=27114&sc=27115&sc=27116&sc=27117&sc=27118&sc=27119&sc=27120&sc=27121&sc=27122&sc=27123&sc=27124&sc=27125&sc=27126&sc=27127&sc=27128&scTemp=27102&scTemp=27103&scTemp=27104&scTemp=27106&scTemp=27107&scTemp=27108&scTemp=27109&scTemp=27111&scTemp=27113&scTemp=27114&scTemp=27115&scTemp=27116&scTemp=27117&scTemp=27118&scTemp=27119&scTemp=27120&scTemp=27121&scTemp=27122&scTemp=27123&scTemp=27124&scTemp=27125&scTemp=27126&scTemp=27127&scTemp=27128&ta=27&tj=0&po=0&pj=1&pc=100
    


# 以下コピー元
## 概要

suumo の中古マンション購入ページをスクレイピングして
差分があれば LINE に通知する Python コードです。

個人用途以外で利用しないでください。

## 動作環境

Windows Pro 20H2, Python 3.9.1

まぁそんな変なもの使ってないのであまりバージョンは気にせずで大丈夫かと

## 事前準備

### 設定ファイルをコピー

```shell
cp config.json.example config.json
```

### LINE Notify のアクセストークンを取得

1. LINE 通知用のグループを作成して、LINE Notify アカウントを招待する
1. なんかググって LINE Notify トークンを取得する
1. 取得したトークンを config.json の"line_notify_api"に貼り付ける

### suuumo で中古マンションを検索

1. https://suumo.jp/kanto/ にアクセスする
1. 中古マンション買うボタンを押す
1. 「エリアから探す」で適当な地域とか条件とかで検索する
1. 検索結果の URL を config.json の"result_url"に貼り付ける

### パッケージインストール

```python
pip install -r requirements.txt
```

これで事前準備は終了です。

## python 実行

```python
python get_property.py
```

## 結果確認

property.csv が生成され、各物件の情報が記載されている。

2 回目以降の python 実行で、物件情報に以下の差分があれば LINE に通知される。

- 追加
- 削除
- 価格

※ 掲載されなくなった物件は CSV からも削除されるので注意してください。

## ToDo

1. コードをきれいにする
1. 収集データの分析コードを追加する
1. 機能ごとに関数を分割(取得、読込、比較、etc...)
1. 重複物件の削除処理
1. アットホーム、ホームズ取得処理
