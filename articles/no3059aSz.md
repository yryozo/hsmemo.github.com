---
layout: default
title: (unrecognied function)(FIXME!)
---
[Top](../index.html)

--- 
### 定義場所(file name)
hotspot/src/share/vm/prims/jni.cpp

### 名前(function name)
```
JNI_ENTRY(void, jni_CallStaticVoidMethod(JNIEnv *env, jclass cls, jmethodID methodID, ...))
```

### 本体部(body)
```
  {- -------------------------------------------
  (1) (デバッグ用の処理)
      (See: JNIWrapper)
      ---------------------------------------- -}

	  JNIWrapper("CallStaticVoidMethod");

  {- -------------------------------------------
  (1) (DTrace のフック点)
      ---------------------------------------- -}

	  DTRACE_PROBE3(hotspot_jni, CallStaticVoidMethod__entry, env, cls, methodID);

  {- -------------------------------------------
  (1) (DTrace のフック点)(リターン用) (See: DT_RETURN_MARK)
      ---------------------------------------- -}

	  DT_VOID_RETURN_MARK(CallStaticVoidMethod);
	
  {- -------------------------------------------
  (1) 可変長引数を JNI_ArgumentPusherVaArg オブジェクトに詰め直した後, 
      jni_invoke_static() を呼んで実際の呼び出し処理を行う.
      ---------------------------------------- -}

	  va_list args;
	  va_start(args, methodID);
	  JavaValue jvalue(T_VOID);
	  JNI_ArgumentPusherVaArg ap(methodID, args);
	  jni_invoke_static(env, &jvalue, NULL, JNI_STATIC, methodID, &ap, CHECK);
	  va_end(args);
	JNI_END
	
```


