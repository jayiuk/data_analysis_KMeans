#data_analysis by KMeans

##KMeans를 사용한 데이터 분석

###데이터 추출을 위해 작성한 쿼리
{
    SELECT T1.*, playcount_sum, playtime_sum, recent_date, mode
FROM(SELECT *
FROM( SELECT WID, COUNT(*)login_count, MAX(level)level
FROM project.raw_login_data GROUP BY 1))T1
INNER JOIN(
SELECT WID, MAX(date)recent_date, mode, SUM(play_count)playcount_sum, SUM(playtime)playtime_sum FROM project.daily_play
GROUP BY WID, mode)T2
ON T1.WID = T2.WID
}

