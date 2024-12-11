# LiveData 나오게 된 배경
## LiveData란?
LiveData란 개발자가 쉽고 편리하고 안정적인 앱을 만들기 위한 jetapck 라이브러리중 하나입니다 그리고 데이터를 관찰하고 관리를 해주는 data Holder 클래스 입니다 data Holder란 데이터를 저장하고 데이터를 업데이트를 해줍니다 일반적인 Obserable이라는 인터페이스와 비교를 하는데 Obserable는 앱의 생명주기를 인식을 할수 없습니다 그래서 액티비티가 종료가 되었는데도 Obserable는 데이터 관찰를 계속해서 리소스 낭비하게 됩니다 그와 달리 Livedata는 액티비티 프래그먼트 서비스등 생명주기를 인식을 해서 데이터 관찰을 합니다 생명주기를 인식한다는 것은 LiveData가 활성상태일때 데이터 업데이트 한다는 의미입니다 또한 활성상태란 STARTED 또는 RESUMED를 의미합니다 생명주기를 인식해서 STARTED 또는 RESUMED일때 ui 업데이트를 하게 됩니다



## LiveData 탄생 배경
jetpack의 본질은 개발자가 쉽고 빠르고 안전한 앱을 만들기 원했습니다 간단한 예를들기 위해 LiveData와 많이 비교하는 Obserable이 있습니다 Obserable은 ReactiveX(Reactive Extensions)를 자바와 코틀린으로 구현한 Rxjava와 RxKotiln으로 만든 라이브러리 입니다 Obserable은 진입장벽이 높습니다 진입 장벽이 높은 이유는 Rxjava와 RxKotiln의 기본 함수형이 있는데  map(), filter(), reduce(), flatMap()을 공부하고 디버깅, 흐름 제어 함수도 공부 해야합니다
밑에는 구글 공식문서에서 퍼왔습니다 LiveData가 옵저버 함수를 만들고 ui 업데이트 하는 과정인데 ui업데이트는 90% 완성입니다

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
## LiveData 나오기전 불편했던 점


## LiveData 장단점


---  
</br>

# StateFlow 나오게 된 배경
## StateFlow란?
## StateFlow 탄생 배경

---  
</br>

# StateFlow는 어떤 문제를 해결해 주는가?
## LiveData의 한계
## StateFlow 장단점
