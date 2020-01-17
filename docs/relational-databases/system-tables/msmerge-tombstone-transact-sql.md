---
title: MSmerge_tombstone (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_tombstone_TSQL
- MSmerge_tombstone
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_tombstone system table
ms.assetid: 8b3fc7bf-729b-40f2-8a26-e7dfbe8ddb38
author: stevestein
ms.author: sstein
ms.openlocfilehash: 12caefe8b764090d46051912c876272c9efe86bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68092662"
---
# <a name="msmerge_tombstone-transact-sql"></a>MSmerge_tombstone (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_tombstone**テーブルは、削除された行に関する情報を格納でき、他のサブスクライバーに反映されるまで削除します。 このテーブルは、パブリケーション データベースとサブスクリプション データベースに保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**rowguid**|**uniqueidentifier**|行の識別子です。|  
|**tablenick**|**int**|テーブルのニックネームです。|  
|**type**|**tinyint**|削除の種類:<br /><br /> 1 = ユーザー削除です。<br /><br /> 5 = フィルター選択されたパーティションに既に行が属していません。<br /><br /> 6 = システム削除です。|  
|**lineage**|**varbinary(249)**|削除されたレコードのバージョンと、削除されたときに認識された更新を示します。 これによって、あるサブスクライバーによって行が削除されているときに、別のサブスクライバーがこれを更新するという競合を、一貫して回避するための規則が定められます。|  
|**generation**|**int**|行が削除されたときに割り当てられます。 サブスクライバーが generation 値 N、生成を満たす廃棄標識だけを要求する場合 > = N が送信されます。|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|削除された行が属する論理レコードを識別します。|  
|**logical_record_lineage**|**varbinary(501)**|サブスクライバーのニックネームとバージョン番号のペアのこの行が属する論理レコードの削除の履歴を維持するために使用されます。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
