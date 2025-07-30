- 신규 컬럼 생성
```scala
val minTempsByStationF = minTempsByStation  
.withColumn("temperature", round($"min(temperature)" * 0.1f * (9.0f / 5.0f) + 32.0f, 2))  
.select("stationID", "temperature").sort("temperature")
```