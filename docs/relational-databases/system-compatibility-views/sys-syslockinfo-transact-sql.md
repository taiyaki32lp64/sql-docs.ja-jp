---
title: sys.syslockinfo (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syslockinfo_TSQL
- sys.syslockinfo_TSQL
- sys.syslockinfo
- syslockinfo
dev_langs:
- TSQL
helpviewer_keywords:
- syslockinfo system table
- sys.syslockinfo compatibility view
ms.assetid: d8cae434-807a-473e-b94f-f7a0e1b2daf0
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c56aa86c20867cfe2cf1da520922d1c74f9c01c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053343"
---
# <a name="syssyslockinfo-transact-sql"></a>sys.syslockinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  許可、変換、および待機のすべてのロック要求についての情報を格納します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
> [!IMPORTANT]  
>  以前のバージョンからこの機能が変更された[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 詳細については、次を参照してください。 [SQL Server 2016 におけるデータベース エンジン機能の重大な変更](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**rsc_text**|**nchar(32)**|ロック リソースの説明。 リソース名の一部が含まれます。|  
|**rsc_bin**|**binary(16)**|バイナリ ロック リソース。 ロック マネージャーに格納されている実際のロック リソースが含まれます。 書式指定済みのロック リソースを独自のロック リソース形式を生成するための詳細について知っているツールは、この列が含まれるを実行するために自己結合**syslockinfo**します。|  
|**rsc_valblk**|**binary(16)**|ロック値ブロック。 リソースの種類によっては、ロック マネージャーによってハッシュされず、特定のロック リソースの所有権が判断されないロック リソース内の追加データが含まれることがあります。 たとえば、ページ ロックは特定のオブジェクト ID で所有されません。 ロックのエスカレーションなどの目的があるためです。 ただし、ロック値ブロックにページ ロックのオブジェクト ID が含まれることがあります。|  
|**rsc_dbid**|**smallint**|リソースに関連付けられているデータベース ID。|  
|**rsc_indid**|**smallint**|該当する場合、リソースに関連付けられているインデックス ID。|  
|**rsc_objid**|**int**|該当する場合、リソースに関連付けられているオブジェクト ID。|  
|**rsc_type**|**tinyint**|リソースの種類:<br /><br /> 1 = NULL リソース (未使用)<br /><br /> 2 = データベース<br /><br /> 3 = ファイル<br /><br /> 4 = インデックス<br /><br /> 5 = テーブル<br /><br /> 6 = ページ<br /><br /> 7 = キー<br /><br /> 8 = エクステント<br /><br /> 9 = RID (行 ID)<br /><br /> 10 = アプリケーション|  
|**rsc_flag**|**tinyint**|内部リソース フラグ。|  
|**req_mode**|**tinyint**|ロック要求モード。 この列には要求側のロック モードが含まれており、許可モード、または変換や待機モードを表します。<br /><br /> 0 = NULL。 リソースへのアクセスは一切許可されません。 プレースホルダーとしての役割を果たします。<br /><br /> 1 = Sch-S (スキーマ安定度)。 スキーマ エレメントに対してスキーマ安定度ロックが保持されているセッションの中では、テーブルやインデックスなどのスキーマ エレメントは削除されません。<br /><br /> 2 = Sch-M (スキーマ修正)。 特定のリソースのスキーマを変更するセッションで保持される必要があります。 他のセッションで目的のオブジェクトが参照されないようにします。<br /><br /> 3 = S (共有)。 保持しているセッションに、リソースへの共有アクセスが許可されます。<br /><br /> 4 = U (更新)。 リソース上で取得された更新ロックが、最終的に更新されることが許可されます。 これは、後で更新される可能性があるリソースが複数のセッションによってロックされるとき、一般的な形式のデッドロックが発生するのを防止するために使用します。<br /><br /> 5= X (排他)。 保持しているセッションで、リソースへの排他アクセスが許可されます。<br /><br /> 6 = IS (共有インテント)。 ロック階層の下位のリソースに S ロックを設定するよう指定します。<br /><br /> 7= IU (更新インテント)。 ロック階層の下位のリソースに U ロックを設定するよう指定します。<br /><br /> 8 = IX (排他インテント)。 ロック階層の下位のリソースに X ロックを設定するよう指定します。<br /><br /> 9 = SIU (共有更新インテント)。 ロック階層の下位のリソースに更新ロックを設定する目的で、リソースへの共有アクセスを指定します。<br /><br /> 10 = SIX (共有排他インテント)。 ロック階層の下位のリソースに排他ロックを設定する目的で、リソースへの共有アクセスを指定します。<br /><br /> 11 = IX (更新排他インテント)。 ロック階層の下位のリソースに排他ロックを設定する目的で、リソースに保持する更新ロックを指定します。<br /><br /> 12 = BU。 一括操作で使用します。<br /><br /> 13 = RangeS_S (共有キー範囲と共有リソース ロック)。 直列化可能な範囲スキャンを指定します。<br /><br /> 14 = RangeS_U (共有キー範囲と更新リソース ロック)。 直列化可能な更新スキャンを指定します。<br /><br /> 15 = RangeI_N (挿入キー範囲と NULL リソース ロック)。 新しいキーをインデックスに挿入する前に、範囲をテストするために使用します。<br /><br /> 16 = RangeI_S。 RangeI_N と S ロックの重なりによって作成されるキー範囲変換ロックです。<br /><br /> 17 = RangeI_U。 RangeI_N と U ロックの重なりによって作成されるキー範囲変換ロックです。<br /><br /> 18 = RangeI_X。 RangeI_N と X ロックの重なりによって作成されるキー範囲変換ロックです。<br /><br /> 19 = RangeX_S。 RangeI_N と RangeS_S ロックの重なりによって作成されるキー範囲変換 ロックです。<br /><br /> 20 = RangeX_U。 RangeI_N と RangeS_U ロックの重なりによって作成されるキー範囲変換ロックです。<br /><br /> 21 = RangeX_X (排他キー範囲と排他リソース ロック)。 範囲内のキーを更新する場合に使用する変換ロックです。|  
|**req_status**|**tinyint**|ロック要求の状態。<br /><br /> 1 = 許可<br /><br /> 2 = 変換<br /><br /> 3 = 待機|  
|**req_refcnt**|**smallint**|ロック参照数。 参照数は、トランザクションが特定のリソースに対してロックを要求するたびに増加します。 参照数が 0 に達するまで、ロックを解放することはできません。|  
|**req_cryrefcnt**|**smallint**|予約済み。 常に 0 に設定されます。|  
|**req_lifetime**|**int**|ロックの有効期限のビットマップ。 特定のクエリ処理方法の実行中は、クエリ プロセッサによってクエリの特定のフェーズが完了するまで、リソース上のロックは保持される必要があります。 ロックの有効期限のビットマップは、クエリの特定フェーズの実行が完了したときに解放できるロックのグループを示すため、クエリ プロセッサとトランザクション マネージャーによって使用されます。 ビットマップ内の特定のビットを使用すると、参照数が 0 に達してもトランザクションの完了時までロックを保持するよう指定できます。|  
|**req_spid**|**int**|内部[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ロックを要求するセッションのプロセス ID。|  
|**req_ecid**|**int**|実行コンテキスト ID (ECID)。 並列操作内のどのスレッドが特定のロックを所有するかを指定するときに使用します。|  
|**req_ownertype**|**smallint**|ロックに関連付けられているオブジェクトの種類。<br /><br /> 1 = トランザクション<br /><br /> 2 = カーソル<br /><br /> 3 = セッション<br /><br /> 4 = 前回のセッション<br /><br /> 3 と 4 は、特殊なセッション ロックで、それぞれデータベースとファイル グループのロックを追跡します。|  
|**req_transactionID**|**bigint**|ID で使用されて一意のトランザクション**syslockinfo**および profiler イベント|  
|**req_transactionUOW**|**uniqueidentifier**|DTC トランザクションの作業単位 ID (UOW)。 MS DTC 以外のトランザクションの場合、UOW は 0 に設定されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [システム ビューへのシステム テーブルのマッピング&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
