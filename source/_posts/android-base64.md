---
title: "[안드로이드] byte Array to String (Base 64를 이용하여 encoding, decoding 시 주의할 점!) - 자바/JAVA"
date: 2020-08-24 01:00:00
tags: 안드로이드
---

## Base64

일단 Base64가 뭘까? 컴퓨터 분야에서 쓰이는 **Base64**란 8비트 이진 데이터를 문자 코드에 영향을 받지 않는 공통 ASCII 영역의 문자들로만 이루어진 일련의 문자열로 바꾸는 인코딩 방식을 가리키는 개념이라고 한다. 

**Encoding** 은 이진데이터를 일련의 문자열로, **Decoding** 은 일련의 문자열을 이진데이터로 바꾸는 것이다.



## encodToString

```java
public static String encodeToString (byte[] input, int flags)
```

Base64를 이용하여 byte Array 를 String으로 Encoding 할 때 이용하는 함수이다.

나는 text를 private key로 디지털 서명한 byte[] 값을 서버에 String 형식으로 보내야하기 때문에 사용했다.

```java
    public String getDigitalSignature(String packageName, String text) {
        try{
            Signature signature = Signature.getInstance(SIGNATURE_ALGORITHM);
            signature.initSign(getPrivateKey(packageName));

            byte[] data = text.getBytes();
            signature.update(data);

            byte[] signatureBytes = signature.sign();
            String signatureStr = Base64.encodeToString(signatureBytes, Base64.NO_WRAP);
            Log.d(TAG, "Signature:" + signatureStr);
            return signatureStr;
        } catch (NoSuchAlgorithmException | InvalidKeyException | SignatureException e) {
            Log.e(TAG, "error in digital signature" + e);
            return null;
        }
    }
```

signatureBytes 를 변형 없이 encoding 하기 위해 Base64.NO_WRAP 옵션을 사용하는 것이 좋다. 왜일까?



>  여기서 주의할 점이 나온다 ! 

긴 길이의 byte 배열의 경우, 

* **Base64.Default**

  ```
  Default values for encoder/decoder flags.
  Constant Value: 0
  ```

  위는 android developers 레퍼런스 설명이다. default 옵션으로, 이 옵션의 경우 76자가 넘는 위치에 개행문자(\n)가 삽입된다. 

  * **예시** 

    ```java
    String signatureStr = Base64.encodeToString(signatureBytes, Base64.DEFAULT);
    Log.d(TAG, "Signature:" + signatureStr);
    ```

    **결과** -> 세보진 않았지만 76자 마다 개행문자가 삽입되는 것을 확인할 수 있다.

    ![2020-08-242.10.47](../image/2020-08-242.10.47.png)

* **Base64.NO_WRAP**

  ```
  Encoder flag bit to omit all line terminators (i.e., the output will be on one long line).
  Constant Value: 2 
  ```

  즉, 개행문자를 삽입하지 않고 긴 한줄의 output 을 갖는다.

  * **예시**

    ```java
    String signatureStr = Base64.encodeToString(signatureBytes, Base64.NO_WRAP);
    Log.d(TAG, "Signature:" + signatureStr);
    ```

    **결과** -> 끊김 없이 한 줄로 나오는 것을 확인할 수 있다.

    ![2020-08-242.07.26](../image/2020-08-242.07.26.png)

* 이 외에도, **CRLF / NO_CLOSE / NO_PADDING / URL_SAFE** 옵션이 있다.

  

> publicKey 를 서버로 전송하는 경우에는 DEFAULT 옵션을 사용하여야 했다.
>
> 때에 따라서 알맞은 옵션을 사용하도록 하자 ! 



마지막으로 ! decoding 시에도 동일한 옵션을 사용해 주어야 한다. 나 같은 경우에는 아래와 같은 코드를 이용했다 (NO_WRAP)

```java
 Base64.decode(signatureStr, Base64.NO_WRAP);
```



출처: https://kjwsx23.tistory.com/234 