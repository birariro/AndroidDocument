# Context 전역으로 사용하기
Context는 Application 에서만 사용할수있지만 <br/>
만약 일반 Class 에서 Context를 사용하고싶을때는 전역으로 빼두고 사용할수있다. <br/>
이 방법은 좋은 방법이 아니라 생각하지만 경우에따라 사용하게될수도 있을것이다. <br/>

```kotlin
object RetrofitClient {
    private  var retrofitClient: Retrofit?=null

    fun getClient(baseUrl:String):Retrofit?{
		Toast.makeText(this,"호출 성공",Toast.LENGTH_SHORT).show()
	}
}
```
위와같이 object 에서 Toast를 하려고 해도 사용할수가없다.  <br/>
Context를 사용할수없는 상황이라 이러한 경우가 발생을 하게되는데  <br/> <br/>

따라서 Context를 사용할수있게 전역으로 배치 해볼것이다.  <br/>

패키지 최상단에  <br/>
App.class 파일을 하나 생성할것이다.  <br/>
```kotlin
class App : Application() {
    companion object{
        lateinit var instance:App
            private set
    }

    override fun onCreate() {
        super.onCreate()
        instance = this
    }
}
```
생성자를 통해 instance 에 this 를 넣게되고

manfiest 에서
```kotlin
<application
        android:name=".App"
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.RetrofitApp">
```
위와같이 application name 에 위에서 만든 App파일을 지정한다.  <br/>


```kotlin
object RetrofitClient {
    private  var retrofitClient: Retrofit?=null

    fun getClient(baseUrl:String):Retrofit?{
		Toast.makeText(App.instance,"호출 성공",Toast.LENGTH_SHORT).show()
	}
}
```
위와같이 전역 context를 사용할수있다.
