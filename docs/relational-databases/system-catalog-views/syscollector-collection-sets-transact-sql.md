---
title: syscollector_collection_sets (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_collection_sets_TSQL
- syscollector_collection_sets
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_collection_sets view
ms.assetid: db0def92-f25b-45da-9709-eab972b33800
author: stevestein
ms.author: sstein
ms.openlocfilehash: a001a6a2da2532ac6d0e2a00079c8bd7c7036b66
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060384"
---
# <a name="syscollectorcollectionsets-transact-sql"></a>syscollector_collection_sets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  スケジュール、コレクション モードの状態など、コレクション セットに関する情報を提供します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|collection_set_id|**int**|コレクション セットのローカル識別子です。 NULL 値は許可されません。|  
|collection_set_uid|**uniqueidentifier**|コレクション セットのグローバルな一意識別子です。 NULL 値は許可されません。|  
|NAME|**nvarchar (4000)**|コレクション セットの名前です。 NULL 値が許可されます。|  
|ターゲット (target)|**nvarchar(max)**|コレクション セットの対象を識別します。 NULL 値が許可されます。|  
|is_system|**bit**|コレクション セットがデータ コレクターに付属のものか、後から dc_admin によって追加されたものかをオン (1) またはオフ (0) で示します。 たとえば、社内またはサード パーティによって開発されたコレクション セットの場合が考えられます。 NULL 値は許可されません。|  
|is_running|**bit**|コレクション セットが実行されているかどうかを示します。 NULL 値は許可されません。|  
|collection_mode|**smallint**|コレクション セットのコレクション モードを指定します。 NULL 値は許可されません。<br /><br /> コレクション モードは、次のいずれかになります。<br /><br /> 0 - キャッシュ モード。 データの収集とアップロードは個別のスケジュールです。<br /><br /> 1-非キャッシュ モード。 データの収集とアップロードは同じスケジュールに従います。|  
|proxy_id|**int**|コレクション セットのジョブ ステップを実行するために使用するプロキシを識別します。 NULL 値が許可されます。|  
|schedule_uid|**uniqueidentifier**|コレクション セットのスケジュールへのポインターを提供します。 NULL 値が許可されます。|  
|collection_job_id|**uniqueidentifier**|コレクション ジョブを識別します。 NULL 値が許可されます。|  
|upload_job_id|**uniqueidentifier**|コレクションのアップロード ジョブを識別します。 NULL 値が許可されます。|  
|logging_level|**smallint**|ログ記録レベルを 0、1、または 2 から指定します。 NULL 値は許可されません。|  
|days_until_expiration|**smallint**|管理データ ウェアハウスに収集されたデータが保存されている日数。 NULL 値は許可されません。|  
|description|**nvarchar (4000)**|コレクション セットをについて説明します。 NULL 値が許可されます。|  
|dump_on_any_error|**bit**|(1) をオンまたはオフ (0) を作成するかどうかを示すために、[!INCLUDE[ssIS](../../includes/ssis-md.md)]エラー時にダンプ ファイル。 NULL 値は許可されません。|  
|dump_on_codes|**nvarchar(max)**|ダンプ ファイルの原因となった [!INCLUDE[ssIS](../../includes/ssis-md.md)] エラー コードのリストです。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 dc_operator、dc_proxy に対する SELECT 権限が必要です。  
  
## <a name="remarks"></a>コメント  
 データ コレクター API で変更または削除が許可されるコレクション セットは、ユーザーが作成したコレクション セットのみです。 システムが提供するコレクション セットは変更または削除できません。 ただし、システム コレクション セットを有効または無効にしたり、その構成を変更することはできます。  
  
## <a name="see-also"></a>関連項目  
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [データ コレクターのビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
