---
title: sys.dm_tran_top_version_generators (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_top_version_generators
- sys.dm_tran_top_version_generators
- dm_tran_top_version_generators_TSQL
- sys.dm_tran_top_version_generators_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_top_version_generators dynamic management view
ms.assetid: cec7809b-ba8a-4df9-b5bb-d4f651ff1a86
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e8fb59e9cfe636f6cab775fa2cb000c60ba08ad2
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262606"
---
# <a name="sysdmtrantopversiongenerators-transact-sql"></a>sys.dm_tran_top_version_generators (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  バージョン ストアに最も多くバージョンを作成しているオブジェクトの仮想テーブルを返します。 **sys.dm_tran_top_version_generators**上位 256 個の集計でグループ化されているレコードの長さを返します、 **database_id**と**rowset_id**します。 **sys.dm_tran_top_version_generators**クエリを実行してデータを取得、 **dm_tran_version_store**仮想テーブルです。 **sys.dm_tran_top_version_generators**非効率的なビューがバージョン ストアにクエリを実行して、バージョン ストアが非常に大きくなることができます。 この関数を使用して、バージョン ストアの高いコンシューマーを検索することをお勧めします。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_tran_top_version_generators**します。  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.dm_tran_top_version_generators  
```  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|データベース ID。|  
|**rowset_id**|**bigint**|行セット id。|  
|**aggregated_record_length_in_bytes**|**int**|各レコードの長さの合計**database_id**と**rowset_id ペア**バージョン ストアにします。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   

## <a name="remarks"></a>コメント  
 **Sys.dm_tran_top_version_generators**を実行して、全体のバージョン ストアのスキャン、多くのページを読み取る必要があります**sys.dm_tran_top_version_generators**システムに干渉することができますパフォーマンス。  
  
## <a name="examples"></a>使用例  
 次の例では、4 つの同時実行トランザクションが存在するテスト シナリオを使用します。これらのトランザクションはそれぞれトランザクション シーケンス番号 (XSN) で識別され、ALLOW_SNAPSHOT_ISOLATION オプションと READ_COMMITTED_SNAPSHOT オプションが ON に設定されているデータベース内で実行されます。 実行されるトランザクションは次のとおりです。  
  
-   XSN-57。SERIALIZABLE 分離での更新操作です。  
  
-   Xsn-58 では、xsn-57 と同じです。  
  
-   Xsn-59 では、スナップショット分離下で選択操作です。  
  
-   Xsn-60 では、xsn-59 と同じです。  
  
 次のクエリを実行します。  
  
```  
SELECT  
    database_id,  
    rowset_id,  
    aggregated_record_length_in_bytes  
  FROM sys.dm_tran_top_version_generators;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
database_id rowset_id            aggregated_record_length_in_bytes  
----------- -------------------- ---------------------------------  
9           72057594038321152    87  
9           72057594038386688    33  
```  
  
 出力は、すべてのバージョンがによって作成されたことを示しています。`database_id``9`バージョンが 2 つのテーブルから生成するとします。  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [トランザクション関連の動的管理ビューおよび関数  &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


