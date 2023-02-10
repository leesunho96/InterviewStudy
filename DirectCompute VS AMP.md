# DirectCompute VS AMP

DirectCompute와 AMP는 모두 GPU 연산 처리를 위한 프로그래밍 모델이다.

그러나 몇가지 차이점이 있다.

1. DirectCompute
    
    DirectCompute는 Microsoft에 의해 제공되는 Low-Level API이며, 개발자에게 Fine-Grained(하나의 작업을 작은 프로세스로 나눈 뒤, 다수의 호출을 통해 작업 생성하는 방식.                              e,g. void Do() → void First_Do() + void Second_Do() 로 나누어 작업 결과를 생성하는 방식. “Flexible System” 상에서 유용하게 사용.) 한 방식의 GPU 연산 처리를 가능하도록 지원하는 방식이다. 
    
    DirectCompute는 GPU 자원 관리와 병렬 처리 알고리즘을 개발자에게 요구하며, 데이터의 병렬 처리를 위한 함수와 데이터형은  자체적으로 제공한다. DirectCompute는 GPU에서 실행 될 HLSL(High Level Shader Language)을 이용한 Shader를 이용하여 병렬처리를 가능하게 하며, 일반적인 방식의 CPU를 이용한 연산보다 상대적으로 효율적인 데이터 처리를 가능하게 한다.
    
2. AMP(Accelerated Massive Parallism)
    
    AMP는 Microsoft에 의해 Visual Studio 2012 이후 버전부터 제공하는 Higher-Level API이며, DirectCompute를 사용할 시 요구되는 저수준 프로그래밍을 제거하고(host-devide 구조 생성 등), 추상화 하여 GPU 연산시 조금 더 편리한 방식으로 제공한다. AMP는 C++ AMP syntax를 사용하며, DirectCompute의 최상단에서 실행된다. 따라서 동일한 GPU 자원이 사용된다.
    
    AMP의 목적은 GPU연산을 일반적인 C++ 프로그램 작성과 유사하게 작성 가능하지만, DirectCompute의 성능을 지원하기 위한 목적을 갖고 있다.
    
    결론적으로 DirectCompute는 GPU에 대한 Fine-Grain한 관리를 제공 할 수 있다는 장점이 있지만, 개발자에게 더 많은 저수준 프로그래밍을 요구한다.
    
    반면에 AMP는 추상화, 단순화 된 API로서 저수준의 작업을 줄여준다는 장점이 있다.