# 📝 동기화 메모장 📝
- 소개: 디바이스 사이즈에 따라서 보여지는 화면이 다른 메모장이다.
- 기간: 2021.02.15 ~ 2021.03.05
- 팀원: [꼬말](https://github.com/hakju), [솔](https://github.com/soleJin)
- [팀 그라운드 룰](https://github.com/hakju/ios-cloud-notes/blob/main/GroundRule.md)
<p align = "center">
 <img src = "https://user-images.githubusercontent.com/50835836/117425115-72eebd00-af5d-11eb-8cd4-9ea4664a5bba.gif" alt = "CompactMode" width = "300" height = "600">
 <img src = "https://user-images.githubusercontent.com/50835836/117425221-90bc2200-af5d-11eb-8f9d-3586aaf2aad5.gif" alt = "RegularMode" width = "600" height = "300">
</p>
 
---

## 👨🏻‍💻 구현 내용 👨🏻‍💻
- 뷰를 코드로 작성하고 오토레이아웃을 적용하였다.
- 디바이스의 크기에 따라 다른 화면을 보여주도록 구현하였다.
- mock data를 활용하여 JSON 데이터를 Decode하여 테스트하였다.
- DataDetectorTypes을 활용하여 메모 영역에서의 메모는 전화번호, URL, 날짜 등을 자동으로 탐지한다.
- 메모의 작성일자는 사용자의 지역 포멧에 맞게 구현하였다.
- 메모 영역에서 user가 터치한 정확한 부분을 찾아서 수정, 삭제를 할 수 있다.
- Core Data를 활용하여 로컬에서 메모의 데이터를 저장하도록 구현하였다.
- 메모의 CRUD를 구현하였다.
- 액티비티 뷰를 구현하여 해당 메모를 공유, 삭제를 할 수 있다.

---

## 💡 어떻게 구현할까? 💡
- 가장 먼저 UI를 그려야겠다고 생각했다. UI를 스토리보드를 통해서 구현할 지, 코드를 통해서 구현할 지 첫번째 고민이 시작되었다. 팀원과 협의한 결과 **코드**로 작성하기로 결정하였다. 그 이유는 스토리보드와 코드로 구현하는 방법 모두 장단점이 있었지만, 코드의 장점에 조금 더 끌렸기 때문이다.    
  - #### UI 구현 방법중 스토리보드, 코드 구현의 차이점
  |  | 장점 | 단점 |
  | :---- | ---- | ---- |
  | **스토리보드** | 눈으로 볼수있기 때문에 비교적 직관적이다. | 협업시 코드를 merge하는 과정에서 충돌을 유발할 수 있다. |
  | **코드** | 추후의 UI가 많아졌을 때, 유지보수 측면에서 이점이 강하다. | 눈으로 직접 확인할 수 없어서 실수를 유발할 수 있다. |   
  - UI를 코드로 구현하며 오토레이아웃도 작성하였다.
  - 디바이스의 사이즈에 따라서 다른 화면이 보여져야되기 때문에 SplitView를 학습하여 적용해봤다.
- SplitView로 화면을 구성하였는데, Compact Size인 화면에서 앱이 처음 실행될 때 메모를 선택하지 않아도 비어있는 메모가 보여지는 에러가 발생했다.   
    - <p> <img src = "https://user-images.githubusercontent.com/50835836/118014062-c31ab480-b38d-11eb-8026-755ad44f3ac1.gif" alt = "error1" width = "300" height = "600"> </p> 
    - [Trouble Shooting](www.naver.com)   
- 이번에는 Regular Size인 화면의 DetailView(우측 View)에서 navigationBar가 안보이는 에러가 발생했다.
    - <p> <img src = "https://user-images.githubusercontent.com/50835836/118010239-ce6be100-b389-11eb-866f-724cf546e076.gif" alt = "error2" width = "600" height = "300"> </p>   
    - [Trouble Shooting](www.naver.com)   

---

## 💯 문제 해결 💯
1. Regular Size인 화면에서 앱이 처음 실행될 때, 메모를 선택하지 않아도 비어있는 메모가 보여지는 에러
    - 원인: SplitView 스택의 최상위가 로드된다. 즉 RegularMode일때의 우측 뷰가 보여지게 되는 것이다.
    - 해결 방안: 
2. DetailView에서 navigationBar가 안보이는 에러
    - 원인: ListView(좌측뷰)에서 ListCell의 메모를 터치하였을 때 선택된 메모의 뷰가 DetailView(우측뷰)를 덮어버린다.
    - 해결 방안: 
3. 키보드가 올라올때 view가 가려지는 현상과 키보드를 내리기 위해서 TextView가 아닌 부분을 터치해야만 한다.
    - 원인: 
    - 해결 방안: 
4. 메모의 리스트를 선택할때, MainViewController에서 DetailViewController의 현재 view를 pop한 뒤 선택된 메모 view를 push해주었다.
    - 원인: 
    - 해결 방안: 
