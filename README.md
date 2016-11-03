Game Programming with C++ STL
============================
This is a Lecture on 2nd Semester of Senior of Univ.

Chapter 01
----------
Necessary C++ grammar before learning STL<br>
<sub>STL을 학습하기 전 꼭 알아야 할 C++ 문법</sub>

Chapter 02
----------
STL comprehension - Container<br>
<sub>STL의 이해 - 컨테이너</sub>

Chapter 03
----------
STL comprehension - Algorithm<br>
<sub>STL의 이해 - 알고리즘</sub>

Chapter 04
----------
OpenGL - Animation<br>
<sub>OpenGL - 애니메이션</sub>

Chapter 06
----------
OpenGL - Keyframe Interpolation<br>
<sub>OpenGL - 키 프레임 보간법</sub>

#### 제어점 변경을 통한 곡선 변화

제어점: 사용자는 제어점을 변경하여 곡선의 경로를 통제하고 싶어함<br>
보간
- 이산적으로 분포한 값의 간격을 채움
근사
- 이산적으로 분포하는 값의 주위를 통과

#### 곡선의 복잡도와 연결도

복잡도
- 몇차 다항식을 사용하여 표현하는가
- 고차 다항식을 쓰면 부드럽지만 연산량이 많아짐
- 3차 다항식이 일반적으로 많이쓰임. 품질과 속도의 균형.

연결도
- 위치 연결 : 끝 점이 연결되어 있다
- 접선연결 : 끝 점에서의 기울기가 같다
- 곡률연결 : 끝 점에서의 곡률 (회전반경)이 같다.

#### 제어점 변경을 통한 곡선 변화

전역적 제어
- 하나의 제어점을 움직이면 전체 곡선이 변함

지역적 제어(사용자가 선호)
- 하나의 제어점을 움직이면 제어점 근처의 곡선 일부만 변함

**사용자는 지역적 변형을 더 선호함**

#### 삼차곡선 (cubic spline)
곡선위의 모든 점에서 C2 연결성 (두번 미분해도 연속임, 부드러움의 정도) 보장

1차 함수를 표현하는 점의 개수는?
- 2개 (2점을 지나는 1차 함수는 하나로 결정됨)

2차 함수를 표현하는 점의 개수는?
- 3개

3차 곡선을 표현하는 점의 개수는?
- 4개

**e.i)** 점 n 개를 모두 지나는 다항식은? <br>
`an-1xn-1 + an-2xn-2 + … + a1x1 + a0x0 = 0` <br>
n개의 점을 입력하여 계수를 구함 <br>
**Answer)**  n-1 차 함수

#### 제어점이 n개 일때의 곡선

n-1 차 다항식으로 표현하는 경우
- 곡선이 부드럽다
- 계산량이 많아 복잡하다
- 전역적 특성으로 조작하기 불편하다.

여러 개의 3차 함수 조각들을 부드럽게 이어서 사용
- 곡선은 (여전히) 부드럽다
- 계산량이 적어진다
- 제어점이 변경되면 몇개의 조각에만 변형이 일어난다.  지역적 특성


이를 위해 Catmull-Rom spline 가 쓰임.

Catmull-Rom spline : 좌우 꼭지점의 기울기 값의 평균이 사잇꼭지점의 기울기 값

#### 삼차곡선의 유도
곡선의 시작점과 끝점이 각각 제어점을 지나야 한다.
- s1(0) = P1
- s1(1) = P2

곡선의 시작점 기울기가 이전 곡선 끝점 기울기와 같아야 한다.
- s’1(0) =  P’1 = s’0(1)
- s’1(1) =  P’2 = s’2(0)

삼차곡선을 다음과 같이 정의하고, 위의 경우를 대입.
```
S(u) = B0 + B1u + B2u2 + B3u3 (단 Bi는 계수)
= P1 + P’1 u + (3(P2-P1)-2 P’1- P’2) u2 + (2(P1-P2)+ P’1+ P’2)u3
```

#### 삼차곡선의 기울기
각 위치에서 P’n을 구하는 방법
- 임의로 대입한다.
- 미분 연속조건을 이용한다.
    - P’1 = a(P2-P0)		: Cardinal spline
    - 일반적으로 a=0.5		: Catmull-Rom spline

Chapter 07
----------
OpenGL - Collision<br>
<sub>OpenGL - 충돌</sub>

Chapter 08
----------
OpenGL - Kinematics<br>
<sub>OpenGL - 운동학</sub>

힘을 고려하지 않는 움직임을 연구하는 학문
- F = ma  (X)
- X = f(t) (O)

물체를 구성하는 뼈대를 움직여서 움직임을 구현함
- 힘이 무시되어 있으므로 부자연스러움
- 수식을 매우 정교하게 적용하여 극복

#### 계층적 모델
물체는 뼈대와 관절로 구성되어 있다고 가정
- 뼈대는 움직이지 못함
- 관절(joint)을 중심으로 움직임이 발생

인체 모형도 뼈대와 관절로 구성됨

#### 운동학의 종류
Forward Kinematics: (p, q) = F(θ<sub>i</sub>)

Inverse Kinematics: θ<sub>i</sub> = F<sup>-1</sup>(p, q)

#### Joint Link 변환

물체 중심(기준)으로부터 말단으로 진행하며 변환이 추가됨
- 전체 변환은 경로를 따른 모든 변환의 곱

실제 모델의 경우
- Joint에서도 거리 변환이 있으며 Link도 회전 변환이 있을 수 있다.

#### 물체의 계층 표현
이전 단계에서 다음 단계로 진행
- 변환(행렬)의 곱으로 표시

#### 물체의 계층 표현
Tree 자료구조
- Node로서 Joint 변환을 표시
- Arc로서 Link 변환을 표시

#### 말단 구조를 그릴 때
- 좌표와  각도 필요
- 깊이 우선 탐색 (depth first traversal)
- 참고) OpenGL의 matrix stack
