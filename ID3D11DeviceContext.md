# ID3D11DeviceContext

ID3D11DeviceContext는 GPU에 Rendering Command를 제공하는 객체이며, GPU의 상태(Vertex, IndexBuffer, Shader, PipelineResources…)의 관리 책임을 갖고 있다.

CPU와 GPU가 Device-Context State를 유지하도록 해주는 객체이다.

DeviceContext는 목적에 맞는 개수의 생성이 필요하다.

예를 들어 GameEngine의 Rendering을 위한 DeviceContext와 Animation 계산을 위한 DirectCompute용 DeviceContext를 소유하는 방식이 있다.

DeviceContext의 수가 늘어남에 따른 장점

- 병렬화를 확대할 수 있으며, 잠재적인 프로그램의 성능 향상을 이룰 수 있다
- 각각의 DeviceContext에 자원을 할당 함으로써 자원 관리가 용이 해 질 수 있다.
- 다양한 입력-출력을 위한 ComputeShader 사용과 같은 작업에 유리 할 수 있다.

DeviceContext의 수가 줄어듬에 따른 장점.

- 작업을 단순화 할 수 있으며, 관리가 편리해진다. 또한 다수의 DeviceContext간 할당 문제를 고려하지 않아도 된다.
- 각각의 DeviceContext의 복제에 따른 메모리 낭비 문제를 줄일 수 있다.
- 최적화와 디버깅이 편리하다.