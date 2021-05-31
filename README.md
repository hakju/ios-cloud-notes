# 📝 동기화 메모장 📝
- 소개: 디바이스 사이즈에 따라서 보여지는 화면이 다른 메모장이다. 클라우드와 연동하여 다른 기기와 동기화할 수 있다.
- 기간: 2021.02.15 ~ 2021.03.05
- 팀원: [꼬말](https://github.com/hakju), [솔](https://github.com/soleJin)
## 🐥팀 그라운드 룰 (꼬말, 솔)

### <우리 팀만의 규칙>

- 디스코드에 있을 때는 언제든지 편하게 연락해도 좋습니다 :)

- TIL 일주일에 적어도 두 번은 꼭 쓰기 (짧아도 괜찮아요🙂)

- 각자 공부 후에도 모르겠는 문제에 대해서는 3시간을 넘기지 않고 질문하기

- 필요한 개념들은 확실히 공부하고 넘어가기

- 수업에 들어가기 전에 예습한 내용 공유하기


### <스크럼>

- 스크럼 시간은 매일 오전 10시

- 나눌 내용

    - 컨디션 공유

    - 어제 공부한 내용 공유

    - 오늘 공부할 내용 공유

    - 프로젝트


### <Branch>

- '1-sole' branch에는 최종 제출할 내용을 PR 보내고 머지는 상대방이.

- 'step1-sole', 'step1-kkomal' branch 에서 작업 후 해당 branch를 깃헙에 푸쉬.

- 'stepn' branch에 각자 브렌치에서 작업한 내용을 머지. (step1-sole -> step1 머지)

- 'stepn' 에 있는 상대방의 작업 내용을 로컬에서 pull하고 자신의 브렌치로 머지. (step1 -> step1-kkomal 머지)

- 커밋메세지 규칙

- 커밋단위 : 빌드되는 상태에서, 기능단위로 커밋하기.


### <Commit Message 규칙>

- feat: 기능구현

- refactor: 기능수정

- fix: 버그 수정

- style: 동작에 영향없는 코드변경, 이름변경

- test: 테스트 추가, 테스트 리팩토링

- docs: 문서수정


### <코딩 컨벤션>

- Swift API 디자인 가이드라인을 준수하기.

- naming에 신경쓰기.

- 의미없는 띄어쓰기, 줄바꿈은 안하도록 주의하기.

- 기능 분리 잘 되도록 주의하기. (1 함수 1 기능 지향)

<p>
 
---
 
## 📱 앱 동작화면 📱
 <img src = "https://user-images.githubusercontent.com/50835836/117425115-72eebd00-af5d-11eb-8cd4-9ea4664a5bba.gif" alt = "CompactMode" width = "295" height = "590"> <img src = "https://user-images.githubusercontent.com/50835836/117425221-90bc2200-af5d-11eb-8f9d-3586aaf2aad5.gif" alt = "RegularMode" width = "590" height = "295">
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
### UI 구현
- 가장 먼저 UI를 그려야겠다고 생각했다. UI를 스토리보드를 통해서 구현할 지, 코드를 통해서 구현할 지 첫번째 고민이 시작되었다. 팀원과 협의한 결과 **코드**로 작성하기로 결정하였다. 그 이유는 스토리보드와 코드로 구현하는 방법 모두 장단점이 있었지만, 코드의 장점에 조금 더 끌렸기 때문이다.    
  - #### UI 구현 방법중 스토리보드, 코드 구현의 차이점
  |  | 장점 | 단점 |
  | :---- | ---- | ---- |
  | **스토리보드** | 눈으로 볼수있기 때문에 비교적 직관적이다. | 협업시 충돌이 빈번하고, 재사용성이 불리하다. |
  | **코드** | 추후의 UI가 많아졌을 때, 유지보수 측면에서 이점이 강하다. | 눈으로 직접 확인할 수 없어서 실수를 유발할 수 있다. |   
  - UI를 코드로 구현하며 오토레이아웃도 작성하였다.
  - 디바이스의 사이즈에 따라서 다른 화면이 보여져야되기 때문에 SplitView를 학습하여 적용해봤다.


#### 1. 문제 해결

