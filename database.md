## programs
|    カラム名    |   データ型   | NULL |  キー   | 初期値 | autoincrement |
| -------------- | ------------ | ---- | ------- | ------ | ------------- |
| title          | varchar(50)  |      |         |        |               |
| program_id     | int          |      | PRIMARY |        | YES           |
| program_detail | varchar(200) |      |         |        |               |
| category       | varchar(20)  |      |         |        |               |

## channels

|   カラム名   |  データ型   | NULL |  キー   | 初期値 | autoincrement |
| ------------ | ----------- | ---- | ------- | ------ | ------------- |
| channel_name | varchar(20) |      |         |        |               |
| program_id   | int         |      |         |        | YES           |
| channel_id   | int         |      | PRIMARY |        | YES           |


## series
|   カラム名    |  データ型   | NULL |  キー   | 初期値 | autoincrement |
| ------------- | ----------- | ---- | ------- | ------ | ------------- |
| season_number | varchar(10) | YES  | PRIMARY |        |               |
| season        | varchar(10) |      |         |        |               |
| program_id    | int         |      | PRIMARY |        | YES           |


## episodes

|    カラム名    |   データ型   | NULL |  キー   | 初期値 | autoincrement |
| -------------- | ------------ | ---- | ------- | ------ | ------------- |
| season_number  | int          | YES  |         |        |               |
| episode_number | int          |      | PRIMARY |        | YES           |
| title          | varchar(50)  |      |         |        |               |
| episode_detail | varchar(200) |      |         |        |               |
| video_time     | date         |      |         |        |               |
| open_day       | date         |      |         |        |               |
| program_id     | int          |      | PRIMARY |        | YES           |
| see_number     | int          |      |         |        |               |

## kpi

|  カラム名  | データ型 | NULL |  キー   | 初期値 | autoincrement |
| ---------- | -------- | ---- | ------- | ------ | ------------- |
| program_id | int      |      | PRIMARY |        | YES           |
| channel_id | int      |      | PRIMARY |        |               |
| see_number | int      |      |         |        |               |

## program_frams
|  カラム名  | データ型 | NULL |  キー   | 初期値 | autoincrement |
| ---------- | -------- | ---- | ------- | ------ | ------------- |
| channel_id | int      |      | PRIMARY |        | YES           |
| start_time | time     |      |         |        |               |
| end_time   | time     |      |         |        |               |
