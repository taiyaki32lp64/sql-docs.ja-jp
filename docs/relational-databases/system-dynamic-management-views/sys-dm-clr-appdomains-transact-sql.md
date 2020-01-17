---
title: sys.dm_clr_appdomains (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_clr_appdomains
- sys.dm_clr_appdomains
- dm_clr_appdomains_TSQL
- sys.dm_clr_appdomains_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_appdomains dynamic management dynamic management view
ms.assetid: 9fe0d4fd-950a-4274-a493-85e776278045
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3ebcda61d95cc5131048ab32701d9d68228646ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138409"
---
# <a name="sysdmclrappdomains-transact-sql"></a>sys.dm_clr_appdomains (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  サーバー内のアプリケーション ドメインごとに 1 行のデータを返します。 アプリケーション ドメイン (**AppDomain**) 内の構造では、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]アプリケーションの分離の単位である共通言語ランタイム (CLR)。 このビューを使用するには理解やトラブルシューティングで実行されている CLR 統合オブジェクトに[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
 CLR 統合マネージド データベース オブジェクトにはいくつかの種類があります。 これらのオブジェクトについては、次を参照してください。[共通言語ランタイム (CLR) 統合によるデータベース オブジェクトの構築](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)します。 これらのオブジェクトが実行されるたびに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]作成、 **AppDomain**下をロードして、必要なコードを実行します。 分離レベル、 **AppDomain**は 1 つ**AppDomain**データベースごとに所有者。 ユーザーによって所有されているすべての CLR オブジェクトは常に同じ実行は、 **AppDomain**データベースごと (場合、ユーザーは、CLR データベース オブジェクトが別のアプリケーション ドメインで実行が別のデータベース内の CLR データベース オブジェクトを登録)。 **AppDomain**コードの実行が終了した後は破棄されません。 代わりに、以降の実行に備えて、メモリ内にキャッシュされます。 これにより、パフォーマンスが向上します。  
  
 詳細については、次を参照してください。[アプリケーション ドメイン](https://go.microsoft.com/fwlink/p/?LinkId=299658)します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**appdomain_address**|**varbinary(8)**|アドレス、 **AppDomain**します。 すべての管理対象のデータベース ユーザーが所有するオブジェクトが同じで常に読み込まれます**AppDomain**します。 この列を使用するにはこれで現在読み込まれているすべてのアセンブリを検索する**AppDomain**で**sys.dm_clr_loaded_assemblies**します。|  
|**appdomain_id**|**int**|ID、 **AppDomain**します。 各**AppDomain**が一意の id。|  
|**appdomain_name**|**varchar(386)**|名前、 **AppDomain**によって割り当てられた[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。|  
|**creation_time**|**datetime**|時刻、 **AppDomain**が作成されました。 **Appdomain**はキャッシュされ、パフォーマンスの向上のため、再利用**creation_time**コードが実行された時間とは限りません。|  
|**db_id**|**int**|このデータベースの ID **AppDomain**が作成されました。 いずれか 2 つの異なるデータベースに格納されているコードを共有できません**AppDomain**します。|  
|**user_id**|**int**|このオブジェクトが実行できるユーザーの ID **AppDomain**します。|  
|**state**|**nvarchar(128)**|現在の状態の記述子を**AppDomain**します。 AppDomain には作成から削除まで、さまざまな状態があります。 詳細については、このトピックの「解説」を参照してください。|  
|**strong_refcount**|**int**|強参照の数**AppDomain**します。 これは、現在これを使用するバッチの実行の数を反映して**AppDomain**します。 このビューの実行を作成します、**強力な参照カウント**場合でも、現在実行中のコードがない**strong_refcount** 1 の値になります。|  
|**weak_refcount**|**int**|弱参照数**AppDomain**します。 これは、内部オブジェクトの数を示します、 **AppDomain**キャッシュされます。 マネージ データベース オブジェクトを実行するときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]キャッシュ内で、 **AppDomain**後で再利用します。 これにより、パフォーマンスが向上します。|  
|**cost**|**int**|コスト、 **AppDomain**します。 コストが高くこの**AppDomain**がメモリ不足でアンロードされます。 コストは通常、メモリの量がこれを再作成に必要な異なります**AppDomain**します。|  
|**value**|**int**|値、 **AppDomain**します。 値が低いほどより高いこの**AppDomain**がメモリ不足でアンロードされます。 値は通常、接続またはバッチの数を使用しているこの異なります**AppDomain**します。|  
|**total_processor_time_ms**|**bigint**|プロセスの開始後、現在のアプリケーション ドメインでの実行中にすべてのスレッドによって使用された、ミリ秒単位の合計プロセッサ時間です。 これに相当**System.AppDomain.MonitoringTotalProcessorTime**します。|  
|**total_allocated_memory_kb**|**bigint**|アプリケーション ドメインの作成後、それによって行われたすべてのメモリ割り当ての、KB 単位の合計サイズです。収集されたメモリ量も差し引かれません。 これに相当**System.AppDomain.MonitoringTotalAllocatedMemorySize**します。|  
|**survived_memory_kb**|**bigint**|最後の完全なブロッキング コレクションで残った、現在のアプリケーション ドメインによって参照されていることが判明しているキロバイト数です。 これに相当**System.AppDomain.MonitoringSurvivedMemorySize**します。|  
  
## <a name="remarks"></a>コメント  
 1 つであるリレーションシップがあります**dm_clr_appdomains.appdomain_address**と**dm_clr_loaded_assemblies.appdomain_address**します。  
  
 以下にリストの可能な限り**状態**値、その説明で発生したときと、 **AppDomain**ライフ サイクルです。 ライフ サイクルを次にこの情報を使用することができます、 **AppDomain**疑わしい点または繰り返し発生するを監視する**AppDomain**インスタンスがアンロード中で、Windows イベント ログを解析する必要はありません。  
  
## <a name="appdomain-initialization"></a>AppDomain の初期化  
  
|状態|説明|  
|-----------|-----------------|  
|E_APPDOMAIN_CREATING|**AppDomain**が作成されています。|  
  
## <a name="appdomain-usage"></a>AppDomain の使用状況  
  
|状態|説明|  
|-----------|-----------------|  
|E_APPDOMAIN_SHARED|ランタイム**AppDomain**が複数のユーザーが使用できる状態です。|  
|E_APPDOMAIN_SINGLEUSER|**AppDomain** DDL 操作で使用できるようにします。 これらは E_APPDOMAIN_SHARED とは異なり、CLR 統合の実行に DDL 操作ではなく共有 AppDomain が使用されます。 このような AppDomain は他の同時実行操作から分離されます。|  
|E_APPDOMAIN_DOOMED|**AppDomain** 、アンロードするようにスケジュールが現在で実行するスレッドがあります。|  
  
## <a name="appdomain-cleanup"></a>AppDomain のクリーンアップ  
  
|状態|説明|  
|-----------|-----------------|  
|E_APPDOMAIN_UNLOADING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR がアンロードする要求が、 **AppDomain**マネージ データベース オブジェクトを含むアセンブリが変更または削除されたため、通常、します。|  
|E_APPDOMAIN_UNLOADED|CLR がアンロードされました、 **AppDomain**します。 これにより、エスカレーション プロシージャの結果は、通常**ThreadAbort**、 **OutOfMemory**、またはユーザー コードで未処理の例外。|  
|E_APPDOMAIN_ENQUEUE_DESTROY|**AppDomain** CLR でアンロードされ、設定を破棄する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。|  
|E_APPDOMAIN_DESTROY|**AppDomain**によって破棄されているが[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。|  
|E_APPDOMAIN_ZOMBIE|**AppDomain**によって破棄された[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 ただし、すべてのへの参照、 **AppDomain**クリーンアップされています。|  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例の詳細を表示する方法を示しています、 **AppDomain**特定のアセンブリ。  
  
```  
select appdomain_id, creation_time, db_id, user_id, state  
from sys.dm_clr_appdomains a  
where appdomain_address =   
(select appdomain_address   
 from sys.dm_clr_loaded_assemblies  
   where assembly_id = 500);  
```  
  
 次の例では、すべてのアセンブリを表示する方法を指定した**AppDomain**:  
  
```  
select a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
from sys.dm_clr_loaded_assemblies as l   
inner join sys.assemblies as a  
on l.assembly_id = a.assembly_id  
where l.appdomain_address =   
(select appdomain_address   
from sys.dm_clr_appdomains  
where appdomain_id = 15);  
```  
  
## <a name="see-also"></a>参照  
 [sys.dm_clr_loaded_assemblies &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)   
 [共通言語ランタイム関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