- SplitView로 화면을 구성하였는데, Compact Size인 화면에서 앱이 처음 실행될 때 메모를 선택하지 않아도 비어있는 메모가 보여지는 문제가 발생했다.   
    - <p> <img src = "https://user-images.githubusercontent.com/50835836/118014062-c31ab480-b38d-11eb-8026-755ad44f3ac1.gif" alt = "error1" width = "300" height = "600"> </p> 
    - Regular Size인 화면에서 앱이 처음 실행될 때, 메모를 선택하지 않아도 비어있는 메모가 보여지는 문제
    
    - 원인: SplitView 스택의 최상위가 로드된다. 현재 SplitView의 스택에는 listView(좌측뷰), detailView(우측뷰) 순서로 되어있기 때문에 앱이 처음 로드될 때 detailView가 보이는 것이다.
    
    - 해결 방안: UISplitViewControllerDelegate의 메서드를 활용하여 해결할 수 있었다.   
      > 매개변수의 secondaryViewController에는 SplitView 인터페이스의 SecondaryViewController가 들어가게 되고, primaryViewController에는 SplitView 인터페이스의 PrimaryViewController 들어가게 된다. 즉, PrimaryViewController는 listViewController, SecondaryViewController는 detailViewController가 해당된다. <br> 이 메서드의 반환값은 Bool 타입으로 fasle일 경우 SecondaryViewController의 content를 인터페이스에 통합하고, true인 경우 SecondaryViewController에 대해 아무작업도 하지않게된다. 
    
     - 나의 경우는 앱이 처음 실행되었을 때 listView가 보여지길 원했기 때문에 detailViewController에 대해서는 어떤 작업도 필요하지 않도록 반환값을 true로 설정하였다.
    ``` swift
    //MainViewController
    
    splitViewController(self, collapseSecondary: detailViewController, onto: listViewController)
    
    extension MainViewController: UISplitViewControllerDelegate {
     func splitViewController(_ splitViewController: UISplitViewController, collapseSecondary secondaryViewController: UIViewController, onto primaryViewController: UIViewController) -> Bool {
        return true
    }
    ```  
    
#### 2. 문제 해결

- 위 문제를 해결하고 나니 이번에는 Regular Size인 화면의 DetailView(우측 View)에서 navigationBar가 안보이는 문제가 발생했다.
    - <p> <img src = "https://user-images.githubusercontent.com/50835836/118010239-ce6be100-b389-11eb-866f-724cf546e076.gif" alt = "error2" width = "600" height = "300"> </p>   
    - DetailView에서 navigationBar가 안보이는 문제
    
    - 원인: ListView(좌측뷰)에서 ListCell의 메모를 터치하였을 때 선택된 메모의 뷰가 DetailView(우측뷰)를 덮어버린다.
    
    - 해결 방안: 이미 생성되어있는 detailView에 textView를 덮어쓰고 있기 때문에 발생한 것이라 파악하고 SplitView(viewControllers) 스택의 최상위에 있는 detailView(우측뷰)를 pop해준다. 선택된 메모를 navigationViewController로 SplitView 스택에 push해준다. 
     ``` swift
     func didTapListCell(memo: Memo?) {
        (self.viewControllers.last as? UINavigationController)?.popToRootViewController(animated: false)
        
        let detailView = DetailViewController()
        detailView.view.backgroundColor = .white
        guard let memo = memo else { return }
        detailView.memoTextView.text = "\(memo.title)\n\n"
        detailView.memoTextView.text += memo.contents
        
        (self.viewControllers.last as? UINavigationController)?.pushViewController(detailView, animated: false)
    }
     ``` 
     
#### 3. 문제 해결

