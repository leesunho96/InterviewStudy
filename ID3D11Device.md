# ID3D11Device

ID3D11Device는 DirectX 11 API의 RenderTarget, Shader, Texture, Buffer와 같은 Direct3D의 가상 자원들을 생성하고, 관리하기 위한 인터페이스 이다.

ID3D11Device는 다음과 같은 기능을 갖고 있다.

- 자원 생성 : ID3D11Device 객체는 Buffer, Texture, Render Target, Shader와 같은 자원들을 생성하고, 관리한다.
- 장치 확인 : ID3D11Device 객체는 Blend State나 Rasterizer State를 설정하는 등의 장치를 확인 할 수 있다.
- 셰이더 컴파일 : ID3D11Device 객체는 Vertex/Pixel Shader를 컴파일 할 수 있다.
- 디버깅 : ID3D11Device 객체는 그래픽 자원과 관련된 경고/에러 메세지를 보고해주며, PIX나 Visual Studio Graphics Debugger와 같은 디버깅 툴에 대한 접근을 지원한다.

ID3D11Devices 객체는 Direct3D의 매우 중요한 객체이며, Rendering 연산시 필요한 자원을 관리하기 위해 사용된다. 일반적으로 프로그램 생성시 해당 객체를 생성하며, 해당 프로그램의 수명 내내 해당 객체를 사용한다.

ID3D11DeviceContext와의 차이점

- ID3D11Device : 물리적 그래픽 장치와의 인터페이스 이며, 자원 생성/관리에 대한 책임을 갖고 있는 객체이다.
- ID3D11DeviceContext :  GPU에서 실행 될 Rendering Command를 위한 인터페이스이다. ID3D11Device에서 생성된 자원(e.g. VertexBuffer, IndexBuffer, Shader ……)을 이용하여 GPU에서 Render하도록 명령하기 위한 인터페이스.