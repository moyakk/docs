## 데이터 조회

### 조회에 사용 할 수 있는 기능

- find()
- aggregate()

### find 와 aggregate 뭐가 다르지?

- find() 는 단순한 조건 검색에 사용된다. ``같아? 달라? 커? 작어? 포함해? 뭐 이런..``
  - 겁나 조합하면 제법 복잡한 조건 검색도 할 수야 있겠다만 굳이..?
  - 여튼 중요한건, find() 는 집계 기능을 제공하지 않는다는 점이다. ``GROUP BY 안됨!``
- aggregate 는 find 에 비해 좀 더 확장된 검색 조건을 활용할 수 있으며, 집계 기능을 이용 할 수 있다.
  - pipeline 이라는걸 통해서 예약어 같은걸로 간단히 집계 처리를 한 결과를 가져올 수 있다.
  - 그 외에 aggregation 의 처리 과정은 C++ 로 개발되어 find() 대비 처리 속도가 매우 빠르다고 한다.
  - 샤딩이라던가 좀 더 전문적인 내용이 나오는데 아직 제대로 공부를 한건 아니라 정리를 못하겠다.

### mongoose 실직적인 사용 예시

- model 의 스키마에 Date 타입인 updated 필드가 있다고 가정한다.
  - 아래 예시는 updated 필드에서 지난 3일간 특정 시간(hour)에 갱신된 데이터만 가져오는 조회 기능을 구현한다.
  - 조회 조건에 사용되는 값은 편의상 momnet.js 를 사용했다.
  - 그냥 코드만 딱 봤을때는 aggregate() 가 더 길어서 복잡해 보이는데, 조회 조건을 더 편하게 넣을 수 있다는 점에 주목하자.

find() 사용
```js
model.find({
  updated: {
    $or: [
      { $gte: moment('2021-07-20 13').startOf('hour'), $le: moment('2021-07-20 13').endOf('hour') },
      { $gte: moment('2021-07-21 13').startOf('hour'), $le: moment('2021-07-21 13').endOf('hour') },
      { $gte: moment('2021-07-22 13').startOf('hour'), $le: moment('2021-07-22 13').endOf('hour') },
    ]   
  }
}, (err, docs) => {
  if (err) throw err ;
  console.log(docs) ;
})
```
aggregate() 사용
```js
model.aggregate([{
  $addFields: {
    updatedDate: { $dateToString: { format: "%Y-%m-%d", date: "$updated" } },
    updatedHour: { $hour : "$updated" }
  }
}, {
  $match: {
    updatedDate: { $in : ["2021-07-20", "2021-07-21", "2021-07-22"] },
    updatedHour: 13
  }
}], (err, docs) => {
  if (err) throw err ;
  console.log(docs) ;
}) ;
```
