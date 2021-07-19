Mongoose

Schema
- RDBMS의 테이블에서 사용되는 스키마 정의와 같은 역할 제공
- 자유분방한 mongodb 에 제약 사항을 추가하는 역할

---

npm install mongoose

const mongoose = require('mongoose') ;
ES6 | import mongoose from "mongoose" ;

mongoose.connect('mongod://localhost/database_name') ;

const mySchema = new mongoose.Schema({
  val1: {
    type: String, 
    required: true, 
    unique: true, 
    lowercase: true, 
    trim: true, 
    default: ''
  },
  date1: {
    type: Date,
    default: Date.now
  }
}) ;

