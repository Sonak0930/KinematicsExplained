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
먼저 길이를 나타내는 파라미터를 정의하겠습니다. a_i와 d_i가 있습니다. 각각 
