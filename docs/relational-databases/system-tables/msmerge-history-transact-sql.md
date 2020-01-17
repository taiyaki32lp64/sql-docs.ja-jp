---
title: MSmerge_history (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_history_TSQL
- MSmerge_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_history system table
ms.assetid: 936195ad-ca07-41a8-a1a0-6699b6e63403
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7de3f8de87804facf6670cf0dd261464143c2aeb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017692"
---
# <a name="msmerge_history-transact-sql"></a>MSmerge_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_history**テーブルに履歴行以前のマージ エージェント ジョブ セッションの結果の詳細な説明にはが含まれています。 このテーブルには、エージェントの出力の行ごとに 1 つの行が含まれています。 このテーブルは、ディストリビューション データベースと各サブスクリプション データベースで使用されます。 ディストリビューション データベースでは、すべてのマージ パブリケーションおよびディストリビューターを使用するサブスクリプションの履歴が含まれます。 各サブスクリプション データベースでは、サブスクライバーでサブスクライブしているパブリケーションの履歴が含まれます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|マージ エージェント ジョブの ID。|  
|**agent_id**|**int**|マージ エージェントの ID。|  
|**comments**|**nvarchar (255)**|メッセージ テキストです。|  
|**error_id**|**int**|エラーの ID、 [MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md)システム テーブル。|  
|**timestamp**|**timestamp**|このテーブルのタイムスタンプ列です。|  
|**updatable_row**|**bit**|設定**1**履歴行を上書きできる場合。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
