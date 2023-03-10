# Lights

현실의 조명은 광원으로부터 물체로 빛이 향하고, 해당 빛을 우리의 눈에서 인식하는 방식으로 이루어 지지만, CPU로 모든 광원으로부터의 빛을 연산하는 행위는 매우 많은 비용을 요구한다. 따라서 우리는 여러가지 방식으로 조명의 처리를 구현하는데 기본적인 4가지가 존재한다.

1. Ambient Color
- 해당 씬의 주된 색상을 의미한다. 해당 색상은 모든 픽셀(혹은 정점)에서  동일한 방향으로, 동일한 색상이 들어온다고 가정한다.
- 일반적으로는 단일색상을 사용하지만, 필요에 따라 색상값을 보간하여 사용하는 경우도 존재한다.
1. Diffuse (Lambert)
- Diffuse는 물체 자신의 색상을 표현하기 위한 조명이다.
- 자신의 색상을 표현하기 위해서는 기본적으로 자신의 갖고 있는 색상 + 조명으로 인한 음영처리가 필요하다. 해당 음영처리는 광원의 방향벡터와 해당 픽셀(혹은 정점)에서의 법선 벡터를 이용하여 계산한다.
- Diffuse Color = Dot(-Light Direction, Normal vector) * Texture Color.
- 조명의 입사 벡터를 뒤집은 후, 해당 지점의 법선 벡터와 내적을 하면 해당 사이각의 cos값이 구해진다. (두 벡터는 모두 정규화된 벡터 → 크기가 1이며, Dot(a, b) = abs(a) * abs(b) * cosX 의 식이 성립하기 때문에 두 벡터의 내적은 두 사이각의 cos값과 동일하다.) x값이 0~90 사이의 값이며, 따라서 0 ≤ cosX ≤ 1이 성립한다. x의 값이 크면(빛의 입사각과 해당 지점의 법선 벡터 사이의 각도가 크다 = 빛의 양이 적다) 점점 0에 가까워 질 것이며, 해당 지점의 색상은 어둡게 반환 될 것이다. 반대로 x의 값이 작으면(빛의 입사각과 해당지점의 법선 벡터 사이의 각도가 작다 = 빛의 양이 많다) 점점 1에 가까워 질 것이며, 원본 색상에 가까운 색상이 반환될 것이다.
- Diffuse는 Unreal Engine의 Material 내부 BaseColor이다.
1. Specular (Phong)
    - 빛의 양을 조절하기 위한 방식이다.
    - 우리가 3차원 물체를 2차원 화면으로 바라보게 되기 때문에, 적절한 빛의 처리가 존재하지 않으면 음영감이 사라지고. 단순한 평면으로 보이게 되며, 해당 현상을 없애기 위해 추가적인 조명 처리가 필요하다.
    - Specular가 0이 되면 물체의 원근감이 사라지며, 커질수록 원근감이 커지게 된다.
    - 쉐이더는 기본적으로 연속적으로 퍼져나가는 값이며, 빛의 밀도는 동일함에 따라 면적이 넓어지면 빛은 흐려지고, 면적이 좁아지면 빛은 점점 강해진다.
    - Specular Color = Power(Dot(R, E) * Shiness) * Color. (R : 들어오는 빛의 법선벡터에 대한 반사 벡터, E : 해당 지점(pixel)로 부터 카메라를 바라보는 방향벡터)
2. Emmisive
    - 물체의 표면에서 스스로 뿜어내는 빛을 표현하는 방식이다.
    - 램프나 어두운 배경의 반짝임 같은 빛을 표현하는데 사용되며, 특히 어두운 배경의 어두운 물체를 표현하는 경우, Emmisive를 사용하여 배경과 물체를 구분하는 등으로 사용된다.
    - Emmisive를 제외한 나머지 세가지는 Vertex Shader에서 처리 한 후, Rasterize State에서 해당 값을 선형 보간하여 Pixel Shader로 넘기는 방식의 처리가 가능하지만(해당 방식의 처리시 비용이 줄어들지면, 어색한 처리가 이루어지게 된다.), Emmisive만큼은 Pixel Shader에서만 처리가 가능하다.

이 외에도 최근에는 Ray-Tracing이라는 방식도 존재한다.

현실의 조명은 다양한 광원에서 대량의 빛이 모든 방향으로 퍼져나가고, 해당 빛들이 물체에 부딛힌 후, 우리의 눈으로 들어온다. 하지만, 카메라에서 빛을 발사하여 해당 빛을 추적하는 방식으로 현실적인 조명 처리를 가능하게 한다.