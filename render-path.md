# 중요한 렌더링 패스

## Construction part (DOM -> CSSOM -> RenderTree의 과정)
    - requests/response : html 파일 요청
    - loading : data 받아옴
    - scripting : 한줄씩 파싱하여 DOM으로 변환, CSSOM으로 변환
    - rendering : 브라우저에 표시하기 위해 렌더 트리를 만들음.


* DOM, CSS의 규칙이 작으면 작을수록 렌더링이 빨라짐.
* 쓸데 없는 태그는 자제. 
* 요소 단위는 작게


## Operation part (layout -> paint -> composition의 과정)
    - layout : 요소들이 어느 위치에 어떻게 표시될껀지 계산하는 과정
    	* 애니메이션이 발생할 때, translate를 이용해서 움직일 때, paint는 일어나지 않고(이미 준비되어 있기 때문에) composition만 바꾸면 된다(Best case)
    	* 무언가 다른 그림이 그려져야 한다면 paint 발생(normal)
    	* 애니메이션으로 인해 layout의 구성요소가 바뀌어야한다. (worst)
    - painting : 그림을 그린다.
    	* layout에서 어떻게 요소들을 배치했느냐에 따라서 조금씩 나누어 이미지를 준비해놓는다.(bitmap 형태)
    	* 즉, 레이어별로 paint를 준비한다 (ex. z-index의 레이어별로 layout를 계산)
    	* css의 will-change의 속성값이 있어 css가 브라우저에 '나는 변경될 수 있는 속성이다'라고 요청하면 브라우저는 따로 레이어를 생성하여 속성을 배치.
    - composition : 미리 준비한 레이어를 차곡차곡 쌓아서 표기