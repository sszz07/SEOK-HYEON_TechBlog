# LiveData 나오게 된 배경
## LiveData란?
LiveData란 jetapck 라이브러리중 하나입니다 그리고 데이터를 관찰하고 관리를 해주는 data Holder 클래스 입니다 data Holder란 데이터를 저장 및 업데이트를 해줍니다 Livedata는 액티비티 프래그먼트 서비스등 생명주기를 인식을 해서 데이터 관찰을 합니다 생명주기를 인식한다는 것은 앱의 활성상태를 의미하는데 활성상태는 STARTED 또는 RESUMED를 의미합니다 LiveData는 STARTED 또는 RESUMED일때 ui 업데이트를 하게 됩니다


## LiveData 탄생 배경
jetpack의 본질은 개발자가 쉽고 빠르고 안전한 앱을 만들기 원했습니다 간단한 예를들기 위해 LiveData와 많이 비교하는 Obserable이 있습니다 Obserable은 ReactiveX(Reactive Extensions)를 자바와 코틀린으로 구현한 Rxjava와 RxKotiln으로 만든 비동기 처리하는 라이브러리 입니다 ReactiveX의 Obserable은 러닝커브가 높습니다 이유는 Rxjava와 RxKotiln의 함수형  map(), filter(), reduce(), flatMap()을 공부하고 익숙하지 않은 Rxjava와 RxKotiln 디버깅, 흐름 제어를 공부해야 합니다
밑에 있는 코드는 안드로이드 LiveData 공식문서에서 퍼왔습니다 LiveData가 옵저버 함수를 만들고 ui 업데이트 하는 과정입니다 물론 밑에 있는 코드 만으로는 완성할수는 없지만 밑에 코드는 80% 완성입니다 복잡한 함수가 없는것을 볼수 있습니다

```java
class NameActivity : AppCompatActivity() {

    // Use the 'by viewModels()' Kotlin property delegate
    // from the activity-ktx artifact
    private val model: NameViewModel by viewModels()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        // Other code to setup the activity...

        // Create the observer which updates the UI.
        val nameObserver = Observer<String> { newName ->
            // Update the UI, in this case, a TextView.
            nameTextView.text = newName
        }

        // Observe the LiveData, passing in this activity as the LifecycleOwner and the observer.
        model.currentName.observe(this, nameObserver)
    }
}
```
---  
</br>

# LiveData는 어떤 문제를 해결해주는가?
## LiveData 나오기전 문제점
1)코드상태 복잡- 과거에는 ui 컴포넌트에 데이터가 자동으로 업데이트가 되지 않아서 따로 컨트롤러와 프레젠터를 만들어서 업데이트를 해줬습니다 그렇게 되면 작업시간이 상승하고 코드의 양도 늘어나게 되었습니다

2)생명주기 비호환성- 액티비티와 프래그먼트는 특정 시점에 파괴되고 생성이 됩니다 Obserable과 비교하면 Obserable는 일반적으로 액티비티 프래그먼트 서비스등 생명주기를 고려하지 않고 데이터 수신할 준비합니다 예를들어 사용하지도 않는 액티비티를 계속 확인하면서 데이터 준비를 하는데 이는 리소스 낭비를 하게 됩니다

3)단일 라이브러리 단점- 안드로이드는 support 라이브러리로 많은 함수를 지원 했습니다 support 라이브러리란 API레벨 13 이상에서 사용 가능한 3만 여개의 함수를 지원해 주는 단일 라이브러리 입니다 단일 여기서 단일 라이브러리가 주는 단점이 있습니다 예를 들어 뷰페이저라는 함수를 사용하고 싶은데 원치 않는 다른 함수까지 업데이트가 됩니다 앱의 규모가 커지면 라이브러리 내의 많은 함수 때문에 용량이 커집니다 안드로이드는 기본적으로 APK당 하나의 DEX파일을 사용하기 때문에 64K 이내의 용량을 사용해야 합니다 dex파일이란 런타임시 실행되는 실코드 를 의미 합니다


