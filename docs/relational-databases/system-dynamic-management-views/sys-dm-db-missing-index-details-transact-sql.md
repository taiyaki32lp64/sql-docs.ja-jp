---
title: sys.dm_db_missing_index_details (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_details
- dm_db_missing_index_details
- sys.dm_db_missing_index_details_TSQL
- dm_db_missing_index_details_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- missing indexes feature [SQL Server], sys.dm_db_missing_index_details dynamic management view
- sys.dm_db_missing_index_details dynamic management view
ms.assetid: ced484ae-7c17-4613-a3f9-6d8aba65a110
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8218ff5c92613b0f152c699a81314cb6a3530885
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263789"
---
# <a name="sysdmdbmissingindexdetails-transact-sql"></a>sys.dm_db_missing_index_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  空間インデックスを除く、欠落インデックスに関する詳細情報を返します。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]では、動的管理ビューでデータベースの包含に影響を与える情報を公開することや、ユーザーがアクセスできる他のデータベースに関する情報を公開することはできません。 この情報を公開することを避けるため、接続されているテナントに属していないデータが含まれるすべての行はフィルターで除外します。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**index_handle**|**int**|特定の欠落インデックスの識別子。 識別子はサーバー内で一意です。 **index_handle**はこのテーブルのキーです。|  
|**database_id**|**smallint**|欠落インデックスを含むテーブルがあるデータベースの識別子。|  
|**object_id**|**int**|インデックスが欠落しているテーブルの識別子。|  
|**equality_columns**|**nvarchar (4000)**|次の形式の等値述語に使用できる列のコンマ区切り一覧。<br /><br /> *table.column* =*constant_value*|  
|**inequality_columns**|**nvarchar (4000)**|次の形式のような不等値述語に使用できる列のコンマ区切り一覧。<br /><br /> *table.column* > *constant_value*<br /><br /> "=" 以外の比較演算子はすべて、不等値を表します。|  
|**included_columns**|**nvarchar (4000)**|クエリの包括列として必要な列のコンマ区切り一覧。 カバリングの詳細については付加列を参照してくださいまたは[付加列インデックスの作成](../../relational-databases/indexes/create-indexes-with-included-columns.md)です。<br /><br /> メモリ最適化インデックス (ハッシュの両方とメモリ最適化非クラスター化)、無視**included_columns**します。 テーブルのすべての列が各メモリ最適化インデックスに含まれています。|  
|**statement**|**nvarchar (4000)**|インデックスが欠落しているテーブルの名前。|  
  
## <a name="remarks"></a>コメント  
 によって返される情報**sys.dm_db_missing_index_details**クエリが、クエリ オプティマイザーによって最適化されて永続化されていないときに更新されます。 欠落インデックスの情報が保持されるのは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の再起動までです。 欠落インデックスの情報を、サーバーの再利用後も保持する場合は、データベース管理者が情報のバックアップ コピーを定期的に作成する必要があります。  
  
 一部である欠落インデックス グループの特定の欠落インデックスを決定する、クエリを実行することができます、 **sys.dm_db_missing_index_groups**動的管理ビューをこれによってで**sys.dm_db_missing_index_details**に基づいて、 **index_handle**列。  

  >[!NOTE]
  >この DMV の結果セットは、600 行に制限されます。 各行には、1 つの欠落インデックスが含まれています。 まで 600 を超える欠落したインデックスがあれば、新しいものを表示できるように、既存の欠落したインデックスに対処する必要があります。 
  
## <a name="using-missing-index-information-in-create-index-statements"></a>CREATE INDEX ステートメントでの欠落インデックス情報の使用  
 によって返される情報に変換する**sys.dm_db_missing_index_details**非等値の列の前に、とを組み合わせて両方メモリ最適化テーブルとディスク ベース インデックスの CREATE INDEX ステートメントに等号列を配置する必要がありますインデックスのキーをようにする必要があります。 付加列は、INCLUDE 句を使用して CREATE INDEX ステートメントに追加します。 等値の列の有効な順序を決定するには、選択度の最も高い列を左の先頭に指定し、選択度が高い順に並べます。  
  
 メモリ最適化インデックスに関する詳細については、次を参照してください。[メモリ最適化テーブルのインデックス](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)します。  
  
## <a name="transaction-consistency"></a>トランザクションの一貫性  
 トランザクションでテーブルを作成または削除する場合、削除されたオブジェクトに関する欠落インデックス情報を含む行は、トランザクションの一貫性を保持するためこの動的管理オブジェクトから削除されます。  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   

## <a name="see-also"></a>関連項目  
 [sys.dm_db_missing_index_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
