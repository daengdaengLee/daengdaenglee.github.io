# 결함 감지, 분류 어플리케이션 UI 개발

## 어플리케이션 개요

- Fault Detection & Classification의 약자
- 반도체 제조와 같은 공정에서 센서 데이터를 입력받아 이상을 감지, 분류하는 시스템

## 기간

- 2018.08 ~ 2018.09

## 프로젝트 종류

- 사내 프로젝트
- Brique

## 사용 기술

- HTML
- CSS
- JavaScript
- [Dygraphs.js](https://github.com/danvk/dygraphs)
- [React.js](https://github.com/facebook/react/)
- [Redux](https://github.com/reduxjs/redux)
- [Redux-Saga](https://github.com/redux-saga/redux-saga)
- [styled-components](https://github.com/styled-components/styled-components)
- [antd](https://github.com/ant-design/ant-design/)

## 주요 업무

- 해당 시스템의 과거 데이터 사각화 및 실시간 모니터링을 위한 웹 UI 제작
- 조건에 따라 알맞은 형태로 변하는 유동적인 조건 입력 폼 UI 제작
- 대용량 데이터 (100만 레코드까지) 를 표현할 수 있는 차트 UI 제작
- 줌, 패닝, 레전드와 같은 차트 기능 커스터마이징
- 특정 조건에 맞는 데이터만 출력하도록 차트 기능 커스터마이징
- 차트 라이브러리 (dygraphs.js)와 React.js 기반의 전체 View 시스템 통합

## 배운 점

- 직접 DOM 을 조작하는 라이브러리를 React.js 와 같은 가상 DOM 기반 라이브러리로 래핑하는 방법
  - React.js 의 prop 으로 업데이트 조건을 받아서 componentDidUpdate 훅에서 DOM 조작 메소드 호출
- 가상 DOM 기반의 라이브러리에서 ref 를 사용하여 DOM 객체를 직접 조작하는 방법

## 문제점 및 개선 방법

### 문제점 1

차트 컴포넌트 외부의 조건이 변경될 때 차트 컴포넌트의 업데이트가 불안정한 문제

#### 원인

- 특정 이벤트나 비동기 작업의 결과에 따라 차트의 줌, 패닝 등 특정 기능을 초기화하거나 주어진 옵션으로 차트의 상태를 변경해야 하는 경우
- 컴포넌트 업데이트 과정에서 해당 차트의 DOM 객체를 조작해야 할 필요성 발생
- 요구사항 구현을 위해 많은 플래그 prop들이 생겨나고 유지보수하고 이해하기 어려운 코드 작성
- 복잡해진 코드로 인해 차트의 동작이 불안정해지고 문제의 원인을 파악하기 어려워짐

#### 개선 방법

- RxJS와 같은 옵저버블, 스트림 개념의 구현체를 사용하여 특정 이벤트를 함수 합성을 통해 일련의 데이터 흐름으로 변경
- 필요한 DOM 변경에 대한 함수를 작성하고 옵저버블을 구독
