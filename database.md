## categories
|   カラム名    |  データ型   | NULL |  キー   | 初期値 | autoincrement |
| ------------- | ----------- | ---- | ------- | ------ | ------------- |
| id            | int         |      | PRIMARY |        | YES           |
| category_name | varchar(20) |      |         |        |               |

## channels
|   カラム名   |  データ型   | NULL |  キー   | 初期値 | autoincrement |
| ------------ | ----------- | ---- | ------- | ------ | ------------- |
| id           | int         |      | PRIMARY |        | YES           |
| channel_name | varchar(20) |      |         |        |               |

## programs
|    カラム名    |   データ型   | NULL |  キー   | 初期値 | autoincrement |     |
| -------------- | ------------ | ---- | ------- | ------ | ------------- | --- |
| id             | int          |      | PRIMARY |        |               | YES |
| program_title  | varchar(100) |      |         |        |               |     |
| program_detail | varchar(200) |      |         |        |               |     |
| category_id    | int          |      | FOREIGN |        |               |     |
| channel_id     | int          |      | FOREIGN |        |               |     |
- 外部キー制約:category_idに対して、categoriesテーブルのidカラムから設定
- 外部キー制約:channel_idに対して、channelsテーブルのidカラムから設定

## episodes

|    カラム名    |   データ型   | NULL |  キー   | 初期値 | autoincrement |
| -------------- | ------------ | ---- | ------- | ------ | ------------- |
| id             | int          |      | PRIMARY |        | YES           |
| episode_title  | varchar(100) |      |         |        |               |
| episode_detail | varchar(200) |      |         |        |               |
| video_time     | time         |      |         |        |               |
| open_day       | DATE         |      |         |        |               |
| see_number     | int          |      |         |        |               |
| episode_number | int          |      |         |        |               |
| program_id     | int          |      | FOREIGN |        |               |
| season_id      | int          |      | FOREIGN |        |               |
- 外部キー制約:season_idに対してseasonsテーブルのidカラムから設定

## time_slots
|  カラム名  | データ型 | NULL |  キー   | 初期値 | autoincrement |
| ---------- | -------- | ---- | ------- | ------ | ------------- |
| id         | int      |      | PRIMARY |        | YES           |
| start_time | DATETIME |      |         |        |               |
| end_time   | DATETIME |      |         |        |               |
| episode_id | int      |      | FOREIGN |        |               |
| channel_id | int      |      | FOREIGN |        |               |
- 外部キー制約:episode_idに対して、episodesテーブルのidカラムから設定
- 外部キー制約:channel_idに対して、channelsテーブルのidカラムから設定

## seasons
|   カラム名    | データ型 | NULL |  キー   | 初期値 | autoincrement |
| ------------- | -------- | ---- | ------- | ------ | ------------- |
| id            | int      |      | PRIMARY |        | YES           |
| season_number | int      |      |         |        |               |
| program_id    | int      |      | FOREIGN |        |               |
- 外部キー制約:program_idに対して、programsテーブルのidカラムから設定

## broadcasts
|   カラム名   | データ型 | NULL |  キー   | 初期値 | autoincrement |
| ------------ | -------- | ---- | ------- | ------ | ------------- |
| id           | int      |      | PRIMARY |        | YES           |
| episode_id   | int      |      | FOREIGN |        |               |
| time_slot_id | int      |      | FOREIGN |        |               |
- 外部キー制約:episode_idカラムはepisodesテーブルのepisode_idを参照
- 外部キー制約:time_slot_idカラムはtime_slotsテーブルのidを参照