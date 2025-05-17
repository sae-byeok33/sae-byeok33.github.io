---
title: unity Inspector
date: 2025-04-18
category: [게임 프로그래밍,unity]
---
![inspector](https://sae-byeok33.github.io/blog-images/posts_unity/Inspector.png)   
## 상단 영역
![inspector_top](https://sae-byeok33.github.io/blog-images/posts_unity/Inspector_top.png)  
**왼쪽 체크박스** : 오브젝트의 활성화 여부  

**오른쪽 체크박스** : Static , 씬에서 움직이지 않는 오브젝트로 변경  

**Tag** : 오브젝트의 태그 분류  

**Layer** : 충돌 , 렌더링 등의 레이어를 지정할 수 있다  

## Transform  
![alt text](https://sae-byeok33.github.io/blog-images/posts_unity/transform.png)  
**Position** : 오브젝트의 위치   

**Rotation** : 오브젝트의 회전    
    -> 각각 X Y Z 를 기준으로 각각 몇 도(°) 회전했는지 보여줌    

**Scale** : 오브젝트의 크기    
사슬 아이콘은 활성화시 X Y Z 축의 크기가 연결된다  

## Mesh Renderer
![alt text](https://sae-byeok33.github.io/blog-images/posts_unity/Mesh.png)  
### Materials
큐브에 적용된 materials  
드래그하면 다른 materials로 교체가 가능함

### Lighting
**Cast Shadows**  
빛을 받았을때 그림자를 만들것인지 설정한다  
+ On : 그림자 생성  
+ Off : 그림자 없음 
+ Two Sided : 양면에서 그림자를 생성함  

**Static Shadow Caster**  
오브젝트가 움직이지 않을때 unity가 미리 계산해서 그림자를 생성함  
그림자를 실시간으로 계산하지 않기 때문에 퍼포먼스가 향상됨  
예를 들면 건물 벽 , 고정된 장식물 등등  

**Contribute Global Illumination**  
오브젝트가 전역 조명 계산(다른 곳을 밝히는데 영향)에 기여할지 설정  
체크시 이 오브젝트에서 나오는 반사광, 색 번짐 등을 라이트맵에 포함  

**Receive Global Illumination**  
Contribute Global Illumination 켜야 활성화 되는 옵션  

    -> Light Probes : 주변 Light Probe에서 계산된 GI를 받아서 동적 오브젝트에도 부드러운 간접광을 표현  
    -> Lightmaps : 라이트맵에 굽힌 조명을 받아 사용  

### Probes
**Light Probes**  
오브젝트가 간접광을 받는 방식 설정  

**Anchor Override**  
빛 계산 기준이 될 위치를 수동으로 지정함  

### Ray Tracing 
RTX계열 GPU가 있어야만 사용이 가능함!!    

**Ray Tracing Mode**  
광선 추적시 오브젝트의 움직임 처리 방식 설정  
+ off : 광선 추적 기능을 끔  
+ static : 움직이지 않는 오브젝트로 간주, 미리 계산된 결과를 사용 (성능 향상)  
+ Dynamic Transform : 움직일 수 있는 오브젝트로 간주, 움직임에 따라 실시간으로 광선 계산

**Procedural Geometry**  
기존 mesh가 아닌 코딩으로 만든 지오메트리도 광선 추적을 가능하게 하는 옵션  

**Prefer Fast Trace**  
광선 추적용 성능을 튜닝하는 옵션  

### Additional Settings
**Motion Vectors**   
오브젝트의 움직임 정보를 GPU에 전달함  
모션 블러, 시간 기반 이펙트, 후처리 효과 등에 사용됨  

+ Camera Motion Only : 카메라 움직임만 반영  
+ Per Object Motion : 오브젝트의 실제 움직임까지 추적 -> 모션 블러 등이 정확해짐  
+ Force No Motion : 어떤 모션도 전달히지 않음  

**Dynamic Occlusion**  
이 오브젝트가 다른 오브젝트에 의해 가려졌을 때, 렌더링을 생략함 -> 성능 최적화  

**Rendering Layer Mask**  
이 오브젝트가 어떤 렌더링 레이어에 속하는지 지정  

