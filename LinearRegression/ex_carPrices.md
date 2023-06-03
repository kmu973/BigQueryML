
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
