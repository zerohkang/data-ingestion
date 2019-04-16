# spark bonus 09231 younghun knag 강영훈

## Bonus Exercise
If you have more time, attempt the following extra bonus exercise:
Another common part of the ETL process is data scrubbing. In this bonus exercise, you will process data in order to get it into a standardized format for later processing.

Review the contents of the file $DEVDATA/devicestatus.txt. This file contains data collected from mobile devices on Loudacre’s network, including device ID, current status, location, and so on. Because Loudacre previously acquired other mobile providers’ networks, the data from different subnetworks has a different format. Note that the records in this file have different field delimiters: some use commas, some use pipes (|), and so on. Your task is the following:

A. Upload the devicestatus.txt file to HDFS.

Ans. 
 #"/loudacre/devicestatus.txt" 파일 로드
 devstatRDD = sc.textFile("/loudacre/devicestatus.txt")

B. Determine which delimiter to use (hint: the character at position 19 is the first use of the delimiter).

Ans.
 #19번 밸류 이상인 값 필터링 및 19밸류 기준 split
 ftRDD = devstatRDD.filter(lambda line: len(line) > 20)
 splitRDD = ftRDD.map(lambda line: line.split(line[19:20]))

C. Filter out any records which do not parse correctly (hint: each record should have exactly 14 values).

Ans.
 #14개의 밸류를 가진 것만 필터링
 CorrectRDD = splitRDD.filter(lambda values: len(values) == 14)

D. Extract the date (first field), model (second field), device ID (third field), and latitude and longitude (13th and 14th fields respectively).

Ans.
 #date, model, deviceID, latitude, longitude 만출력
 resultRDD = CorrectRDD.map(lambda values: (values[0], values[1], values[2], values[12], values[13]))

E. The second field contains the device manufacturer and model name (such as Ronin S2). Split this field by spaces to separate the manufacturer from the model (for example, manufacturer Ronin, model S2). Keep just the manufacturer name.

Ans.
 #모델에서 제조사만 표시
 resultRDD = CorrectRDD.map(lambda values: (values[0], values[1].split(' ')[0], values[2], values[12], values[13]))

F. Save the extracted data to comma-delimited text files in the /loudacre/devicestatus_etl directory on HDFS.

Ans.
 #, Delimiter로 텍스트 파일 저장
 resultRDD = CorrectRDD.map(lambda values: (values[0], values[1].split(' ')[0], values[2], values[12], values[13]))

G. Confirm that the data in the file(s) was saved correctly.

Ans.
 Reffer to etl_bonus6.png(screenshot)




# .end

