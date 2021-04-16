## 요구사항
앱의 기능중에 친구에게 공유하기 기능으로<br/>
카카오톡 , 페이스북 기타 메신저에 해당앱을 공유하는 기능을 추가해야한다.<br/>

## 구현
```
<string name="sharingText">이 앱을 추천합니다!\n\nhttps://play.google.com/store/apps/details?id=PackageName/string>
```
플레이스토어에서 해당앱의 링크를 공유해야한다.
위와같은 링크 구조를 가지고있으며 마지막에는 해당 앱의 패키지 명이들어간다.
패키지명은 AndroidManifest.xml 에서 확인 가능.

```
var intent = Intent.createChooser( Intent(Intent.ACTION_SEND).apply {
	type = "text/plain"
	putExtra(Intent.EXTRA_TEXT,getString(R.string.sharingText))
},"공유하기")
startActivity(intent)
```
끝
