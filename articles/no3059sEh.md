---
layout: default
title: (unrecognied function)(FIXME!)
---
[Top](../index.html)

--- 
### 定義場所(file name)
hotspot/src/cpu/x86/vm/assembler_x86.cpp

### 名前(function name)
```
void MacroAssembler::sign_extend_byte(Register reg) {
```

### 本体部(body)
```
  {- -------------------------------------------
  (1) コード生成:
      * movsbl 命令が使える環境の場合:
        「movsbl(movsx) 命令を使う」
      * そうではない場合:
        「shll(shl) で 24bit 左シフトした後, sarl(sar) で上位 32bit を 0 クリアしながら 24bit 算術右シフト」
      ---------------------------------------- -}

	  if (LP64_ONLY(true ||) (VM_Version::is_P6() && reg->has_byte_register())) {
	    movsbl(reg, reg); // movsxb
	  } else {
	    shll(reg, 24);
	    sarl(reg, 24);
	  }
	}
	
```


