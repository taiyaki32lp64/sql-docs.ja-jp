---
title: sp_dbmmonitoraddmonitoring (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitoraddmonitoring
- sp_dbmmonitoraddmonitoring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], monitoring
- sp_dbmmonitoraddmonitoring
ms.assetid: 9489dc30-af29-4363-a172-4645947fc95e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4ed53c6a72b201129cf9f75214261bbdd47d6fb9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108153"
---
# <a name="spdbmmonitoraddmonitoring-transact-sql"></a>sp_dbmmonitoraddmonitoring (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース ミラーリング サーバー インスタンス上のすべてのミラー化されたデータベース ミラーリングの状態を定期的に更新するモニターのジョブを作成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dbmmonitoraddmonitoring [ update_period ]  
```  
  
## <a name="arguments"></a>引数  
 *update_period*  
 更新間隔を分単位で指定します。 この値は、1 から 120 分に指定できます。 既定値は 1 分です。  
  
> [!NOTE]  
>  更新間隔が小さすぎる場合、クライアント、応答時間が増加する可能性があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 このプロシージャを実行するには、サーバー インスタンス上で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを実行できることが必要です。また、データベース ミラーリング監視ジョブを実行するにはエージェントが実行中であることが必要です。  
  
 データベース ミラーリングが開始された場合[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 **sp_dbmmonitoraddmonitoring**プロシージャが自動的に実行します。 ALTER DATABASE ステートメントを使用して手動でのミラーリングを開始する場合、サーバー インスタンスでミラー化されたデータベースを監視する必要がありますを実行する**sp_dbmmonitoraddmonitoring**手動でします。  
  
> [!NOTE]  
>  実行する場合**sp_dbmmonitoraddmonitoring** 、データベース ミラーリングをセットアップする前に、監視ジョブは実行されますが、ミラーリング監視の履歴を格納するデータベースの状態テーブルは更新されません。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例は、更新間隔として使用した監視を開始`3`分。  
  
```  
EXEC sp_dbmmonitoraddmonitoring 3;  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース ミラーリングの監視 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangemonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitordropmonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
