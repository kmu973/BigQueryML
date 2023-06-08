```SQL
CREATE OR REPLACE MODEL
  `logistic.iris_model` OPTIONS(MODEL_TYPE ='LOGISTIC_REG',
    INPUT_LABEL_COLS=['species'],
    AUTO_CLASS_WEIGHTS=TRUE ) AS
SELECT
  *
FROM
  `udemy-bgml.logistic.iris`
```

![image](https://github.com/kmu973/BigQueryML/assets/70645899/b2bd1956-b6ce-4d66-a001-e4e844f398f6)


```SQL
CREATE OR REPLACE MODEL
assignments.iris_model
OPTIONS(MODEL_TYPE = 'LOGISTIC_REG',
    INPUT_LABEL_COLS = ['species'],
    MAX_ITERATIONS = 50,
    LEARN_RATE_STRATEGY = 'LINE_SEARCH',
    EARLY_STOP = TRUE,
    DATA_SPLIT_METHOD = 'AUTO_SPLIT',
    CATEGORY_ENCODING_METHOD = 'ONE_HOT_ENCODING'
) AS
SELECT *
FROM `bq-ml-332311.assignments.iris`
```

![image](https://github.com/kmu973/BigQueryML/assets/70645899/4a3a7e1b-3550-4de5-adfe-3b8e708ee100)
