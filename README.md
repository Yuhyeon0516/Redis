# Redis

In Memory Database의 대표적인 Redis에 대한 공부를 하면서 적어둔 일기장입니다.

## 시작하기에 앞서

### Redis를 사용하는 이유

- 장점

  1. Redis는 모든 데이터가 메모리에 저장되어 빠르다.
  2. 데이터를 단순한 구조로 관리할 수 있다.
  3. 다양한 기능이 없어 무겁지않고 단순하다.

- 단점
  1. 메모리보다 큰 데이터셋을 다룰수 없다.
     - 예를들어 HDD의 크기가 100GB이나 메모리가 8GB라면 8GB만큼의 데이터만 다룰 수 있다.

### 초기 설정

Redis를 설치하고 실행하는 방법에는 크게 두가지가 있다.  
하나는 [Redis](http://redis.com)에서 Redis Cloud 서비스를 이용하는 것이 있고, 또 다른 하나는 local 환경에 Redis를 설치하고 실행하는 방법이 있다.  
아무래도 개발간에는 당연히 local 환경이 편할 것 같다고 생각되고, 아래는 MacOS기준 설치 방법이다.

1. `brew install redis`를 통해 Redis 설치
2. `redis-server` 명령어로 Redis server를 실행
3. `redis-cli` 명령어를 통해 Redis 접속
4. `brew services stop redis` or `redis-cli shutdown` 명령어로 필요 시 Redis 종료

### 자주 사용하는 쿼리

쿼리 명령어가 꽤나 많으니 아래 공식문서를 참고하여 사용하면 될 것 같다.  
https://redis.io/docs/latest/commands/

- Settters

  - `SET <key> <value>`

    - 에시: `SET message 'hi there!'`
      - message라는 key에 'hi there!'의 value를 저장
    - 옵션
      - `EX <seconds>`: 만료 시간을 초 단위로 지정
      - `PX <milliseconds>`: 만료 시간을 밀리초 단위로 지정
      - `EXAT <timestamp-seconds>`: 만료 시간을 유닉스 타임스탬프 초로 지정
      - `PXAT <timestamp-milliseconds>`: 만료 시간을 유닉스 타임스탬프 밀리초로 지정
      - `NX`: 키가 존재하지 않을때만 실행
      - `XX`: 키가 존재할때 실행
      - `KEEPTTL`: 만료 시간을 유지
      - `GET`: 키가 가지고 있던 값을 가져옴. 키가 없다면 nil을 반환하고, 키에 값이 없다면 오류를 반환함.

  - `SETNX`
    - `SET` 명령어에 `NX` 옵션을 더한것과 같음
  - `SETEX`
    - `SET` 명령어에 `EX` 옵션을 더한것과 같음
  - `MSET`
    - `SET` 명령어를 반복해서 호출
    - 예시: `MSET color red model toyota`
      - color key에 red value를 넣고 model key에 toyota value를 넣음
  - `MSETNX`

    - `MSET` 명령어에 `NX` 옵션을 더한것과 같음

  - `SETRANGE <key> <index> <string>`
    - key에 들어있는 value의 index부터 string으로 변경함
    - 예시: `SETRANGE model 2 blue`를 진행 시 model key의 값이 'toyota'라면 'toblue'로 변경함

- Getters

  - `GET <key>`

    - 예시: `GET message`
      - message라는 key의 value를 가져옴

  - `MGET`

    - `GET` 명령어를 반복해서 호출
    - 예시: `MGET color model`
      - color key의 value와 model key의 value를 array로 가져옴

  - `GETRANGE <key> <start_index> <last_index>`

    - key에 들어있는 value를 start_index ~ last_index까지의 value만 가져옴
    - 예시: `GETRANGE model 0 2`를 진행 시 model key에 value가 'toyota'라면 'toy'만 가져옴

  - `INCRBY <key> <number>`

    - key에 들어있는 number형태의 value에 number를 더한 값을 돌려줌

  - `DECRBY <key> <number>`

    - key에 들어있는 number형태의 value에 number를 뺀 값을 돌려줌

  - `INCRBYFLOAT <key> <float>`
    - key에 들어있는 number 또는 float형태의 value에 float을 더한 값을 돌려줌
    - 빼고싶으면 `<float>` 값을 음수로 주면됨

- Delete

  - `DEL <key>`
    - key를 삭제함

### 이커머스 앱 실습(./rbay)
