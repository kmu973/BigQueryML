```SQL
-- select distinct bedrooms from `boosted_trees.housing`;

-- select * from `boosted_trees.housing` where bedrooms = 0
 
-- delete from `boosted_trees.housing` where bedrooms = 0

-- select distinct bedrooms from `boosted_trees.housing`

-- select * from `boosted_trees.housing` where bedrooms = 0

-- delete from `boosted_trees.housing` where bedrooms = 0

-- select count(*) from `boosted_trees.housing` where bedrooms = 33

-- select * from `boosted_trees.housing` where bedrooms = 33 
 
-- delete from `boosted_trees.housing` where bedrooms = 33

-- select distinct bathrooms from `boosted_trees.housing`

-- delete from `boosted_trees.housing` where bathrooms = 0
 
-- select * from `boosted_trees.housing` where bathrooms >= 6

-- select count(*) from  `bq-ml-332311.boosted_trees.housing` where yr_renovated = 0 or yr_built is null


CREATE OR REPLACE TABLE `xgboost.house_clean` AS SELECT
CAST (EXTRACT(MONTH FROM date) AS STRING) AS month,
bedrooms,
bathrooms,
sqft_living, 
sqft_lot,
floors,
cast(view as string) as view,
cast(waterfront as string) as waterfront,
cast(condition as string) as condition,
cast(grade as string) as grade,
sqft_above,
(EXTRACT(Year FROM date) - yr_built) as age_of_house,
cast( (case when yr_renovated = 0 then 0 else 1 end) as string) as renovated,
cast( (case when sqft_basement = 0 then 0 else 1 end) as string) as basement,
cast(zipcode as string) as zipcode,
lat, long, 
price/10000 as price

FROM
bq-ml-332311.xgboost.housing
```

```SQL
CREATE OR REPLACE MODEL boosted_tree.house_run1
OPTIONS
(model_type='BOOSTED_TREE_REGRESSOR',
input_label_cols=['price'], 
BOOSTER_TYPE='DART', 
TREE_METHOD='AUTO',
early_stop=False,
enable_global_explain = true
) AS
SELECT
*
FROM boosted_tree.house_clean

-- FEATURE_IMPORTANCE	
SELECT  *  FROM ML.FEATURE_IMPORTANCE(MODEL `bq-ml-332311.check.model_only_lat`) 

CREATE OR REPLACE MODEL
  boosted_tree.model_hyp_final OPTIONS (model_type='BOOSTED_TREE_REGRESSOR',
    input_label_cols=['price'],
    BOOSTER_TYPE='DART',
    TREE_METHOD='AUTO',
	early_stop=TRUE,
    enable_global_explain = TRUE,
    MAX_TREE_DEPTH = HPARAM_CANDIDATES ([3,
      5,
      7,
      9,
      15,
      25]),
    MIN_TREE_CHILD_WEIGHT= HPARAM_CANDIDATES ([1,
      3,
      5,
      7]),
    LEARN_RATE = HPARAM_RANGE (0,
      0.5),
    NUM_TRIALS = 30 ) AS
SELECT
  * EXCEPT( floors,
    renovated,
    basement)
FROM
  boosted_tree.housing_final


SELECT 100-AVG((ABS(predicted_price- price)/price)*100)
FROM ML.PREDICT(MODEL `bq-ml-332311.boosted_tree.model_hyp_final`,
(
SELECT
* 
FROM `bq-ml-332311._2be3b8f9f2386579dd939bcd3b6e9572859327bb.anon44dbcb37_d718_4410_969b_dc513ad0d9d4_imported_data_split_eval_data`
))
```
