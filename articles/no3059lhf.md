---
layout: default
title: (unrecognied function)(FIXME!)
---
[Top](../index.html)

--- 
### 定義場所(file name)
hotspot/src/share/vm/interpreter/templateTable.cpp

### 名前(function name)
```
void TemplateTable::def(Bytecodes::Code code, int flags, TosState in, TosState out, void (*gen)(), char filler) {
```

### 本体部(body)
```
  {- -------------------------------------------
  (1) (assert)
      ---------------------------------------- -}

	  assert(filler == ' ', "just checkin'");

  {- -------------------------------------------
  (1) 引数違いの TemplateTable::def() を呼ぶだけ
      ---------------------------------------- -}

	  def(code, flags, in, out, (Template::generator)gen, 0);
	}
	
```


