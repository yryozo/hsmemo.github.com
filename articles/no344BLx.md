---
layout: default
title: (unrecognied function)(FIXME!)
---
[Top](../index.html)

--- 
### 定義場所(file name)
hotspot/src/share/vm/gc_implementation/parallelScavenge/psVirtualspace.cpp

### 名前(function name)
```
bool PSVirtualSpaceHighToLow::expand_by(size_t bytes) {
```

### 本体部(body)
```
  {- -------------------------------------------
  (1) (assert)
      ---------------------------------------- -}

	  assert(is_aligned(bytes), "arg not aligned");
	  DEBUG_ONLY(PSVirtualSpaceVerifier this_verifier(this));
	
  {- -------------------------------------------
  (1) もしまだ commit できるサイズよりも拡張を要求されたサイズの方が大きければ, expand_by は失敗 (ここでリターン)
      ---------------------------------------- -}

	  if (uncommitted_size() < bytes) {
	    return false;
	  }
	
  {- -------------------------------------------
  (1) special() であれば既に全ての領域が commit 済みなので何もしない.
      (See: )
      special() でなければ, os::commit_memory() で必要なサイズ分 commit を行う.
      ---------------------------------------- -}

	  char* const base_addr = committed_low_addr() - bytes;
	  bool result = special() || os::commit_memory(base_addr, bytes, alignment());

  {- -------------------------------------------
  (1) os::commit_memory() を実行して失敗した場合以外は, _committed_high_addr フィールドをサイズ分増加させる.
      ---------------------------------------- -}

	  if (result) {
	    _committed_low_addr -= bytes;
	  }
	
  {- -------------------------------------------
  (1) 結果をリターン
      ---------------------------------------- -}

	  return result;
	}
	
```


