# BigQueryML

[Model selection guied](https://cloud.google.com/bigquery/docs/bqml-introduction)

<img src="https://github.com/kmu973/BigQueryML/assets/70645899/9dd176b7-0c04-4e5f-a6ff-895582fb7e8c" width="500">

## Linear Regression

[code](https://cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm)

```SQL
{CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL}
model_name
[OPTIONS(MODEL_TYPE = { 'LINEAR_REG' | 'LOGISTIC_REG' },
    INPUT_LABEL_COLS = string_array,
    OPTIMIZE_STRATEGY = { 'AUTO_STRATEGY' | 'BATCH_GRADIENT_DESCENT' | 'NORMAL_EQUATION' },
    L1_REG = float64_value,
    L2_REG = float64_value,
    MAX_ITERATIONS = int64_value,
    LEARN_RATE_STRATEGY = { 'LINE_SEARCH' | 'CONSTANT' },
    LEARN_RATE = float64_value,
    EARLY_STOP = { TRUE | FALSE },
    MIN_REL_PROGRESS = float64_value,
    DATA_SPLIT_METHOD = { 'AUTO_SPLIT' | 'RANDOM' | 'CUSTOM' | 'SEQ' | 'NO_SPLIT' },
    DATA_SPLIT_EVAL_FRACTION = float64_value,
    DATA_SPLIT_COL = string_value,
    LS_INIT_LEARN_RATE = float64_value,
    WARM_START = { TRUE | FALSE },
    AUTO_CLASS_WEIGHTS = { TRUE | FALSE },
    CLASS_WEIGHTS = struct_array,
    ENABLE_GLOBAL_EXPLAIN = { TRUE | FALSE },
    CALCULATE_P_VALUES = { TRUE | FALSE },
    FIT_INTERCEPT = { TRUE | FALSE },
    CATEGORY_ENCODING_METHOD = { 'ONE_HOT_ENCODING`, 'DUMMY_ENCODING' }
)];
```
## Logistic Regression

## K-means clusturing

```
limitations
- applicable to only numerical attributes
- not perform well when clusters are varying sizes and density
- needs clipping of the outliers

notes
- anormally detection
```
[code](https://cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans)

```SQL
{CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL}
model_name
[OPTIONS(MODEL_TYPE = { 'KMEANS' },
    NUM_CLUSTERS = int64_value,
    KMEANS_INIT_METHOD = { 'RANDOM' | 'KMEANS++' | 'CUSTOM' },
    KMEANS_INIT_COL = string_value,
    DISTANCE_TYPE = { 'EUCLIDEAN' | 'COSINE' },
    STANDARDIZE_FEATURES = { TRUE | FALSE },
    MAX_ITERATIONS = int64_value,
    EARLY_STOP = { TRUE | FALSE },
    MIN_REL_PROGRESS = float64_value,
    WARM_START = { TRUE | FALSE }
)];
```
