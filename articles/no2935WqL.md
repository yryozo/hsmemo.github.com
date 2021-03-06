---
layout: default
title: Serviceability 機能 ： JVMTI の処理 ： JVMTI 関数の処理 ： イベント管理 (Event Management) ： 各イベントの通知処理 ： GarbageCollectionStart イベントの処理  
---
[Up](no29359PS.html) [Top](../index.html)

#### Serviceability 機能 ： JVMTI の処理 ： JVMTI 関数の処理 ： イベント管理 (Event Management) ： 各イベントの通知処理 ： GarbageCollectionStart イベントの処理  

--- 
## 概要(Summary)
(See: JVMTI 仕様)

GarbageCollectionStart イベントの処理は JvmtiGCMarker クラスによって行われる (See: JvmtiGCMarker, SvcGCMarker).

## 処理の流れ (概要)(Execution Flows : Summary)
```
(略) (See: [here](no28916sKh.html) for details)
-> VM_GenCollectForAllocation::doit()
   -> SvcGCMarker::SvcGCMarker()
      -> JvmtiGCMarker::JvmtiGCMarker()
         -> JvmtiExport::post_garbage_collection_start()
            -> (登録されているコールバックを呼び出す)

(略)
-> VM_GenCollectFull::doit()
   -> SvcGCMarker::SvcGCMarker()
      -> (同上)

(略)
-> VM_GenCollectForPermanentAllocation::doit()
   -> SvcGCMarker::SvcGCMarker()
      -> (同上)

(略)
-> CMSCollector::do_CMS_operation()
   -> SvcGCMarker::SvcGCMarker()
      -> (同上)

(略) (See: [here](no3718vrX.html) for details)
-> VM_ParallelGCFailedAllocation::doit()
   -> SvcGCMarker::SvcGCMarker()
      -> (同上)

(略) (See: [here](no2935XW2.html) for details)
-> VM_ParallelGCFailedPermanentAllocation::doit()
   -> SvcGCMarker::SvcGCMarker()
      -> (同上)

(略) (See: [here](no2935JgF.html) for details)
-> VM_ParallelGCSystemGC::doit()
   -> SvcGCMarker::SvcGCMarker()
      -> (同上)

(略)
-> ConcurrentMark::checkpointRootsFinal()
   -> SvcGCMarker::SvcGCMarker()
      -> (同上)

(略)
-> G1CollectedHeap::do_collection()
   -> SvcGCMarker::SvcGCMarker()
      -> (同上)

(略)
-> G1CollectedHeap::do_collection_pause_at_safepoint()
   -> SvcGCMarker::SvcGCMarker()
      -> (同上)
```

## 処理の流れ (詳細)(Execution Flows : Details)






