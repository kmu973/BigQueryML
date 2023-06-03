# first model

<img src="https://github.com/kmu973/BigQueryML/assets/70645899/98e25b41-9849-44f9-b8d6-0f894896fde2" width="500">

```
CREATE OR REPLACE MODEL
  `udemy-bgml.regression.car_price` 
OPTIONS(model_type = 'linear_reg', input_label_cols = ['price']) AS 
SELECT CarName, fueltype, aspiration, doornumber, carbody, drivewheel, 
  enginelocation, wheelbase, carlength, carwidth, carheight, curbweight, 
  enginetype, cylindernumber, enginesize, fuelsystem, boreratio, stroke, 
  compressionratio, horsepower, peakrpm, citympg, highwaympg, price 
FROM `regression.car_price_data`
```


# second model

<img src="https://github.com/kmu973/BigQueryML/assets/70645899/a70b5bec-cc92-421b-8100-da784de3a1fc" width="500">

```SQL
CREATE MODEL IF NOT EXISTS
assignments.car_model
OPTIONS(MODEL_TYPE = 'LINEAR_REG',
    INPUT_LABEL_COLS = ['price'],
    OPTIMIZE_STRATEGY = 'AUTO_STRATEGY',
    MAX_ITERATIONS = 50,
    LEARN_RATE_STRATEGY = 'LINE_SEARCH',
    EARLY_STOP = TRUE,
    DATA_SPLIT_METHOD = 'AUTO_SPLIT',
    CATEGORY_ENCODING_METHOD = 'ONE_HOT_ENCODING'
) AS
SELECT 
symboling,
fueltype,
aspiration, 
doornumber, 
carbody,    
drivewheel, 
enginelocation, 
wheelbase,  
carlength,  
carwidth,   
carheight,  
curbweight, 
enginetype, 
cylindernumber, 
enginesize, 
fuelsystem, 
boreratio,  
stroke, 
compressionratio,   
horsepower, 
peakrpm,    
citympg,    
highwaympg, 
price
FROM `bq-ml-332311.assignments.car`

-- Calculate accuracy

SELECT 100-AVG((ABS(predicted_price -price)/price) *100) FROM ML.PREDICT (MODEL `assignments.car_model`,( SELECT * FROM `bq-ml-332311.assignments.car`))
```
