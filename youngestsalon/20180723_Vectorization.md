### 2018.07.23. 데잇걸즈 TWL : 기계학습 기초 & 단어 벡터화



#### 1. 오전 : 기계학습 기초

- 과제 관련 안내

  - TWL : pull request 하지 않으면 commit log가 남지 않음.

  - 10 minutes to Pandas : Gardening 담당하는 조에서는 Issue 새로 생성해서 진행 요망.

    ~~~
    폴더 생성
    git init
    git remote add origin (GitHub 주소)
    git remote -v
    git remote add upstream (GitHub 주소)
    git remote -v
    git pull --rebase upstream master
    수정 작업
    git add 파일명
    git commit -m "메시지"
    git push -u upstream master
    ~~~

    

- 나는 누구? 여기는 어디?
  - Pandas : Python의 대표적인 데이터 분석 라이브러리
  - Numpy : 행렬, 대규모 다차원 배열을 쉽게 처리하게 해줌. C를 기반으로 개발되어서 좀 더 빠름.
  - Scikit-learn : 머신러닝 관련 라이브러리
    1. 분류 
       - 개/고양이 분류 (딥러닝의 대표적인 사례)
       - 페이스북 사진에 태그할 때 사진에서 사람들을 골라내는 기능
       - G메일의 폴더 분류 (소셜/광고/일반 메일/스팸)
       - 각종 인터넷 사이트 로그인 시 Bot 여부 체크를 위해 그림의 특정 요소를 고르게 할 때 등
    2. 회귀 : 수요 예측, 리뷰 평점 예측
    3. 클러스터링(군집화) : G메일의 폴더 분류(소셜/광고/일반 메일/스팸) 등
    4. 차원 축소 기법으로 시각화



- soynlp 실습 (7/19 실습에 이어서 진행)
  - 정규표현식 (Re 모듈) : 모든 언어에 다 있음. 데이터 처리할때 꼭 공부해야 함.
  - 불용어(개행문자/특수문자 등) 제거 : preprocessing 예제, remove_stopwords 예제



