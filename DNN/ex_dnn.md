```SQL
select distinct activity from `bq-ml-332311.dnn.har`

CREATE OR REPLACE MODEL dnn.run1
OPTIONS
    (model_type='DNN_CLASSIFIER',
    input_label_cols=['activity'], 
    HIDDEN_UNITS=HPARAM_CANDIDATES([STRUCT([32,64,128]), STRUCT([32,64])]),
    DROPOUT=HPARAM_RANGE(0,0.8),
    BATCH_SIZE = 32,
    NUM_TRIALS = 10,
    EARLY_STOP = TRUE,
    OPTIMIZER = 'ADAM'
    ) AS

SELECT * FROM `bq-ml-332311.dnn.har`

```
