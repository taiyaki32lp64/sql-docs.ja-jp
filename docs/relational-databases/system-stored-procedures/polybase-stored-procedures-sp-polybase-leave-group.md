---
title: sp_polybase_leave_group (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
f1_keywords:
- sp_polybase_leave_group
- sp_polybase_leave_group_TSQL
helpviewer_keywords:
- sp_polybase_leave_group
ms.assetid: ef87a8f1-5407-47b5-b8bf-bd7d08c0f0fe
author: rothja
ms.author: jroth
ms.openlocfilehash: 0071746f2d65dd0c9c699beeacf404bf3dd7bb65
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941923"
---
# <a name="sppolybaseleavegroup-transact-sql"></a>sp_polybase_leave_group (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  SQL Server インスタンスをスケール アウト計算 PolyBase グループから削除します。 
 
 SQL Server インスタンスが必要、 [PolyBase ガイド](../../relational-databases/polybase/polybase-guide.md)機能をインストールします。  PolyBase では、SQL Server 以外のデータ ソース、Hadoop と Azure blob ストレージなどの統合を使用できます。 参照してください[sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_polybase_leave_group;  
  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 CONTROL SERVER 権限が必要です。  
  
## <a name="remarks"></a>コメント  
 コンピューティング ノードは、グループからのみ削除できます。  
  
 ストアド プロシージャを実行した後に、コンピューターに、PolyBase エンジンと PolyBase データ移動サービスを再起動します。 確認するヘッド ノードで次の DMV を実行する: **sys.dm_exec_compute_nodes**します。  
  
## <a name="example"></a>例  
 例では、PolyBase グループから現在のコンピューターを削除します。  
  
```sql  
EXEC sp_polybase_leave_group ;  
```  
  
## <a name="see-also"></a>関連項目  
 [PolyBase の概要](../../relational-databases/polybase/get-started-with-polybase.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
