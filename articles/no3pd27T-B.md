---
layout: default
title: ASPSYoungGen クラス 
---
[Top](../index.html)

#### ASPSYoungGen クラス 



---
## <a name="noDTX0201n" id="noDTX0201n">ASPSYoungGen</a>

### 概要(Summary)
ParallelScavengeHeap 使用時において, New Generation の管理を担当するクラスの 1つ (See: [here](no3718kvd.html) for details).

このクラスは, UseAdaptiveGCBoundary オプションが指定されている場合用 
(= GC Ergonomics を用いた動的領域サイズ調整を行う場合用) (See: PSYoungGen).


```
    ((cite: hotspot/src/share/vm/gc_implementation/parallelScavenge/asPSYoungGen.hpp))
    class ASPSYoungGen : public PSYoungGen {
```

### 使われ方(Usage)
#### インスタンスの格納場所(where its instances are stored)
ParallelScavengeHeap オブジェクトの _young_gen フィールドに格納されている.

(ただしこのフィールドには, ASPSYoungGen オブジェクトではなく,
スーパークラスである PSYoungGen オブジェクトが格納されることもある.
その場合にはこのクラスはどこからも使用されない.)


```
    ((cite: hotspot/src/share/vm/gc_implementation/parallelScavenge/parallelScavengeHeap.hpp))
    class ParallelScavengeHeap : public CollectedHeap {
    ...
      static PSYoungGen* _young_gen;
```

(なお, AdjoiningGenerations オブジェクトの _young_gen フィールドにも同じインスタンスが格納されている.
正確には, こちらで生成されたものが ParallelScavengeHeap のフィールドにコピーされる)


```
    ((cite: hotspot/src/share/vm/gc_implementation/parallelScavenge/adjoiningGenerations.hpp))
    class AdjoiningGenerations : public CHeapObj {
    ...
      PSYoungGen* _young_gen;
```

#### 生成箇所(where its instances are created)
AdjoiningGenerations::AdjoiningGenerations() 内で(のみ)生成されている.

(なお ASPSYoungGen オブジェクトが生成されるかどうかは UseAdaptiveGCBoundary オプションの値によって決まる.
UseAdaptiveGCBoundary オプションが指定されている場合は ASPSYoungGen が生成され, そうでない場合は PSYoungGen が生成される)


```
    ((cite: hotspot/src/share/vm/gc_implementation/parallelScavenge/adjoiningGenerations.cpp))
    AdjoiningGenerations::AdjoiningGenerations(ReservedSpace old_young_rs,
                                               size_t init_low_byte_size,
                                               size_t min_low_byte_size,
                                               size_t max_low_byte_size,
                                               size_t init_high_byte_size,
                                               size_t min_high_byte_size,
                                               size_t max_high_byte_size,
                                               size_t alignment) :
    ...
      if (UseAdaptiveGCBoundary) {
    ...
        // Place the young gen at the high end.  Passes in the virtual space.
        _young_gen = new ASPSYoungGen(_virtual_spaces.high(),
                                      _virtual_spaces.high()->committed_size(),
                                      min_high_byte_size,
                                      _virtual_spaces.high_byte_size_limit());
    ...
      } else {
    ...
        // Create the generations.  Virtual spaces are not passed in.
        _young_gen = new PSYoungGen(init_high_byte_size,
                                    min_high_byte_size,
                                    max_high_byte_size);
```




### 詳細(Details)
See: [here](../doxygen/classASPSYoungGen.html) for details

---
