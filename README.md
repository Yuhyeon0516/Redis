# Redis

인메모리 Database의 대표적인 Redis에 대한 공부를 하면서 적어둔 일기장입니다.

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
