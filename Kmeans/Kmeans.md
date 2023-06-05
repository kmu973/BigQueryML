```SQL
CREATE OR REPLACE MODEL
  `clustering.bike_trips_run2` TRANSFORM( start_station_name,
    end_station_name,
    subscriber_type,
    duration_minutes,
    CAST(EXTRACT(hour
      FROM
        start_time) AS string) AS ride_hour) OPTIONS(model_type='kmeans',
      num_trials = 6,
      num_clusters= HPARAM_RANGE(2,
        7),
      kmeans_init_method='kmeans++',
      distance_type='cosine',
      min_rel_progress=0.005) AS
  SELECT
    start_time,
    start_station_name,
    end_station_name,
    subscriber_type,
    duration_minutes,
  FROM
    `bigquery-public-data.austin_bikeshare.bikeshare_trips`


SELECT * FROM ML.PREDICT (MODEL `clustering.bike_trips_run2`, TABLE `bigquery-public-data.austin_bikeshare.bikeshare_trips`)

select avg(duration_minutes) as duration_minutes, centroid_id from `clustering.results_temp_bike_cos` group by centroid_id

SELECT * FROM ML.CENTROIDS(MODEL `clustering.bike_trips_run2`)

select * from (SELECT * FROM ML.DETECT_ANOMALIES (MODEL `clustering.bike_trips_run2`, STRUCT (0.2 as contamination), TABLE `bigquery-public-data.austin_bikeshare.bikeshare_trips`)) where is_anomaly is true
```
