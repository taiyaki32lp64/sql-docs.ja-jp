---
title: logmarkhistory (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- logmarkhistory
- logmarkhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logmarkhistory system table
ms.assetid: 5c1becc5-f34e-4869-bf69-dfafab684540
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0674bf993087b349d4e8b6f9947c65167e94df8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001804"
---
# <a name="logmarkhistory-transact-sql"></a>logmarkhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  コミットされているマークされたトランザクションごとに 1 つの行が含まれています。 このテーブルに格納されます、 **msdb**データベース。  
  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|ローカル データベースがマークされたトランザクションが発生しました。|  
|**mark_name**|**nvarchar(128)**|マークされたトランザクションのユーザーの名前。|  
|**description**|**nvarchar (255)**|マーク付きのトランザクションに指定されたユーザー定義の説明。 NULL にすることができます。|  
|**user_name**|**nvarchar(128)**|マーク付きのトランザクションを実行したデータベース ユーザー名。 NULL にすることができます。|  
|**lsn**|**numeric(25,0)**|Mark が発生したトランザクション レコードのログ シーケンス番号。|  
|**mark_time**|**datetime**|マークされたトランザクション (ローカル時刻) の時間をコミットします。|  
  
## <a name="see-also"></a>関連項目  
 [マークされたトランザクションへのデータベースの復元 &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)   
 [システム テーブル &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
