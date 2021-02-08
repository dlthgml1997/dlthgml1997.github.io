---
title: "[안드로이드] 해시 키 얻어오기 - Kotlin"
date: 2020-08-14 21:23:00
tags: 안드로이드
---



안드로이드 스튜디오에서 코드를 통해 해시 키를 얻어올 수 있다.

"package name"에 프로젝트 패키지 네임을 넣고 실행하면 로그에 해시키가 찍힌다.

```kotlin
 override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        try {     // 해시키
            val info = packageManager.getPackageInfo("package name", PackageManager.GET_SIGNATURES)
            for (signature in info.signatures) {
                val md = MessageDigest.getInstance("SHA")
                md.update(signature.toByteArray())
                val sign = Base64.encodeToString(md.digest(), Base64.DEFAULT)
                Log.e("hash key TAG", "hash key : $sign")
                //Toast.makeText(getApplicationContext(),sign,     Toast.LENGTH_LONG).show();
            }
        } catch (e: PackageManager.NameNotFoundException) {
            Log.e("hash key TAG", "error: $e")
        } catch (e: NoSuchAlgorithmException) {
            Log.e("hash key TAG", "error: $e")
        }
    }
```

