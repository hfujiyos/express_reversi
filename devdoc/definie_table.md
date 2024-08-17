# テーブル定義書

| 項目           | システム情報                                             |
| :------------- | -------------------------------------------------------- |
| システム名     | nextjs-food-delivery                                     |
| サブシステム名 | nextjs-food-delivery-backend                             |
| URL            | http://localhost:1337/admin                              |
| GitHub         | https://github.com/hfujiyos/nextjs-food-delivery-backend |
| 備考           | Strapi（HeadlessCMS）                                    |

## restaurant（レストランコンテンツタイプ）

| No. | 論理名 | 物理名 | データ型 | 属性 | デフォルト | 備考 |
| :-- | ------ | ------ | -------- | ---- | ---------- | ---- |
| 1   | 23     | 3232   | 232      | 1232 | 2342       |

| No. | 論理名         | 物理名      | データ型  | 属性           | デフォルト | 備考 |
| :-- | -------------- | ----------- | --------- | -------------- | ---------- | ---- |
| 1   | レストラン名   | name        | Text      | Short text     |            |      |
| 2   | レストラン説明 | description | Rich text |                |            |      |
| 3   | レストラン画像 | image       | Media     | Multiple media |            |      |

|          | Marketer | Designer | Vue | React | Swift | Android | Flutter | PHP | Rails | Go  | AWS | GCP |
| :------: | -------- | -------- | --- | ----- | ----- | ------- | ------- | --- | ----- | --- | --- | --- |
| ｽｷﾙｱﾝｹｰﾄ | ー       | △        | △   | ◯     | ◯     | ー      | ー      | △   | ◯     | △   | ー  | ー  |
| ｽｷﾙｸｴｽﾄ  | ◯        | ◯        | ◯   | ◯     | ◯     | ー      | △       | ◯   | ◯     | △   | ◯   | ◯   |
|  登竜門  | ー       | ー       | ー  | ◯     | ー    | ー      | ー      | ー  | ー    | ー  | ー  | ー  |
| ｷｬﾘｱﾏｯﾌﾟ | ◯        | ◯        | ◯   | ◯     | ◯     | ◯       | ◯       | ◯   | ◯     | ◯   | ◯   | ◯   |

## dish（料理コンテンツタイプ）

| No. | 論理名             | 物理名      | データ型 | 属性         | デフォルト | 備考 |
| :-- | ------------------ | ----------- | -------- | ------------ | ---------- | ---- |
| 1   | 料理名             | name        | Text     | Short text   |            |      |
| 2   | 料理説明           | description | Text     | Long text    |            |      |
| 3   | 料理画像           | image       | Media    | Single media |            |      |
| 4   | 料理単価           | price       | Number   | integer      |            |      |
| 5   | 1 対多リレーション | restaurant  | Relation |              |            |      |

- Dish.restaurant（Restaurant has many Dishes）Restaurant.dishes
