# Docker
+
```
docker pull mongo 
```
+
```
docker run -d \
--name mongodb \
-p 27017:27017 \
-v /home/mongodb:/data/db \
-e MONGO_INITDB_ROOT_USERNAME=root \
-e MONGO_INITDB_ROOT_PASSWORD=secure \
mongo
```
로그인 및 접속하기
- 계정을 사용하지 않고 그냥 로그인해서 조회나 데이터 등록 등을 하면 unauthorized 오류가 발생한다.
```
docker exec -ti mongodb mongo -u root -p
```


### RDBMS 기준 개념 비교
|RDBMS|MONGODB|
|---|---|
|Database|Database|
|Table|Collection|
|Row|Document|
|Column|Field|



# MongoDB
+
```
show dbs
show collections
db.collection.find()
db.collection.find().pretty()
```
+
```
> use test_db
switched to db test_db
> db
test_db
```
+
```
db.collection_1.insert({id:"id1", weight: 1.0})
```
