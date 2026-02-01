## detabase作成
- create database newprograms;

## 作成したデータベースを選択し、テーブルとカラムを作成
- use newprograms;
  - create table categories (id int auto_increment, category_name varchar(20), primary key(id));
  - create table channels (id int auto_increment, channel_name varchar(20), primary key(id));
  - create table programs (id int auto_increment, channel_id int, channel_id int, program_title varchar(100), program_detail varchar(200), primary key(id));
  - create table episodes (id int auto_increment, program_id int, season_id int, episode_title varchar(100), episode_detail varchar(200), video_time time, open_day date, see_number int, episode_number int primary key(id));
  - create table seasons (id int auto_increment, program_id int, season_number int primary key(id));
  - create table time_slots (id int auto_increment, episode_id int, channel_id int, start_time datetime, end_time datetime, primary key(id));
  - create table broadcasts (id int auto_increment, episode_id int, time_slot_id int, primary key(id));

 ## 外部キー設定方法
- xamppを使用しているため、mysqlのphpadminからGUIでリレーションという項目を使用し外部キーを設定
　※注意点としては、参照先にカラムがないと設定ができないため、あらかじめカラムを作成しておく
  - 外部キー設定方法は以下
    - 外部キーを設定したいテーブルを選択
    - 画面上部の構造という項目をクリック
    - リレーションビューをクリック
    - 左側のカラムでは外部キーを設定したいカラムを選択(参照元)
    - 外部キーの参照先のテーブルをプルダウンから選択
    - 左側のカラムでは外部キーの参照先のカラムをプルダウンから選択
    - 実行

## 外部キーを設定
- 外部キーを設定するテーブルは以下
### programs
|    カラム名    |   データ型   | NULL |  キー   | 初期値 | autoincrement |     |
| -------------- | ------------ | ---- | ------- | ------ | ------------- | --- |
| id             | int          |      | PRIMARY |        |               | YES |
| program_title  | varchar(100) |      |         |        |               |     |
| program_detail | varchar(200) |      |         |        |               |     |
| category_id    | int          |      | FOREIGN |        |               |     |
| channel_id     | int          |      | FOREIGN |        |               |     |
- 外部キー制約:category_idに対して、categoriesテーブルのidカラムから設定
- 外部キー制約:channel_idに対して、channelsテーブルのidカラムから設定

### episodes

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

### time_slots
|  カラム名  | データ型 | NULL |  キー   | 初期値 | autoincrement |
| ---------- | -------- | ---- | ------- | ------ | ------------- |
| id         | int      |      | PRIMARY |        | YES           |
| start_time | DATETIME |      |         |        |               |
| end_time   | DATETIME |      |         |        |               |
| episode_id | int      |      | FOREIGN |        |               |
| channel_id | int      |      | FOREIGN |        |               |
- 外部キー制約:episode_idに対して、episodesテーブルのidカラムから設定
- 外部キー制約:channel_idに対して、channelsテーブルのidカラムから設定

### seasons
|   カラム名    | データ型 | NULL |  キー   | 初期値 | autoincrement |
| ------------- | -------- | ---- | ------- | ------ | ------------- |
| id            | int      |      | PRIMARY |        | YES           |
| season_number | int      |      |         |        |               |
| program_id    | int      |      | FOREIGN |        |               |
- 外部キー制約:program_idに対して、programsテーブルのidカラムから設定

### broadcasts
|   カラム名   | データ型 | NULL |  キー   | 初期値 | autoincrement |
| ------------ | -------- | ---- | ------- | ------ | ------------- |
| id           | int      |      | PRIMARY |        | YES           |
| episode_id   | int      |      | FOREIGN |        |               |
| time_slot_id | int      |      | FOREIGN |        |               |
- 外部キー制約:episode_idカラムはepisodesテーブルのepisode_idを参照
- 外部キー制約:time_slot_idカラムはtime_slotsテーブルのidを参照

## 各テーブルにデータを挿入
- categoriesテーブル
  - insert into categories(category_name) values ('アニメ'), ('ドラマ'), ('映画'), ('ニュース'), ('スポーツ'), ('ペット');
- channelsテーブル
  - insert into channels (channel_name) values ('ドラマ1'), ('ドラマ2'), ('アニメ1'), ('アニメ2'), ('スポーツ'), ('ペット');
- programsテーブル
  - insert into programs (program_title, program_detail, category_id, channel_id) values ('君と過ごす季節', '高校生の恋愛と成長を描く青春ドラマ', 2, 1), ('都会の弁護士', '都会で活躍する弁護士の物語', 2, 2), ('ネコ王国の冒険', '猫たちが王国を救うファンタジーアニメ', 1, 3), ('ロボットヒーローX', '未来のロボットが世界を守るアニメ', 1, 4), ('プロ野球ダイジェスト', '最新のプロ野球情報を届ける', 5, 5), ('わんこライフ', '犬との暮らしを紹介する番組', 6, 6);
