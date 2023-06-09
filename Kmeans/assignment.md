```SQL
CREATE MODEL
   `kmeans.iris_kmeans` OPTIONS ( MODEL_TYPE='KMEANS',
    num_trials = 6,
    num_clusters= HPARAM_RANGE(2,
      7),
    KMEANS_INIT_METHOD='RANDOM') AS
SELECT
   *
FROM
`udemy-bgml.logistic.iris`
```

```SQL
CREATE MODEL
  `kmeans.iris_kmeans2`
OPTIONS(MODEL_TYPE = 'KMEANS',
    NUM_CLUSTERS = 3,
    KMEANS_INIT_METHOD = 'RANDOM',
    DISTANCE_TYPE = 'EUCLIDEAN',
    MAX_ITERATIONS = 50,
    EARLY_STOP = FALSE)
    AS
SELECT
  *
FROM
  `udemy-bgml.logistic.iris`
 ```
