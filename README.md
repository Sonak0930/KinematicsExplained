# KinematicsExplained
Forward Kinematics와 Inverse Kinematics 개념을 학습하고 간단하게 시뮬레이션 합니다.

# Kinematics
kinematics는 수학적인 계산을 이용해서 물체의 움직임을 계산하는 역학의 한 분야입니다.
Forward Kinematics와 Inverse Kinematics 2 종류가 있습니다.
이들은 서로 역 관계에 있으며, Forward Kinematics는 로봇의 각 관절의 각도가 주어졌을때, 최종 포지션과 방향을 결정합니다.
Inverse Kinematics는 원하는 최종 방향과 포지션이 주어졌을 때, 각 관절의 각도를 결정합니다.

# Forward Kinematics
먼저 Forward Kinematics 부터 살펴보겠습니다. 편의상 FK라고 부르겠습니다.


<img width="892" height="846" alt="image" src="https://github.com/user-attachments/assets/2de5529c-9a5d-432b-b3b7-202b0274054f" />

FK는 이전 관절과 다음 관절 두 지점 사이의 Transformation(공간변환)으로 정의됩니다. 그림에서는 왼쪽이 0번 joint, 오른쪽이 1번 joint(관절)라고 하겠습니다.
j0->j1으로 가는 Transformation은 좌표축의 회전으로 정의할 수 있습니다.
opengl 기준으로 left-handed coordinate system(왼손 좌표계: 이미지 왼쪽 아래에 있는 좌표축 시스템)을 따라서 j0과 j1에서 좌표축을 각각 정의했습니다.

transformation을 할 때 좌표축을 언급하는 이유는, vector대상으로 transformation을 수행한다고 볼 수도 있지만
축 자체를 회전 시켜도 결과가 동일하기 때문입니다. 따라서 이해하기 쉽도록 **좌표축이 회전한다** 라고 설명하겠습니다.

어쨌든 j0 -> j1 회전으로 좌표축이 변하게 되는데, 이 회전을 정의하기 위해서는 4개의 파라미터가 필요합니다.

<img width="851" height="633" alt="image" src="https://github.com/user-attachments/assets/004a25b9-c6e8-4a71-9536-7bff75d22036" />

먼저 길이를 나타내는 파라미터를 정의하겠습니다. a_i와 d_i가 있습니다. 이 파라미터들은 j0과 j1사이의 translation position을 정의합니다.

<img width="1040" height="710" alt="image" src="https://github.com/user-attachments/assets/f2ce2ad1-ad04-46db-8e2d-51808f6a60c7" />

그 다음으로는 angle rotation을 정의합니다.
angle rotation에는 x angle과 z angle을 사용합니다.


### Definition of Transfomration matrix and y-axis
<img width="751" height="68" alt="image" src="https://github.com/user-attachments/assets/38e874c5-2961-4ec9-a017-7639803336b9" />

먼저 특이한 점은, joint 팔의 회전을 나타낼 때 4개의 Transformation이 필요합니다.
기본적인 3d Transfomration은 XYZ에 대한 angle 3개와 Translation 3개로 총 6개가 필요하지만, Kinmatics 로봇팔의 움직임에는 y축에 대한 translation과 rotation을 고려하지 않아도 됩니다.

그 이유는 아래 DH model에서 함께 설명하겠습니다.

# DH Model
<img width="782" height="431" alt="image" src="https://github.com/user-attachments/assets/6f8b2f78-588c-49ba-b9ec-1a525c210a65" />

왜냐하면 Denavit-Hartenberg (DH) Parameters: The Standard Framework 에서의 기본 가정 때문입니다.
DH는 로봇팔의 움직임을 설명하는 가장 기초적인 모델인데, 이 로봇팔에서는 사람의 팔과는 다르게 로봇 팔이 움직일 수 있는 각도가 1개 축으로만 제한되어 있습니다.
그래서 자유롭게 움직일 수 있는 각도가 1개 각도 (theta, in one axis)기 때문에, 자유도가 1이다 라고 표현합니다.

DH 모델에서는 아까 constraint 3개와 assumption 2개가 존재합니다.



## Categorization of each placed status of arms.

이전에 기계 팔의 회전을 정의할 때 x,z 2개의 축에 대해서만 transformation을 정의하는 이유가 궁금할 것이라 사료됩니다.
저도 “왜 y축 회전/translation은 없는가?”라는 질문을 하게 되었습니다.

<img width="1520" height="1290" alt="image" src="https://github.com/user-attachments/assets/d0bc2c22-b8b6-47a3-b041-8b16d6a85045" />

위 컨디션은 joint 2개의 로봇팔이 주어졌을 때, joint i, i+1번째의 z축이 공간에 배치되는 경우를 나타냅니다.
z_i, z_i+1을 i, i+1번째 joint의  position vector(위치를 나타내는 벡터)라고 정의하겠습니다.
그런데 z축이 공간 상에 배치가 되는 방식에는 여러가지 케이스가 존재합니다.

### c1(Collinearity, Axis alignment): 
<img width="776" height="119" alt="image" src="https://github.com/user-attachments/assets/1d727cd7-dfb2-4bec-8a26-85b2dd103428" />

먼저 zi, zi+1 이 컨디션은 두 벡터가 한 직선 위에 있거나(collinear) 평행(parallel)하다는 것을 나타냅니다.
c1은 기본적으로는 z i+1, z i가 같은 선상에 있다는 의미지만, 식 자체의 의미로는 평행한 케이스도 포함하고 있습니다.


<img width="350" height="322" alt="image" src="https://github.com/user-attachments/assets/0f5f4223-db0c-49db-932c-4c1207649647" />
<img width="1198" height="812" alt="image" src="https://github.com/user-attachments/assets/702c3434-f097-4436-a38f-0d213968930b" />

Collinear한 경우는, 팔을 곧게 뻗었을 때를 생각하면 편합니다. 어깨와 팔꿈치가 일직선이므로, 두 관절에서의 좌표축의 방향이 동일합니다. 

<img width="342" height="335" alt="image" src="https://github.com/user-attachments/assets/8b9c5ea4-681d-40e3-9989-c3135bb682d8" />

### C2(Coplanarity)
<img width="910" height="243" alt="image" src="https://github.com/user-attachments/assets/f0924eb1-e104-46d3-b6bd-8908ce756f9d" />

parallel한 케이스는 다음과 같습니다. 여기서 z벡터는 실제 로봇팔이 아니라, 로봇팔의 z축을 나타냅니다.
Parallel한 경우는 팔꿈치를 접은 모양새입니다. 축의 회전은 변하지만, z축의 방향은 위쪽으로 동일합니다.

<img width="2556" height="1209" alt="image" src="https://github.com/user-attachments/assets/73a5ab4f-ca3c-4fcb-a3c3-3b6fe37f4e33" />

왼쪽 스케치가 Collinear link, 오른쪽은 Parallel한 경우 입니다.

### C3(Axis Coincidence)
<img width="883" height="239" alt="image" src="https://github.com/user-attachments/assets/9b6c0abe-a411-45c3-a04b-72754cea0d73" />



<img width="526" height="191" alt="image" src="https://github.com/user-attachments/assets/5c4835be-7dc2-4fa6-b7f1-170850c50eee" />

x Rotation matrix, x축으로 theta만큼 회전시키는 행렬이다.