- 기계학습 기초

  - [Scikit-learn 개발자의 ODSCON 발표 자료](https://github.com/amueller/odscon-2015/blob/master/machine-learning-with-scikit-learn-odscon-expanded.pdf) 참조

    

  - 지도학습 (Supervised Machine Learning)

    - Model → Prediction  (예측) → Evaluation (측정)
    - 분류(Classification), 회귀(Regression) 등
    - 예시 'clf.fit(X_train, y_train)' : X는 행렬이라 대문자, y는 vector라서 소문자 사용 

  - 비지도학습 (Unsupervised Machine Learning)

    - Model → New View : Label Data가 없음.

    - 기계가 데이터의 Feature를 분석해서 Label을 찾아내는 형태의 기계학습

      

  - Overfitting, Underfitting

    - Underfitting

      1. 머신러닝이 학습한 데이터가 너무 적은 경우
      2. 머신러닝의 예측값과 실제 데이터의 차이는 크지 않으나, 데이터 자체가 너무 적음

    - Overfitting

      1. 머신러닝이 학습한 데이터가 너무 많은 경우
      2. 결측치 등이 포함 → 머신러닝의 예측값과 실제 데이터의 차이가 커짐

    - 머신러닝은 Underfitting과 Overfitting 사이의 적절한 지점을 찾는 과정

      

  - Decision Trees, Random Forests

    - Decision Trees : 시각화 하기 좋으나 정확도가 떨어진다.
    - Random Forests : 정확도 개선을 위해 Decision Trees를 여러 번 시행함
    - 분석의 depth가 너무 깊어지면 Overfitting이 발생, 너무 얕으면 Underfitting이 발생





#### 2. 오후 : 단어 벡터화

- 자연어 처리 : 텍스트 데이터 정제 / 전처리

  - 기계가 텍스트를 이해할 수 있도록 텍스트를 정제

  - 신호와 소음을 구분, 결측치로 인한 Overfitting을 방지

  - 한국어 전처리 방법

    - HTML 태그, 특수문자, 이모티콘 정리
    - 정규표현식 사용
    - 불용어 (Stopword) 제거 : 조사, 접미사 등
    - 어간추출 (Stemming) : 단어를 축약형으로 바꿔줌
    - 음소표기법 (Lemmatizing) 
      1. 품사 정보가 보존된 형태의 기본형으로 반환
      2. 동음다의어에 대해 각 단어의 품사를 판단하여 그에 따른 적합한 의미를 추출

    

- 자연어 처리 : 텍스트 데이터 벡터화

  - 0과 1밖에 모르는 기계에게 인간의 언어 알려주기

  - 컴퓨터는 숫자만 인식 가능 : 바이너리 코드로 처리 필요

  - 머신러닝/딥러닝 알고리즘은 수치 데이터만 이해 : 텍스트 / 범주형 데이터 → 수치형 데이터

    

  - Bag of Word (BOW)

    - 토큰화(문장 → 단어) + 문서에서 사용된 단어 정리 + 문장 별 각 사용 여부 정리(벡터화)

    - 머신러닝에 기반한 자연어 처리 도구

    - 단점 : 단어의 사용 빈도에 따른 가중치 부여가 불가능, 단어의 순서가 무시됨

      

  - TF-IDF 

    - TF (Term Frequency, 단어 빈도) : 특정한 단어가 문서 내에 얼마나 자주 등장하는가?

    - DF(Document Frequency, 문서 빈도) : 특정한 단어가 문서군 내에서 자주 사용되는가?

    - IDF(Inverse Document Frequency, 역문서 빈도) : DF의 역수

    - TF-IDF : TF * IDF (즉, 곱한 값)

    - 머신러닝에 기반한 자연어 처리 도구

    - BOW의 단점을 보완

    - 동일 문서 내에서 자주 반복되는 단어(= 조사 등의 불용어인 경우)는 무시 

    - 다른 문서에는 별로 없으나, 특정 문서에서 반복되는 단어(= 문서의 주제)는 가중치 부여

      

  - Word2Vec

    - Word imbedding to Vector 의 약자
    - Vector 사이즈가 크면 neural net 성능이 잘 안 나옴 → Word2Vec이 필요
    - 딥러닝에 기반한 자연어 처리 도구
    - 단어를 트레이닝 시킬 때 주변 단어를 label로 매치하여 최적화
      - CBOW : 전체 텍스트로 하나의 단어를 예측. 작은 데이터셋에 유리함.
      - Skip-Gram : 타겟 단어들로부터 원본 단어를 역으로 예측. 큰 규모의 데이터셋에 유리함.
    - 분산된 텍스트 표현을 사용하여 개념 간 유사성을 봄



- 자연어 처리 : 텍스트 데이터 시각화
  - 워드클라우드 
  - 단어 수, 문장 길이, 특수문자, 불용어 갯수 등을 시각화
  - 자연어 처리로 할 수 있는 일 : 맞춤법 수정, 스팸메일 검출, 기계번역, 추천, 챗봇, 자동답변 등



- 실습
  - 한국어 단어 임베딩 모형 테스트 (http://w.elnn.kr/search/) : 재미있는 결과들
    1. 인생 - 남자 + 돈 = 떼돈
    2. 여자 - 남자 + 돈 = 술값
  - NLP : Bag of Words 파일 
    1. Scikit-learn의 CountVectorizer를 통한 단어 벡터화
    2. TF-IDF : TfidTransformer()
  - NLP : Word2Vec 파일
    1. Gensim : Python의 Word2Vec 기능 패키지
    2. 참고 : 수학 개념 중, 벡터의 내적을 구하는 방법은 알고 있어야 함



- 과제
  - 실습 관련 
    - Bag of Words 실습 파일 : for 문 연습으로 불용어 처리 실습
    - Word2Vec 실습 파일 : 단어 유사도 시각화 결과 슬랙 실습 채널에 공유
  - 튜토리얼 : 월요일 B, 화요일 C, 목요일 E, 금요일 G
  - 가드닝 : 10분 판다스 월요일 A, 튜토리얼 화요일 D, 튜토리얼 목요일 F, 10분 판다스 금요일 H
