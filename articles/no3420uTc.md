---
layout: default
title: (unrecognied function)(FIXME!)
---
[Top](../index.html)

--- 
### 定義場所(file name)
hotspot/src/share/vm/gc_implementation/g1/g1OopClosures.hpp

### 名前(function name)
```
  FilterAndMarkInHeapRegionAndIntoCSClosure(G1CollectedHeap* g1,
                                            OopsInHeapRegionClosure* oc,
                                            ConcurrentMark* cm)
```

### 本体部(body)
```
  {- -------------------------------------------
  (1) フィールドの初期化
      ---------------------------------------- -}

	  : _g1(g1), _oc(oc), _cm(cm) { }
	
```


