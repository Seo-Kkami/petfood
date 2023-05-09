# 사용법

### connect.js를 추가해야 함

const mysql = require('mysql');

const conn = {
host: 'localhost',
port: '3306',
user: 'root',
password: '',
database: 'petsfood',
};

let connect = mysql.createConnection(conn);
connect.connect();

module.exports = { connect };
위의 코드에서 password를 채워서 사용하면 됨!

## 라이브러리 및 프레임워크

#### 프론트엔드

react
react-router-dom
styled-components
axios
http-proxy-middleware

#### 백엔드

express

## 개발환경 및 DB

OS: windows 10
Tool: VSCode
DB: MySQL

## 22.05.04

### 테이블 수정 : user 테이블에 password 컬럼을 추가

alter table user add password varchar(30) not null;

## 22.05.08

### 회원가입 구현 완료 : id, pw, 애완동물이름, 품종명 저장완료 품종명은 DB에 존재해야하므로 확인하고 저장

#### 쿼리

`select * from specie where breed = '${req.body.breed}';`
`insert into user values ('${req.body.id}','${req.body.password}');`
`insert into pet values ('${req.body.id}','${req.body.breed}','${req.body.petName}');`

참고사이트 [https://velog.io/@soshin_dev/ERRHTTPHEADERSSENT-Cannot-set-headers-after-they-are-sent-to-the-client-%EC%98%A4%EB%A5%98](https://velog.io/@soshin_dev/ERRHTTPHEADERSSENT-Cannot-set-headers-after-they-are-sent-to-the-client-%EC%98%A4%EB%A5%98)

## 22.05.09

### 로그인 구현 완료 : 로그인 상태면 메인 페이지에서 종과 품종명이 자동으로 입력되게 구현

#### 쿼리

`select * from user where user_id = '${req.body.id}' and password = '${req.body.password}';`
`select breed, species from specie where breed = (select breed from pet where user_id = '${req.body.id}');`

##### 기타

localStorage를 이용하여 로그인된 유저의 id를 저장
로그인 버튼을 로그아웃 버튼으로 바꾸고 로그아웃 버튼을 누르면 localStorage에서 id 데이터를 삭제

## 22.05.10

### 종과 음식명을 입력하면 섭취가능여부를 출력

#### 쿼리

`select is_edibility from edibility where species = '${req.body.species}' and food_name = '${req.body.foodName}';`
