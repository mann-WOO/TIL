# Jenkins

> 지속적 통합 / 지속적 배포(CI/CD)를 도와주는 대표적인 툴

<br>

## 0. Docker 설치

> Docker: 리눅스 응용 프로그램들을 컨테이너로 관리하는 소프트웨어

### 설치중 발생한 문제

- 도커 설치 후 재부팅했으나 CPU의 가상화 사용 설정이 꺼져있다는 경고가 발생하며 도커가 종료됨. PC 재부팅하여 BIOS 설정에 들어가 CPU의 Virtualization 기능을 켜줘서 해결
- 이후 WSL2 구성 요소와 관련해 Linnux kernel을 업데이트 하라는 경고가 뜸. 안내된 사이트로 들어가 설치 완료하여 해결

<br>

## 1. Docker에 젠킨스 설치

### 설치중 특이사항

- 기본 설치 플러그인의 설치가 꽤 오래 걸림.

<br>

## 2. Jenkins와 Gitlab 연동

- 깃랩에서 API token을 발급받아 Jenkins의 시스템 설정에서 등록해준다.
- 젠킨스에 blue ocrean, gitlab, nodesjs 관련 플러그인을 설치해준다.

<br>

## 3. Nginx 설치 후 설정

- 엔진엑스가 로컬의 경로를 참조해 웹서버를 구동시키도록 설치한다.

  - ```bash
    docker run --name nginx -d -p 80:80 -v [로컬경로]:/usr/share/nginx/html nginx
    ```

<br>

## 4. Jenkins Pipeline 생성

- 생성한 파이프라인의 설정에서 'Build Trigger'를 통해 깃랩에서 푸시가 발생했을 경우 파이프라인을 이용해 빌드가 이루어지도록 한다.
  - secret token 을 gitlab의 intergration / trigger 에 등록한다.
  - 이 때 젠킨스가 로컬호스트에서 작동하고 있기 때문에 trigger 또한 로컬 호스트의 주소로 존재한다. gitlab은 로컬호스트를 트리거로 사용하는 것을 금지한다. 따라서  ngrok을 이용해 나의 로컬호스트로 접근할 수 있는 임시 도메인을 부여받고 (실습 목적이므로) 해당 도메인을 사용해 trigger 주소를 설정해줬다.

<br>

## 5. Jenkins Pipeline Script 편집

### Pipeline에서 nodejs 툴을 이용하기 위한 설정

- jenkins 관리 - global tool configurations에서 nodejs tool을 등록한다.

### Pipeline Script

```json
pipeline {
    agent any
    tools {
        nodejs "nodejs"
    }

    stages {
        stage('prepare') {
            steps {
                git credentialsId: '깃랩Id', url: '깃랩저장소url'
            }
        }
        stage('build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
            post {
                success {
                    sh 'scp -r /var/jenkins_home/workspace/pipeline_test/dist /var/jenkins_home/dist'
                }
            }
        }
    }
}
```

- vue 프로젝트를 배포하는 연습을 했기 때문에 npm run build를 통해 배포파일을 만들었다.
- 처음에는 도커의 볼륨에 저장된 dist 폴더를 로컬로 가져오려고 시도했으나, scp를 통한 로컬 접근이 계속 거부되었다. 
- jenkins 컨테이너를 만들 때부터 jenkins 내부의 폴더와 로컬의 폴더를 동기화(?) 하는 방식을 적용해 해결할 수 있었다. 도커 볼륨 내부의 지정한 폴더에 생성된 파일을 전달하고, 해당 폴더가 로컬과 동기화되기 때문에 로컬에도 파일이 전달된다.

<br>

## 6. 최종 작동 방식

1. gitlab 프로젝트 저장소에 push 발생
2. gitlab에서 trigger 작동
3. trigger는 jenkins pipeline을 작동
4. pipeline script에 따라 저장소를 다운받아 npm 라이브러리를 설치하고 빌드
5. build한 결과물을 배포 서버에 전달
   - 현재는 로컬에서 nginx 서버를 만들어 진행했지만, 정식으로 배포를 한다면 클라우드 서버 등이 될 것
6. 배포 완료