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

## 4 Parameters required for Transformation

그러면 왜 3개의 축에 대한 회전이 필요한데, 2개의 축에 대해서만 transformation을 정의하는지 궁금할 것입니다.
“왜 y축 회전/translation은 없는가?”라는 질문을 하게 되었습니다.
그 이유를 두 가지 방식으로 설명할 수 있는데.

<img width="1469" height="1391" alt="image" src="https://github.com/user-attachments/assets/541db701-bb7b-45aa-ba41-468b92477b6b" />

일단 첫 번째는 정석적인 방식으로, axiom: 공리 기반 constraint(condition: 조건)으로 설명하는 방식입니다.

<img width="1520" height="1290" alt="image" src="https://github.com/user-attachments/assets/d0bc2c22-b8b6-47a3-b041-8b16d6a85045" />

z_i, z_i+1을 joint i, i+1에서의 방향벡터라고 정의하겠습니다.
그러면 로봇이 정상적으로 동작하기 위해서는 다음과 같은 세 가지 공리가 성립해야 합니다.

c1: ||zi x zi+1|| = 0
먼저 zi, zi+1
이 컨디션은 두 벡터가 한 평면에 있다라는 것을 나타냅니다.
(평행하거나, )

<img width="1198" height="812" alt="image" src="https://github.com/user-attachments/assets/702c3434-f097-4436-a38f-0d213968930b" />


<img width="526" height="191" alt="image" src="https://github.com/user-attachments/assets/5c4835be-7dc2-4fa6-b7f1-170850c50eee" />

x Rotation matrix, x축으로 theta만큼 회전시키는 행렬이다.


