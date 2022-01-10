# 円に接する正多角形の面積と円の面積とを比較してまとめたい件


## 準備

  * ruby インストール

## 設定

  `setting.yml`に、書く. 下記がサンプル

  ```
  ---
  # 調べる最大の正多角形の角数
  max_n: 2000

  # 指定の角形まではスキップしない
  no_skip_until: 1500

  # スキップする数
  skip: 10

  # 結果を出力するファイルパス
  out_csv: out.csv
  ```
## 実行

コマンドプロンプトで、

```
rake
```