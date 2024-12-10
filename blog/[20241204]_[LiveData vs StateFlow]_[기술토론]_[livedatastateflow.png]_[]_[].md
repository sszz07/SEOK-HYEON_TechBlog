# LiveData 나오게 된 배경
## LiveData란?
LiveData란 개발자가 쉽고 편리하고 안정적인 앱을 만들기 위한 jetapck 라이브러리중 하나입니다 그리고 데이터를 관찰하고 관리를 해주는 data Holder 클래스 입니다 data Holder란 데이터를 저장하고 데이터를 업데이트를 해줍니다 일반적인 Obserable이라는 인터페이스와 비교를 하는데 Obserable는 앱의 생명주기를 인식을 할수 없습니다 그래서 액티비티가 종료가 되었는데도 Obserable는 데이터 관찰를 계속해서 리소스 낭비하게 됩니다 그와 달리 Livedata는 액티비티 프래그먼트 서비스등 생명주기를 인식을 해서 데이터 관찰을 합니다 생명주기를 인식한다는 것은 LiveData가 활성상태일때 데이터 업데이트 한다는 의미입니다 또한 활성상태란 STARTED 또는 RESUMED를 의미합니다 생명주기를 인식해서 STARTED 또는 RESUMED일때 ui 업데이트를 하게 됩니다



## LiveData 탄생 배경
LiveData가 나오기 전에는 네트워크를 통해 데이터를 가져왔고 사용자의 상호 작용으로 상태가 바뀌게 되면 
ive data 이전에는 네트워크를 통해 데이터를 가져오거나 사요자 상호작용으로 상태가 바뀌게 되면 controller나 presenter에서 ui에 일일히 값을 넣어주는 보일러 플레이트 코드가 필요했습니다. 그런 불편함을 해결해주는게 live data이고 그러니 당연히 유지보수성도 좋아지겠죠.


---  
</br>

# LiveData는 어떤 문제를 해결해주는가?
## LiveData 나오기전 문제점
## LiveData 장단점
### 생명주기를 인식하는 방법

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
