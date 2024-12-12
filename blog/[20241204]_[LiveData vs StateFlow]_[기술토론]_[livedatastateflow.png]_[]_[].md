# LiveData 나오게 된 배경
## LiveData란?
LiveData란 jetapck 라이브러리중 하나입니다 그리고 데이터를 관찰하고 관리를 해주는 data Holder 클래스 입니다 data Holder란 데이터를 저장 및 업데이트를 해줍니다 Livedata는 액티비티 프래그먼트 서비스등 생명주기를 인식을 해서 데이터 관찰을 합니다 생명주기를 인식한다는 것은 앱의 활성상태를 의미하는데 활성상태는 STARTED 또는 RESUMED를 의미합니다 LiveData는 STARTED 또는 RESUMED일때 ui 업데이트를 하게 됩니다


## LiveData 탄생 배경
jetpack의 본질은 개발자가 쉽고 빠르고 안전한 앱을 만들기 원했습니다 간단한 예를들기 위해 LiveData와 많이 비교하는 Obserable이 있습니다 Obserable은 ReactiveX(Reactive Extensions)를 자바와 코틀린으로 구현한 Rxjava와 RxKotiln으로 만든 라이브러리 입니다 Obserable은 진입장벽이 높습니다 진입 장벽이 높은 이유는 Rxjava와 RxKotiln의 기본 함수형이 있는데  map(), filter(), reduce(), flatMap()을 공부하고 익숙하지 않은 Rxjava와 RxKotiln 디버깅, 흐름 제어 함수도 공부 해야합니다
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

3)단일 라이브러리 단점- 안드로이드는 support 라이브러리로 많은 함수를 지원 했습니다 support 라이브러리란 API레벨 13 이상에서 사용 가능한 3만 여개의 함수를 지원해 주는 단일 라이브러리 입니다 단일 여기서 단일 라이브러리가 주는 단점이 있습니다 예를 들어 뷰페이저라는 함수를 사용하고 싶은데 원치 않는 다른 함수까지 업데이트가 됩니다 앱의 규모가 커지면 라이브러리 내의 많은 함수 때문에 용량이 커집니다 안드로이드는 기본적으로 APK당 하나의 DEX파일을 사용하기 때문에 64K 이내의 용량을 사용해야 합니다 dex파일이란 런타임시 실행되는 코드 입니다 밑에 있는 이미지를 보면 리소스를 많이 차지하는것을 보실수 있습니다


## LiveData로 문제 해결 방법
1)MVVM패턴 뷰모델과 livedata를 사용한 간결한 코드
MVVM 패턴은 로직의 독립성을 강조 합니다 뷰=UI 로직 뷰모델=데이터 가공  모델=비즈니스 로직 형태로 각각 역할이 있습니다 LiveData는 뷰모델에 속하며 UI에 데이터 바인딩을 할수 있게 데이터를 가공하고 ui 업데이트를 하게 됩니다
또한 LiveData를 통해 각각 View에 종속되지 않습니다 1개의 뷰에 1개의 뷰모델을 사용하지 않는다는 의미입니다 이렇게 되면 여러개의 view에 하나의 LiveData로 역할이 가능하고 간결한 코드로 만들어 집니다


2)Observer와 Lifecyleview를 활용한 앱 안전성



---  
</br>

# StateFlow 나오게 된 배경
## StateFlow란?


## StateFlow 탄생 배경


---  
</br>

# StateFlow는 어떤 문제를 해결해 주는가?
## LiveData의 한계


## StateFlow로 문제 해결 방법


### StateFlow 단점은 없을까?
