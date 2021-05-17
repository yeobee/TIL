# Vuex Digest

Vuex를 사용하는 이유?

컴포넌트가 많아졌을 경우 데이터의 관리가 어려워짐

컴포넌트 간 데이터 공유를 편하게 하기 위해서 사용

## 1. Vuex 구성요소

- state

  - 데이터

- getters

  - computed와 비슷한 역할

- mutations

  - state를 변경하는 역할(==state를 직접 조작하면 안됨)

- actions

  - state를 비동기적으로 변경하는 역활
  - mutations를 통해 '간접적' 으로 state를 변경

  

## 2. 컴포넌트에서의 활용법

- state,getters => computed에서 사용

  ```javascript
  //state
  this.$store.state.키값
  
  //getters
  this.$store.getters.함수면
  ```

  

- mutations,actions => methods에서 사용

  ```javascript
  //mutations
  //git에서 commit은 기록
  //mutations은 state의 변경사항의 기록
  this.$store.commit('함수명', 매개변수)
  
  //actions
  this.$store.dispatch('함수명', 매개변수)
  ```

  

## 3. helpers

- store에 있는 요소들의 등록을 간편하게 도와주는 함수

```javascript
//App.vue

import {mapState} from 'vuex'
import {mapGetters} from 'vuex'
import {mapMutations} from 'vuex'
import {mapActions} from 'vuex'

export default {
    computed: {
        ...mapState(['이름1', '이름2']),
        ...mapGetters(['이름1', '이름2']),
    },
    methods: {
        ...mapMutations(['함수명1', '함수명2']),
        ...mapActions(['함수명1', '함수명2']),
    },
}
```

