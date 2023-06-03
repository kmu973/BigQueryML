# BigQueryML

[Model selection guied](https://cloud.google.com/bigquery/docs/bqml-introduction)

<img src="https://github.com/kmu973/BigQueryML/assets/70645899/9dd176b7-0c04-4e5f-a6ff-895582fb7e8c" width="500">

## Linear Regression

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
