---
layout: default
title: (unrecognied function)(FIXME!)
---
[Top](../index.html)

--- 
### 定義場所(file name)
hotspot/src/share/vm/prims/jvmtiRawMonitor.cpp

### 名前(function name)
```
int JvmtiRawMonitor::raw_notify(TRAPS) {
```

### 本体部(body)
```
  {- -------------------------------------------
  (1) (トレース出力)
      ---------------------------------------- -}

	  TEVENT (raw_notify) ;

  {- -------------------------------------------
  (1) カレントスレッドがロックを持っていなければ, ここでリターン (OM_ILLEGAL_MONITOR_STATE).
      ---------------------------------------- -}

	  if (THREAD != _owner) {
	    return OM_ILLEGAL_MONITOR_STATE;
	  }

  {- -------------------------------------------
  (1) JvmtiRawMonitor::SimpleNotify() を呼んで待機しているスレッドを起床させる.
      ---------------------------------------- -}

	  SimpleNotify (THREAD, false) ;
	  return OM_OK;
	}
	
```