- 위 문제를 해결하는 과정에서 메모리적 낭비가 발생되었다. 메모가 선택되었을 때 이미 생성되어있던 view를 선택된 메모의 view가 덮어썼기때문에 기존의 view를 pop해준뒤 선택된 메모를 새로운 view로 push해주도록 해결하였다. 이 과정에서 기존의 view는 생성이 된 후 메모가 선택된다면 메모리에서 제거가 되기때문에 기존의 view를 그대로 사용할수는 없는것일까?라는 고민에서 시작되었다.
    - 위 2번 문제의 연장으로 메모를 선택할때, MainViewController에서 DetailViewController의 현재 view를 pop한 뒤 선택된 메모 view를 push해주었다. 기존에 생성되어있는 detailView를 사용할 수는 없을까?라는 고민이 있었다.
    
    - 원인: 이전 DetailViewController를 pop해서 메모리에서 삭제하고 새로운 DetailViewController를 초기화해서 셋팅하고 push 하고 있기 때문에 메모리가 낭비된다고 생각했다.
    
    - 해결 방안: 기존에 생성되어있는 view를 pop하지 않고 기존 view에 그대로 push하도록 코드를 개선하였다.
     ``` swift 
     func didTapListCell(memo: Memo?) {
        guard let lastView = self.viewControllers.last as? UINavigationController else { return }
        
        let detailView = DetailViewController()
        detailView.view.backgroundColor = .white
        guard let memo = memo else { return }
        detailView.memoTextView.text = "\(memo.title)\n\n"
        detailView.memoTextView.text += memo.contents
        
        lastView.pushViewController(detailView, animated: false)
    }
    ```
### Core Data
- 앱이 종료되고 난 후에 다시 앱이 실행되었을 때, 메모들이 초기화되고 있었다. 앱을 다시 실행하더라도 메모가 저장되어있게 하고싶었다. 팀원과 코어데이터를 사용하기로 했다.
    
    - CRUD를 구현하였다.
    
    ``` swift
    func read() {
        do {
            self.list = try context.fetch(Memo.fetchRequest())
        }
        catch {}
    }
    
    func create(text: String?) {
        guard let text = text else { return }
        let newTitle = spiltText(text: text).title
        let newContents = spiltText(text: text).contents
        let newMemo = Memo(context: context)
        newMemo.title = newTitle
        newMemo.contents = newContents
        newMemo.lastModifiedDate = Date()
        
        do {
            try context.save()
            read()
        }
        catch {}
    }
    
    func update(memo: Memo?, text: String?) {
        guard let memo = memo else { return }
        guard let text = text else { return }
        let updatedTitle = spiltText(text: text).title
        let updatedContents = spiltText(text: text).contents
        
        memo.title = updatedTitle
        memo.contents = updatedContents
        memo.lastModifiedDate = Date()
        
        do {
            try context.save()
            read()
        }
        catch {}
    }
    
    func delete(memo: Memo?) {
        guard let memo = memo else { return }
        context.delete(memo)
        
        do {
            try context.save()
            read()
        }
        catch {}
    }
    ```

### Action Sheet
- 삭제와 공유하는 버튼을 만들어주었다.
    
    <img src = "https://user-images.githubusercontent.com/50835836/120177591-8e3ea680-c243-11eb-8abf-470d2001a1bf.gif" alt = "Action Sheet Video" width = "590" height = "295">
    
    - 처음 더보기 버튼을 누르면 어떤일을 수행할 지, 액션 시트를 통해서 결정하게된다.
    
    - 메모를 삭제할 때, 경각심을 높이기위해 alert창으로 한번 더 물어본다.
    
    ``` swift
    @objc private func didTapEllipsisButton() {
        let sheet = UIAlertController(title: nil, message: nil, preferredStyle: .actionSheet)
        sheet.addAction(UIAlertAction(title: "Cancel", style: .cancel, handler: nil))
        sheet.addAction(UIAlertAction(title: "Share...", style: .default, handler: { _ in
            self.didTapShareButton()
        }))
        sheet.addAction(UIAlertAction(title: "Delete", style: .destructive, handler: { _ in
            self.didTapCheckDeleteButton()
        }))
        self.present(sheet, animated: true )
    }
    
    private func didTapCheckDeleteButton() {
        let alret = UIAlertController(title: "진짜요?", message: "정말로 삭제하시겠어요?", preferredStyle: .alert)
        alret.addAction(UIAlertAction(title: "취소", style: .cancel, handler: nil))
        alret.addAction(UIAlertAction(title: "삭제", style: .destructive, handler: { _ in
            self.didTapDeleteButton()
        }))
        self.present(alret, animated: true)
    }
    
    private func didTapDeleteButton() {
        guard let index = index else { return }
        let memo = MemoData.shared.list[index]
        MemoData.shared.delete(memo: memo)
        self.navigationController?.popViewController(animated: false)
        self.detailViewDelegate?.didDeleteMemo()
    }
    ```

