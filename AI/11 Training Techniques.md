1 [Generalization]
	[hyperparameter]
	[drop out]
2 [Weight initialization (가중치 초기화)]
	[상수 초기화]
	[분포 초기화]
3 [코드]
4
# 1. 모델 정규화
1. **방법 1** : 최적의 hyperparameter 탐색
2. **방법 2:** drop out
**목표**
- 과대 적합을 방지
- 테스트 성능 최대로 확보

## Hyperparameter
- 딥러닝 설계자가 실험적으로 설정 할 수 있는 값들 
  (layer 개수, 필더 크기, 채널 크기, 학습률)
- 근데 시행 착오가 많이 필요
그렇다면 최적의 hyperparameter 찾는 방법
- 테스트(Test) 데이터 셋 : 사용 불가
- 검증(Validation) 데이터 셋 : 사용하기
**방법**:
	1) hyperparameter 세팅하고 Training set 학습
	2) Validation set 정확도 측정
	3) 해당 정확도 바탕을 hyperparameter 재설정
만약 validation set 이 없다면...
	- 학습 데이터 셋의 일부를 활용

## Dropout
- 신경망의 뉴런을 임의로 삭제하면서 "학습" := 학습 때는 은닉층 (hidden layer) 의 뉴런을 무작위로 골라 삭제하는 방식이다
- 이때 Hyperparameter는 'Dropout rate' 
	- dropout rate 는 각 레이에어서 총 뉴런 중에 끈 뉴런의 비율이 됨
**Effectiveness of Dropout**
	가중치가 특정 feature에 대해서만 작동하지 않고 균등하게 학습하게 유도함
	안 보이는 데이터에 better performance
	**실제 Test 에서는 dropout 작동을 꺼두고 모든 가중치를 활용하여 연산 진행**
	-> Train 할 때 dropout 했던 것 들을 Test 할 때는 다시 다 가져오기

# 2. Weight initialization (가중치 초기화)

가중치의 초기값 설정
- 초기값을 어떻게 설정하느냐가 학습에 중요한 영향을 미치고 초기값을 설정하는 다양한 바법들이 존재한다
	-  **상수(constant) 초기화**
		- 가중치를 0으로 초기화
		- 가중치를 임의의 상수로 초기화
	- **분포 초기화** : 가우시안정규 분포 활용
- 초기값을 아주 작은 난수로 초기화 경우의 **문제....**
	- 출력이 점점 0 에 가까워진다
	- 학습이 효과적으로 진행되지 않음
- 대표적인 가중치 초기화 방식
	- Xavier initialization
	- He initialization
	