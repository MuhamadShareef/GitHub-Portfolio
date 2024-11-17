-- 02- Data Exploration.sql 

-- checking the data types of all columns 

SELECT 
  table_name,
  column_name,
  data_type,
  is_nullable
FROM 
  `leafy-sanctuary-412122.cyclistic_data.INFORMATION_SCHEMA.COLUMNS`
WHERE 
  table_name 
  LIKE 'cyclistic_data_2019%'


-- Counting NULL values for each column in the table

SELECT 
  COUNT(*) - COUNT(ride_id) AS ride_id_nulls,
  COUNT(*) - COUNT(rideable_type) AS rideable_type_nulls,
  COUNT(*) - COUNT(started_at) AS started_at_nulls,
  COUNT(*) - COUNT(ended_at) AS ended_at_nulls,
  COUNT(*) - COUNT(start_station_name) AS start_station_name_nulls,
  COUNT(*) - COUNT(start_station_id) AS start_station_id_nulls,
  COUNT(*) - COUNT(end_station_name) AS end_station_name_nulls,
  COUNT(*) - COUNT(end_station_id) AS end_station_id_nulls,
  COUNT(*) - COUNT(start_lat) AS start_lat_nulls,
  COUNT(*) - COUNT(start_lng) AS start_lng_nulls,
  COUNT(*) - COUNT(end_lat) AS end_lat_nulls,
  COUNT(*) - COUNT(end_lng) AS end_lng_nulls,
  COUNT(*) - COUNT(member_casual) AS member_casual_nulls
FROM `leafy-sanctuary-412122.cyclistic_data.cyclistic_data_2019_merged`


-- Remove rows with NULL values in key columns


SELECT 
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual
FROM `leafy-sanctuary-412122.cyclistic_data.cyclistic_data_2019_merged`
WHERE ride_id IS NOT NULL
  AND rideable_type IS NOT NULL
  AND started_at IS NOT NULL
  AND ended_at IS NOT NULL
  AND start_station_name IS NOT NULL
  AND start_station_id IS NOT NULL
  AND end_station_name IS NOT NULL
  AND end_station_id IS NOT NULL
  AND start_lat IS NOT NULL
  AND start_lng IS NOT NULL
  AND end_lat IS NOT NULL
  AND end_lng IS NOT NULL
  AND member_casual IS NOT NULL


-- Checking for duplicate rows

SELECT 
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual,
  COUNT(*) AS duplicate_count
FROM `leafy-sanctuary-412122.cyclistic_data.cyclistic_data_2019_merged`
GROUP BY 
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual
HAVING COUNT(*) > 1    -- There are no duplicated rows


-- Checking if all ride_id values have the same length

SELECT 
  LENGTH(ride_id) AS ride_id_length,
  COUNT(*) AS count
FROM `leafy-sanctuary-412122.cyclistic_data.cyclistic_data_2019_merged`
GROUP BY LENGTH(ride_id)
ORDER BY ride_id_length;


-- Checking for unique types in rideable_type

SELECT 
  rideable_type,
  COUNT(*) AS count
FROM `leafy-sanctuary-412122.cyclistic_data.cyclistic_data_2019_merged`
GROUP BY rideable_type
ORDER BY count DESC;