- episodesテーブル
  - INSERT INTO episodes (
    episode_title,
    episode_detail,
    video_time,
    open_day,
    see_number,
    episode_number,
    season_id,
    program_id
) VALUES
('出会いの春', '主人公たちの出会い', '00:45:00', '2025-04-01', 1200, 1, 1, 1),
('すれ違い', '誤解が生まれる', '00:45:00', '2025-04-08', 980, 2, 1, 2),
('告白', '気持ちを伝える', '00:45:00', '2025-04-15', 1500, 3, 1, 3),
('雨の日の約束', '二人の距離が縮まる', '00:45:00', '2025-04-22', 1100, 4, 1, 4),
('依頼人の嘘', '難事件の始まり', '00:50:00', '2025-05-01', 800, 1, 2, 5),
('法廷の攻防', '証言の矛盾', '00:50:00', '2025-05-08', 900, 2, 2, 6),
('逆転判決', '意外な結末', '00:50:00', '2025-05-15', 1300, 3, 2, 1),
('王国の危機', '敵の襲来', '00:25:00', '2025-06-01', 2000, 1, 3, 2),
('勇者ネコ誕生', '主人公の覚醒', '00:25:00', '2025-06-08', 2200, 2, 3, 3),
('仲間集結', '仲間が集まる', '00:25:00', '2025-06-15', 1800, 3, 3, 4),
('決戦前夜', '最終決戦前', '00:25:00', '2025-06-22', 2100, 4, 3, 5),
('起動', 'ロボット誕生', '00:30:00', '2025-07-01', 1700, 1, 4, 6),
('敵ロボット', '初戦闘', '00:30:00', '2025-07-08', 1600, 2, 4, 1),
('裏切り者', '仲間の裏切り', '00:30:00', '2025-07-15', 1900, 3, 4, 2),
('開幕戦特集', '開幕戦の振り返り', '00:20:00', '2025-03-25', 500, 1, 5, 3),
('注目選手', 'スター選手紹介', '00:20:00', '2025-04-01', 600, 2, 5, 4),
('名場面集', '名プレー集', '00:20:00', '2025-04-08', 700, 3, 5, 5),
('子犬の成長', '成長記録', '00:15:00', '2025-02-01', 300, 1, 6, 6),
('しつけ講座', '基本トレーニング', '00:15:00', '2025-02-08', 350, 2, 6, 1),
('ドッグラン', '犬の遊び場紹介', '00:15:00', '2025-02-15', 400, 3, 6, 2);
- seasonsテーブル
  - insert into seasons (season_number, program_id) values (1, 1), (2, 2), (3, 3), (1, 4), (3, 5), (2, 6);
- time_slotsテーブル
  - INSERT INTO time_slots (start_time, end_time, episode_id, channel_id) VALUES
('2026-01-29 21:00:00', '2026-01-29 21:45:00', 101, 1),
('2026-02-02 21:00:00', '2026-02-02 21:45:00', 102, 1),
('2026-02-02 21:00:00', '2026-02-02 21:45:00', 103, 1),
('2026-02-02 21:00:00', '2026-02-02 21:45:00', 104, 1),
('2026-03-05 22:00:00', '2026-03-05 22:50:00', 105, 2),
('2026-03-12 22:00:00', '2026-03-12 22:50:00', 106, 2),
('2026-03-19 22:00:00', '2026-03-19 22:50:00', 107, 2),
('2026-04-01 18:00:00', '2026-04-01 18:25:00', 108, 3),
('2026-04-08 18:00:00', '2026-04-08 18:25:00', 109, 3),
('2026-04-15 18:00:00', '2026-04-15 18:25:00', 110, 3),
('2026-05-01 18:00:00', '2026-05-01 18:25:00', 111, 3),
('2026-05-01 19:00:00', '2026-05-01 19:30:00', 112, 4),
('2026-05-08 19:00:00', '2026-05-08 19:30:00', 113, 4),
('2026-05-15 19:00:00', '2026-05-15 19:30:00', 114, 4),
('2026-05-22 20:00:00', '2026-05-22 20:20:00', 115, 5),
('2026-06-01 20:00:00', '2026-06-01 20:20:00', 116, 5),
('2026-06-08 20:00:00', '2026-06-08 20:20:00', 117, 5),
('2026-06-15 10:00:00', '2026-06-15 10:15:00', 118, 6),
('2026-06-22 10:00:00', '2026-06-22 10:15:00', 119, 6),
('2026-06-28 10:00:00', '2026-06-28 10:15:00', 120, 6);

- broadcastsテーブル
  - INSERT INTO broadcast (time_slot_id, episode_id)
VALUES
(21, 101),
(22, 102),
(23, 103),
(24, 104),
(25, 105),
(26, 106),
(27, 107),
(28, 108),
(29, 109),
(30, 110),
(31, 111),
(32, 112),
(33, 113),
(34, 114),
(35, 115),
(36, 116),
(37, 117),
(38, 118),
(39, 119),
(40, 120);