---
layout: default
title: (unrecognied function)(FIXME!)
---
[Top](../index.html)

--- 
### 定義場所(file name)
hotspot/src/share/vm/services/memoryManager.cpp

### 名前(function name)
```
GCMemoryManager* MemoryManager::get_parnew_memory_manager() {
```

### 本体部(body)
```
  {- -------------------------------------------
  (1) 新しい ParNewMemoryManager のインスタンスを作ってリターンするだけ.
      ---------------------------------------- -}

	  return (GCMemoryManager*) new ParNewMemoryManager();
	}
	
```

