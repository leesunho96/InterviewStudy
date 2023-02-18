# RenderTarget

RenderTarget은 Graping Pipeline에서 Rendering Operation의 결과물을 저장하는 Buffer이다. RenderTarget은 Rendering 과정의 마지막 목적지이며, 화면에 저장 될 최종 이미지를 저장한다.

Direct3D에서 RenderTarget은 Texture이거나 Rendering Pipeline중 VS-PS 를 거쳐 나온 결과물이며, 화면에 출력되거나 추가적인 이미지 처리를 위한 입력값으로 사용 될 수 있다. 

RenderTarget은 post-processing effect, reflection, shadow 등 다양한 목적을 위하여 사용 될 수 있다. 또한 depth buffer, stencil buffer, multisampling 기술등을 위해 사용 될 수 있다.