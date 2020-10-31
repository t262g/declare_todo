# テーブル設計

## users テーブル

| Column   | Type   | Options                   |
| -------- | ------ | ------------------------- |
| nickname | string | null: false               |
| email    | string | null: false, unique: true |
| password | string | null: false               |

### Association

- has_many :declarations
- has_many :cheers
- has_one :point
- has_many :follows

## declarations テーブル

| Column     | Type       | Options                        |
| ---------- | ---------- | ------------------------------ |
| content    | text       | null: false                    |
| expiration | integer    | null: false                    |
| user       | references | null: false, foreign_key: true |

### Association

- belongs_to :user
- has_many :cheers
- has_one :judge_declaration

## cheers テーブル

| Column      | Type       | Options                        |
| ----------- | ---------- | ------------------------------ |
| comment     | text       |                                |
| check       | integer    |                                |
| user        | references | null: false, foreign_key: true |
| declaration | references | null: false, foreign_key: true |

### Association

- belongs_to :user
- belongs_to :declaration
- has_one :judge_cheer

## judge_declarations テーブル

| Column      | Type       | Options                        |
| ----------- | ---------- | ------------------------------ |
| judge_point | integer    | null: false                    |
| declaration | references | null: false, foreign_key: true |

### Association

belongs_to :declaration
has_many :judge_cheers

## judge_cheers テーブル

| Column            | Type       | Options                        |
| ----------------- | ---------- | ------------------------------ |
| judge_point       | integer    | null: false                    |
| cheer             | references | null: false, foreign_key: true |
| judge_declaration | references | null: false, foreign_key: true |

### Association

belongs_to :cheer
belongs_to :judge_declaration

## Points テーブル

| Column            | Type       | Options                        |
| ----------------- | ---------- | ------------------------------ |
| declaration_point | integer    | null: false                    |
| cheer_point       | integer    | null: false                    |
| user              | references | null: false, foreign_key: true |

### Association

- belongs_to :user

## follows テーブル

| Column | Type       | Options                        |
| ------ | ---------- | ------------------------------ |
| user   | references | null: false, foreign_key: true |
| user   | references | null: false, foreign_key: true |

### Association

- belongs_to :user