# BigQueryML

[Model selection guied](https://cloud.google.com/bigquery/docs/bqml-introduction)

<img src="https://github.com/kmu973/BigQueryML/assets/70645899/9dd176b7-0c04-4e5f-a6ff-895582fb7e8c" width="500">

```
spatial queries
https://cloud.google.com/bigquery/docs/reference/standard-sql/geography_functions

date queries
https://cloud.google.com/bigquery/docs/reference/standard-sql/date_functions

hyperparameter tuning
https://cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-hyperparameter-tuning

model export
https://cloud.google.com/bigquery/docs/exporting-models#export_model_formats_and_samples
```

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

tips
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

## Boosted trees

```
types 
- adaptive boosting
- gradient boosting
- XGBoost

tips
- no need to do feature selection but have to do feature engineering
```

[code](https://cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree)
```
{CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL} model_name
[OPTIONS(MODEL_TYPE = { 'BOOSTED_TREE_CLASSIFIER' | 'BOOSTED_TREE_REGRESSOR' },
         BOOSTER_TYPE = {'GBTREE' | 'DART'},
         NUM_PARALLEL_TREE = int64_value,
         DART_NORMALIZE_TYPE = {'TREE' | 'FOREST'},
         TREE_METHOD = {'AUTO' | 'EXACT' | 'APPROX' | 'HIST'},
         MIN_TREE_CHILD_WEIGHT = int64_value,
         COLSAMPLE_BYTREE = float64_value,
         COLSAMPLE_BYLEVEL = float64_value,
         COLSAMPLE_BYNODE = float64_value,
         MIN_SPLIT_LOSS = float64_value,
         MAX_TREE_DEPTH = int64_value,
         SUBSAMPLE = float64_value,
         AUTO_CLASS_WEIGHTS = { TRUE | FALSE },
         CLASS_WEIGHTS = struct_array,
         INSTANCE_WEIGHT_COL = string_value,
         L1_REG = float64_value,
         L2_REG = float64_value,
         EARLY_STOP = { TRUE | FALSE },
         LEARN_RATE = float64_value,
         INPUT_LABEL_COLS = string_array,
         MAX_ITERATIONS = int64_value,
         MIN_REL_PROGRESS = float64_value,
         DATA_SPLIT_METHOD = { 'AUTO_SPLIT' | 'RANDOM' | 'CUSTOM' | 'SEQ' | 'NO_SPLIT' },
         DATA_SPLIT_EVAL_FRACTION = float64_value,
         DATA_SPLIT_COL = string_value,
         ENABLE_GLOBAL_EXPLAIN = { TRUE | FALSE },
         XGBOOST_VERSION = { '0.9' | '1.1' }
)];
```



