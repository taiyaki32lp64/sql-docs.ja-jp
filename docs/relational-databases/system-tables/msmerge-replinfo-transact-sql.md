---
title: MSmerge_replinfo (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_replinfo_TSQL
- MSmerge_replinfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_replinfo system table
ms.assetid: b0924094-c0cc-49c1-869a-65be0d0465a0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 045f9ab13b701b8dbd5e0895531932c21767853f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909047"
---
# <a name="msmerge_replinfo-transact-sql"></a>MSmerge_replinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_replinfo**テーブルには、サブスクリプションごとに 1 つの行が含まれています。 このテーブルは、サブスクリプションに関する情報を追跡します。 このテーブルは、パブリケーション データベースとサブスクリプション データベースに保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|レプリカの一意な ID。|  
|**use_interactive_resolver**|**bit**|調整時に、インタラクティブ競合回避モジュールを使用するかどうかを指定します。<br /><br /> **0** = は、インタラクティブ競合回避モジュールを使用しません。<br /><br /> **1** = 対話型の競合回避モジュールを使用します。|  
|**validation_level**|**int**|サブスクリプションに対して実行する検証の種類。 指定されたレベルの検証には、これらの値のいずれかを指定できます。<br /><br /> **0** = 検証なし。<br /><br /> **1** = 行数のみの検証。<br /><br /> **2** = 行数とチェックサムの検証。<br /><br /> **3** = 行数とバイナリ チェックサムの検証。|  
|**resync_gen**|**bigint**|サブスクリプションの再同期化で使用される世代番号。 値 **-1**サブスクリプションが再同期のマークされていないことを示します。|  
|**login_name**|**sysname**|サブスクリプションを作成したユーザーの名前。|  
|**hostname**|**sysname**|サブスクリプションのパーティションの生成時に、パラメーター化された行フィルターで使用される値。|  
|**merge_jobid**|**binary(16)**|サブスクリプションのマージ ジョブ ID。|  
|**sync_info**|**int**|内部使用のみ。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
