# README

# アプリケーション名
usedbook SFT

# アプリケーションの概要
大学で使う教科書がオンラインで安価に購入でき、かつそのお金を寄付できるというサービスです。会員登録をすれば誰でも本を出品・購入する事ができます。この本の売り上げの7割が海外の学校建設などの寄付にあてられます。

# URL

# テスト用アカウント
購入者用
メールアドレス: @gmail.com
パスワード: 
購入用カード情報
番号：4242424242424242
期限：3月25年
セキュリティコード：123
出品者用
メールアドレス名: @gmail.com
パスワード: 

# 利用方法
WebブラウザGoogle Chromeの最新版を利用してアクセスしてください。
ただしデプロイ等で接続できないタイミングもございます。その際は少し時間をおいてから接続してください。
接続先およびログイン情報については、上記の通りです。
同時に複数の方がログインしている場合に、ログインできない可能性があります。
テストアカウントでログイン→トップページから出品ボタン押下→商品情報入力→商品出品
確認後、ログアウト処理をお願いします。

# 目指した課題解決
教科書を安価に購入したいと思う大学生と勉強がしたいと願う海外の子供達の双方の課題を解決することを目的としています。

# 洗い出した要件
| 優先順位           | 機能             | 目的               | 詳細                       | ストーリー                             | 見積もり |
| (高:3、中:2、低:1) |                  |                    |                            |                                        |          |
| ------------------ | ---------------- | ------------------ | -------------------------- | -------------------------------------- | -------- |
| 3                  | ユーザー管理機能 | ユーザーが会員     | ユーザーの名前や住所などの | トップページから新規登録をクリックして | 2        |
|                    |                  | 登録するため       | 情報を登録する             | 必要な情報を入力する                   |          |
| 3                  | 商品出品機能     | ユーザーが本を     | 出品したい本の題名や販売価 | 会員登録したユーザーは出品ボタンをクリ | 9        |
|                    |                  | 出品するため       | 格などの情報を入力して出品 | ックして必要な情報を入力する           |          |
|                    |                  |                    | をする                     |                                        |          |
| 3                  | 商品一覧表示機能 | ユーザーが出品     | 出品された本が全て表示され | 全てのユーザーはトップページで本の一覧 | 2        |
|                    |                  | された本を見るため | る                         | を見る事ができる                       |          |
| 3                  | 商品詳細表示機能 | ユーザーが出品され | 本の題名や状態、カテゴリー | 全てのユーザーは一覧表示されている本を | 2        |
|                    |                  | た本の詳細情報を知 | といった詳細が表示される   | クリックして本の詳細情報を見る         |          |
|                    |                  | るため             |                            |                                        |          |
| 3                  | 商品情報編集機能 | 出品したユーザーが | 商品を出品したユーザーはい | 会員登録したユーザーは詳細ページから編 | 2        |
|                    |                  | 商品情報を編集する | つでも販売価格などの詳細情 | 集ボタンをクリックし商品の情報を編集す |          |
|                    |                  | ため               | 報を編集できる             | る                                     |          |
| 3                  | 商品情報削除機能 | 出品したユーザーが | 商品を出品したユーザーはい | 会員登録したユーザーは詳細ページから削 | 2        |
|                    |                  | 商品情報を削除する | つでも出品した商品を削除で | 除ボタンをクリックし商品を削除する     |          |
|                    |                  | ため               | きる                       |                                        |          |
| 3                  | 商品購入機能     | ユーザーが本を購入 | ユーザーがクレジットカード | 会員登録したユーザーは詳細ページから購 | 4        |
|                    |                  | するため           | の情報を入力することで本を | 入ボタンをクリックしカード情報を入力し |          |
|                    |                  |                    | 購入できる                 | て購入する                             |          |

# 実装した機能についてのGIFと説明


# 実装予定の機能

# データベース設計
## users テーブル

| Column                | Type    | Options     |
| --------------------- | ------- | ----------- |
| nickname              | string  | null: false |
| email                 | string  | null: false |
| encrypted_password    | string  | null: false |
| familyname_kana       | string  | null: false |
| firstname_kana        | string  | null: false |
| familyname_kata       | string  | null: false |
| firstname_kata        | string  | null: false |
| birthday              | date    | null: false |

### Asociation
- has_many :books
- has_many :orders
- has_one :address

## books テーブル

| Column           | Type       | Options                        |
| ---------------- | ---------- | ------------------------------ |
| name             | string     | null: false                    |
| description      | text       | null: false                    |
| category_id      | integer    | null: false                    |
| condition_id     | integer    | null: false                    |
| shipping_fee_id  | integer    | null: false                    | 
| prefecture_id    | integer    | null: false                    | 
| shipping_day_id  | integer    | null: false                    | 
| price            | integer    | null: false                    |
| user             | references | null: false, foreing_key: true |

### Asociation
- belongs_to :user
- has_one :order
- belongs_to_active_hash :category
- belongs_to_active_hash :condition
- belongs_to_active_hash :shipping_fee_id
- belongs_to_active_hash :prefecture_id
- belongs_to_active_hash :shipping_day_id


## orders テーブル

| Column           | Type       | Options                        |
| ---------------- | ---------- |------------------------------- | 
| user             | references | null: false, foreing_key: true |
| book             | references | null: false, foreing_key: true |

### Asociation
- belongs_to :book
- belongs_to :user


## addresses テーブル

| Column        | Type       | Options                     |
| ------------  | -------    | -----------                 |
| postal_code   | string     | null: false                 |
| prefecture_id | integer    | null: false                 |
| city          | string     | null: false                 |
| address_line  | string     | null: false                 |
| building      | string     |                             |
| phone_number  | string     | null: false                 |
| user          | references |                             |

### Asociation
- belongs_to :user
- belongs_to_active_hash :prefecture_id

# ローカルでの動作方法
ruby 6.0.0