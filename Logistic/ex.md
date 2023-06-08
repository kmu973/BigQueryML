```SQL
SELECT Date, Location, WindGustDir, WindDir9am,	WindDir3pm, RainToday,	RainTomorrow,
safe_Cast(MinTemp as FLOAT64) as MinTemp,
safe_Cast(MaxTemp as FLOAT64) as MaxTemp,
safe_Cast(Rainfall as FLOAT64) as Rainfall,
safe_Cast(Evaporation as FLOAT64) as Evaporation,
safe_Cast(Sunshine as FLOAT64) as Sunshine,
safe_Cast(WindGustSpeed as FLOAT64) as WindGustSpeed,
safe_Cast(WindSpeed9am as FLOAT64) as WindSpeed9am,
safe_Cast(WindSpeed3pm as FLOAT64) as WindSpeed3pm,
safe_Cast(Humidity9am as FLOAT64) as Humidity9am,
safe_Cast(Humidity3pm as FLOAT64) as Humidity3pm,
safe_Cast(Pressure9am as FLOAT64) as Pressure9am,
safe_Cast(Pressure3pm as FLOAT64) as Pressure3pm,
safe_Cast(Cloud9am as FLOAT64) as Cloud9am,
safe_Cast(Cloud3pm as FLOAT64) as Cloud3pm,
safe_Cast(Temp9am as FLOAT64) as Temp9am,
safe_Cast(Temp3pm as FLOAT64) as Temp3pm
FROM `bq-ml-332311.regression.weather_train`

SELECT count(*), RainTomorrow FROM `bq-ml-332311.logistic.weather_train_final` group by RainTomorrow

CREATE OR REPLACE MODEL regression.weather_prediction
OPTIONS(MODEL_TYPE='logistic_reg',
    INPUT_LABEL_COLS=['RainTomorrow'],
  AUTO_CLASS_WEIGHTS=True, 
  enable_global_explain = TRUE) AS
SELECT *
FROM `bq-ml-332311.logistic.weather_train_final` where RainTomorrow != 'NA'

SELECT *
FROM ML.EVALUATE(MODEL `regression.weather_prediction`, TABLE `bq-ml-332311._2be3b8f9f2386579dd939bcd3b6e9572859327bb.anon8689051a_8b8f_44ed_87eb_984cc7ebd245_imported_data_split_eval_data` , STRUCT(0.55 AS threshold))

SELECT *
FROM ML.ROC_CURVE (MODEL `regression.weather_prediction`, TABLE `bq-ml-332311._2be3b8f9f2386579dd939bcd3b6e9572859327bb.anone94e23b8_d235_43d4_9dc6_f85d4a918e69_imported_data_split_eval_data`,GENERATE_ARRAY(0.4,0.6,0.01) )

SELECT
  recall,
  true_positives / (true_positives + false_positives) AS precision FROM ML.ROC_CURVE (MODEL `regression.weather_predict1`, TABLE `bq-ml-332311._2be3b8f9f2386579dd939bcd3b6e9572859327bb.anone94e23b8_d235_43d4_9dc6_f85d4a918e69_imported_data_split_eval_data`,GENERATE_ARRAY(0.4,0.6,0.01) )
  
SELECT *
FROM ML.CONFUSION_MATRIX (MODEL `regression.weather_prediction`, TABLE `bq-ml-332311._2be3b8f9f2386579dd939bcd3b6e9572859327bb.anoneeb473f4_7143_43e9_ad34_261f1e896633_imported_data_split_training_data` , STRUCT(0.55 AS threshold))

SELECT * 
FROM ML.PREDICT(MODEL `regression.weather_prediction`, TABLE `bq-ml-332311._2be3b8f9f2386579dd939bcd3b6e9572859327bb.anoneeb473f4_7143_43e9_ad34_261f1e896633_imported_data_split_training_data` , STRUCT(0.45 AS threshold))
  
SELECT *
FROM ML.GLOBAL_EXPLAIN(MODEL `regression.weather_prediction`, STRUCT(TRUE AS class_level_explain))
```
