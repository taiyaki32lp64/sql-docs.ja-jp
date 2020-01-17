---
title: sys.dm_tran_transactions_snapshot (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_transactions_snapshot
- dm_tran_transactions_snapshot
- sys.dm_tran_transactions_snapshot_TSQL
- dm_tran_transactions_snapshot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_transactions_snapshot dynamic management view
ms.assetid: 03f64883-07ad-4092-8be0-31973348c647
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b91ac554186c37b2e074dd3faded49a01259222e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262686"
---
# <a name="sysdmtrantransactionssnapshot-transact-sql"></a>sys.dm_tran_transactions_snapshot (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  仮想テーブルを返します、 **sequence_number**の各スナップショット トランザクションときにアクティブなトランザクションを開始します。 このビューで返される情報を基に、次のことを確認できます。  
  
-   現在アクティブなスナップショット トランザクションの数を調べます。  
  
-   特定のスナップショット トランザクションで無視されるデータ変更。 スナップショット トランザクションの開始時にアクティブになっているトランザクションですべてのデータ変更トランザクションによってそのトランザクションがコミットした後でもは無視されます、スナップショット トランザクションで。  
  
 たとえば、次の出力から**sys.dm_tran_transactions_snapshot**:  
  
```  
transaction_sequence_num snapshot_id snapshot_sequence_num  
------------------------ ----------- ---------------------  
59                       0           57  
59                       0           58  
60                       0           57  
60                       0           58  
60                       0           59  
60                       3           57  
60                       3           58  
60                       3           59  
60                       3           60  
```  
  
 `transaction_sequence_num` 列は、現在のスナップショット トランザクションのトランザクション シーケンス番号 (XSN) です。 2 つの出力を示しています。`59`と`60`します。 `snapshot_sequence_num` 列は、各スナップショット トランザクションの開始時にアクティブ状態にあったトランザクションのトランザクション シーケンス番号です。  
  
 スナップショット トランザクション xsn-59 の開始、xsn-57 と xsn-58 では、2 つのアクティブなトランザクションの中に出力結果が実行されています。 Xsn-57 または xsn-58 では、データの変更を加え場合、xsn-59 では、変更を無視し、データベースのトランザクション上一貫性のあるビューを維持するために行のバージョン管理を使用します。  
  
 スナップショット トランザクション xsn-60 では、xsn-57 と xsn-58 でおよび xsn-59 によって行われたデータ変更を無視します。  
  
## <a name="syntax"></a>構文  
  
```  
  
dm_tran_transactions_snapshot  
```  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|スナップショット トランザクションのトランザクション シーケンス番号 (XSN)。|  
|**snapshot_id**|**int**|それぞれのスナップショット ID[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントは、read committed を使用して開始行のバージョン管理します。 Read committed を使用して実行されている各クエリをサポートしているデータベースのトランザクション上一貫性のあるビューの生成にこの値が使用される行のバージョン管理します。|  
|**snapshot_sequence_num**|**bigint**|スナップショット トランザクションが開始したときに有効となっていたトランザクション シーケンス番号。|  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   
  
## <a name="remarks"></a>コメント  
 スナップショット トランザクションの開始時に、[!INCLUDE[ssDE](../../includes/ssde-md.md)]の時点でアクティブになっているトランザクションがすべて記録します。 **sys.dm_tran_transactions_snapshot**すべての現在アクティブなスナップショット トランザクションは、この情報を報告します。  
  
 各トランザクションは、トランザクションの開始時に割り当てられるトランザクション シーケンス番号によって識別されます。 トランザクションは、BEGIN TRANSACTION または BEGIN WORK ステートメントが実行されたときに開始されますが、 トランザクション シーケンス番号は、BEGIN TRANSACTION または BEGIN WORK ステートメントの後、最初にデータにアクセスする [!INCLUDE[ssDE](../../includes/ssde-md.md)] ステートメントが実行されたときに[!INCLUDE[tsql](../../includes/tsql-md.md)]によって割り当てられます。 トランザクション シーケンス番号は 1 ずつ増加します。  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [トランザクション関連の動的管理ビューおよび関数  &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

