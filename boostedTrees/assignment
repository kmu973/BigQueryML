```SQL
CREATE OR REPLACE MODEL
  XGboost.seeds_model OPTIONS (model_type='BOOSTED_TREE_CLASSIFIER',
    input_label_cols=['type'],
    BOOSTER_TYPE='DART',
    learn_rate=0.2,
    early_stop=FALSE,
    DART_NORMALIZE_TYPE='FOREST',
    TREE_METHOD='EXACT',
    l2_reg=1.5,
    MIN_SPLIT_LOSS=0.5,
    MAX_TREE_DEPTH=9,
    MIN_TREE_CHILD_WEIGHT=2,
    enable_global_explain = TRUE ) AS
SELECT
  *
FROM
  XGboost.seeds
```
