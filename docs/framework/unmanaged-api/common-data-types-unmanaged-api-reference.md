---
title: "共有のデータ型 (アンマネージ API リファレンス) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "reference"
dev_langs: 
  - "C++"
ms.assetid: e4ab2c4c-9433-4eba-9e9a-096de406cafb
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# 共有のデータ型 (アンマネージ API リファレンス)
このトピックでは、C\/C\+\+ `typedef` ステートメントで定義される .NET Framework のアンマネージ API で使用する、簡単なデータ型について示します。 これらのデータ型は通常、C\/C\+\+ のプリミティブ データ型のエイリアスです。 一般的にこれらのデータ型の値は不透明です。これらのデータ型の値は他の関数またはメソッドに対して変更なしで渡せるように、特定の関数またはメソッドによって返されるためです。  
  
|データ型|定義|定義されている場所|説明|  
|----------|--------|---------------|--------|  
|AppDomainID|`typedef UINT_PTR AppDomainID;`|corprof.h|アプリケーション ドメインの識別子。|  
|AssemblyID|`typedef UINT_PTR AssemblyID;`|corprof.h|アセンブリの識別子。|  
|ClassID|`typedef UINT_PTR ClassID;`|corprof.h|マネージ クラスの識別子。|  
|CONNID|`typedef DWORD CONNID;`|cordebug.h、mscoree.h|Microsoft SQL Server のインスタンスへ接続されるスレッドの接続識別子。|  
|ContextID|`typedef UINT_PTR ContextID;`|corprof.h|特定のマネージ スレッドに関連付けられているコンテキストの識別子。|  
|COR\_PRF\_ELT\_INFO|`typedef UINT_PTR COR_PRF_ELT_INFO;`|corprof.h|特定のスタック フレームに関する情報を表す不透明なハンドル。|  
|COR\_PRF\_FRAME\_INFO|`typedef UINT_PTR COR_PRF_FRAME_INFO;`|corprof.h|スタック フレームを指す不透明なハンドル。 これは、自身が渡されるコールバックの間のみ有効です。|  
|CORDB\_ADDRESS|`typedef ULONG64 CORDB_ADDRESS;`|cordebug.h|メモリ内アドレス。|  
|CORDB\_CONTINUE\_STATUS|`typedef DWORD CORDB_CONTINUE_STATUS;`|cordebug.h|継続状態。|  
|CORDB\_REGISTER|`typedef ULONG64 CORDB_REGISTER;`|cordebug.h|CPU レジスタの値。|  
|FunctionID|`typedef UINT_PTR FunctionID;`|corprof.h|関数またはメソッドの識別子。|  
|GCHandleID|`typedef UINT_PTR GCHandleID;`|corprof.h|ガベージ コレクション ハンドル。|  
|mdToken|`typedef UINT32 mdToken;`|corprof.h|メタデータ トークン \(メタデータ テーブル内の行\)。|  
|ModuleID|`typedef UINT_PTR ModuleID;`|corprof.h|アセンブリ モジュールの識別子。|  
|ObjectID|`typedef UINT_PTR ObjectID;`|corprof.h|オブジェクトの識別子。|  
|ProcessID|`typedef UINT_PTR ProcessID;`|corprof.h|マネージ プロセスの識別子。|  
|ReJITID|`typedef UINT_PTR ReJITID;`|corprof.h|JIT コンパイルされた関数の識別子。|  
|TASKID|`typedef UINT64 TASKID;`|cordebug.h、mscoree.h|[ICLRTask](../../../ocs/framework/unmanaged-api/hosting/iclrtask-interface.md) インスタンスの識別子。|  
|ThreadID|`typedef UINT_PTR ThreadID;`|corprof.h|マネージ スレッドの識別子。|  
  
## 参照  
 [アンマネージ API リファレンス](../../../docs/framework/unmanaged-api/index.md)