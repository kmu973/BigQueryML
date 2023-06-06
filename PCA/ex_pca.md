```

CREATE OR REPLACE MODEL `pca.wine_model` OPTIONS (MODEL_TYPE='PCA', NUM_PRINCIPAL_COMPONENTS=3) AS SELECT * EXCEPT(id, target) FROM `pca.wine`

SELECT * FROM ML.EVALUATE (MODEL `bq-ml-332311.pca.wine_model`)

SELECT
  *
FROM
  ML.PREDICT (MODEL `bq-ml-332311.pca.wine_model`,
    (
    SELECT
      * EXCEPT (id
        )
    FROM
      `pca.wine`),
    STRUCT (TRUE AS KEEP_ORIGINAL_COLUMNS))

--without PCA

CREATE OR REPLACE MODEL pca.wine_without_pca
OPTIONS(MODEL_TYPE = 'BOOSTED_TREE_CLASSIFIER',
         DATA_SPLIT_METHOD = 'AUTO_SPLIT',
         BOOSTER_TYPE = 'GBTREE',
        MAX_ITERATIONS = 50,
        TREE_METHOD = 'HIST',
        INPUT_LABEL_COLS = ['target']
)
AS
SELECT * FROM `bq-ml-332311.pca.wine`

-- with PCA
CREATE OR REPLACE MODEL pca.wine_with_pca
OPTIONS(MODEL_TYPE = 'BOOSTED_TREE_CLASSIFIER',
         DATA_SPLIT_METHOD = 'AUTO_SPLIT',
         BOOSTER_TYPE = 'GBTREE',
        MAX_ITERATIONS = 50,
        TREE_METHOD = 'HIST',
        INPUT_LABEL_COLS = ['target']
)
AS
SELECT principal_component_1,principal_component_2,principal_component_3,target FROM `bq-ml-332311.pca.wine_new`
```
