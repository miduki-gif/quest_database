## エピソード視聴数トップ3のエピソードタイトルと視聴数を取得
- select id, episode_detail, see_number from episodes order by see_number desc limit 3;

## エピソード視聴数トップ3の番組タイトル、シーズン数、エピソード数、エピソードタイトル、視聴数を取得
- select * from time_slots inner join episodes on time_slots.episode_id = episodes.id inner join channels on time_slots.channel_id = channels.id inner join programs on episodes.program_id = programs.id inner join seasons on episodes.season_id = seasons.id order by see_number desc limit 3;

## 本日の番組表を表示するために、本日、どのチャンネルの、何時から、何の番組が放送されるのかを知りたいです。本日放送される全ての番組に対して、チャンネル名、放送開始時刻(日付+時間)、放送終了時刻、シーズン数、エピソード数、エピソードタイトル、エピソード詳細を取得
- select * from broadcasts b join time_slots ts on b.time_slot_id = ts.id join episodes e on b.episode_id = e.id join channels c on ts.channel_id = c.id join programs p on e.program_id = p.id where date(start_time) = curdate();

## ドラマというチャンネルがあったとして、ドラマのチャンネルの番組表を表示するために、本日から一週間分、何日の何時から何の番組が放送されるのかを知りたいです。ドラマのチャンネルに対して、放送開始時刻、放送終了時刻、シーズン数、エピソード数、エピソードタイトル、エピソード詳細を本日から一週間分取得
- select * from broadcasts b join time_slots ts on b.time_slot_id = ts.id join episodes e on b.episode_id = e.id join channels c on ts.channel_id = c.id join programs p on e.program_id = p.id where date(start_time) between curdate() and date_add(curdate(), interval 6 day);