## LiveData로 문제 해결
1)MVVM패턴 뷰모델과 livedata를 사용한 간결한 코드
MVVM 패턴은 로직의 독립성을 강조 합니다 뷰=UI 업데이트 로직 뷰모델=데이터 가공 모델=비즈니스 로직 형태로 각각 역할이 있습니다 LiveData는 뷰모델에 속하며 UI에 데이터 바인딩을 할수 있게 데이터를 가공하고 자동으로 ui 업데이트를 하게 됩니다 또한 LiveData를 통해 각각 View에 종속되지 않습니다 1개의 뷰에 1개의 뷰모델을 사용하지 않는다는 의미입니다 이렇게 되면 여러개의 view에 하나의 LiveData로 역할이 가능하고 간결한 코드로 만들어 집니다


2)Observer 패턴과 Lifecyle owner를 활용한 앱 안전성
LiveData는 데이터를 관찰 할 수 있는 데이터 홀더 클래스 입니다 그럼 어떻게 데이터를 관찰할까요? Observer 패턴을 이용해서 관찰을 합니다 Observer 패턴란 LiveData에서 데이터 업데이트 되면 Observer 객체에게 알립니다 그 다음 Observer 객체는 최신 데이터로 ui 업데이트를 하게 됩니다 그리고 Lifecyle owner로 앱의 생명주기 파악이 됩니다 LiveData가 가진 큰 장점 입니다 예를들어 백스텍에 있는 액티비티가 종료가 되어서 stop이 되었을때 Lifecyle owner로 상태 확인을 합니다 확인하게 되면 백스텍에 있는 액티비티와 충돌을 일어나지 않습니다 이유는 액티비티가 stop이 되면 자동으로 LiveData와 Observer 객체는 비활성이 됩니다 그래서 불필요한 흐름이 없어지니 메모리 효율에서도 좋게 됩니다

---  
</br>

# StateFlow 나오게 된 배경
## StateFlow란?
StateFlow 알기 위해서 Flow를 먼저 알아야 합니다 Flow는 코루틴 기반으로 비동기식을 값을 제어하는 반응형 스트림 입니다 즉 StateFlow는 코루틴의 Flow api에서 제공하는 Flow 종류 중 하나 입니다 Stateflow는 상태 관리에 최적화된 Hot Stream 입니다 Hot Stream이란 항상 최신 상태를 보유하며 상태가 변경되는 데이터 스트림 도구 입니다


## StateFlow 탄생 배경
코루틴은 여러개의 태스크가 하나의 프로세스에서 동작 할수 있는 동시성 프로그래밍 입니다 코루틴을 먼저 설명한 이유는 StateFlow가 코루틴 기반이기 때문입니다(여기까지 진행 했습니다!!!)  

---  
</br>

# StateFlow는 어떤 문제를 해결해 주는가?
## LiveData의 한계
LiveData의 한계는 안드로이드 클린 아키텍처 관점에서 보겠습니다 안드로이드 클린 아키텍처는 Presentation layer, Domain layer, Data layer로 구성이 되어 있습니다 LiveData는 UI의 상태에 집중하기 위해 만들었습니다. 값의 변화는 항상 메인 쓰레드를 통해 관리를 합니다. Data Layer에서 비동기 방식으로 데이터를 저장하고 처리하기에 메인 스레드에서 동작하는 LiveData는 맞지 않습니다. 또한 LiveData는 안드로이드 플랫폼에 속해있는 있으면 클린 아카텍처 에서는 불편 한 문제 일수 있습니다. 이유는 Domain layer에서는 플랫폼과 연관이 없는 계층 입니다. LiveData는 Presentation에 속해 있는데 클린 아키텍처 구조는 
Presentation-> Domain 단방향으로 움직입니다. 그래서 Domain layer는 플랫폼과 관련이 없고 repository, model, usecase를 이용해서 순수 자바와 코틀린으로 작업을 하는 계층입니다. 

## StateFlow로 문제 해결 방법


### StateFlow 단점은 없을까?
