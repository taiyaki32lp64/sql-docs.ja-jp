---
title: sys.dm_os_buffer_descriptors (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_buffer_descriptors_TSQL
- dm_os_buffer_descriptors_TSQL
- sys.dm_os_buffer_descriptors
- dm_os_buffer_descriptors
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_buffer_descriptors dynamic management view
ms.assetid: 012aab95-8888-4f35-9ea3-b5dff6e3f60f
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7395d52b7c91678f11a37a4da32877f31e5780bf
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265865"
---
# <a name="sysdmosbufferdescriptors-transact-sql"></a>sys.dm_os_buffer_descriptors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在では、すべてのデータ ページに関する情報を返します、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]バッファー プールです。 このビューの出力は、バッファー プール内のデータベース ページのディストリビューションをデータベース、オブジェクト、または種類に従って決定するために使用できます。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、この動的管理ビューは、バッファー プール拡張ファイルのデータ ページに関する情報も返します。 詳細については、次を参照してください。[バッファー プール拡張機能](../../database-engine/configure-windows/buffer-pool-extension.md)します。  
  
 ディスクから読み込まれたデータ ページは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバッファー プールにコピーされ、再使用に備えてキャッシュされます。 キャッシュされたデータ ページには、それぞれ 1 つのバッファー記述子が割り当てられます。 このバッファー記述子により、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに現在キャッシュされている各データ ページが一意に識別されます。 sys.dm_os_buffer_descriptors では、キャッシュされたページのすべてのユーザーとシステム データベースを返します。 これには、リソース データベースに関連付けられているページも含まれます。  
  
> **注:** これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_os_buffer_descriptors**します。  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id|**int**|バッファー プール内のページに関連付けられているデータベースの ID。 NULL 値が許可されます。|  
|file_id|**int**|ページに関連する保存済みの画像を格納するファイルの ID。 NULL 値が許可されます。|  
|page_id|**int**|ファイル内のページの ID。 NULL 値が許可されます。|  
|page_level|**int**|ページのインデックス レベル。 NULL 値が許可されます。|  
|allocation_unit_id|**bigint**|ページのアロケーション ユニットの ID。 この値は sys.allocation_units の結合に使用できます。 NULL 値が許可されます。|  
|page_type|**nvarchar(60)**|など、ページを種類します。データ ページやインデックス ページです。 NULL 値が許可されます。|  
|row_count|**int**|ページの行数。 NULL 値が許可されます。|  
|free_space_in_bytes|**int**|使用できるページの空き領域 (バイト単位)。 NULL 値が許可されます。|  
|is_modified|**bit**|1 = ディスクからの読み取り後にページが変更されました。 NULL 値が許可されます。|  
|numa_node|**int**|バッファーの Nonuniform Memory Access ノード。 NULL 値が許可されます。|  
|read_microsec|**bigint**|バッファーにページを読み込むために必要な実時間 (マイクロ秒)。 この数字では、バッファーを再利用するとリセットされます。 NULL 値が許可されます。|  
|is_in_bpool_extension|**bit**|1 = ページがバッファー プール拡張機能。 NULL 値が許可されます。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   
   
## <a name="remarks"></a>コメント  
 sys.dm_os_buffer_descriptors では、リソース データベースによって使用されているページが返されます。 sys.dm_os_buffer_descriptors では、ページの空きや流用ページ、または読み取られたときにエラーを発生したページに関する情報は返されません。  
  
|From|変換先|基準|リレーションシップ|  
|----------|--------|--------|------------------|  
|sys.dm_os_buffer_descriptors|sys.databases|database_id|多対一|  
|sys.dm_os_buffer_descriptors|\<userdb>.sys.allocation_units|allocation_unit_id|多対一|  
|sys.dm_os_buffer_descriptors|\<userdb>.sys.database_files|file_id|多対一|  
|sys.dm_os_buffer_descriptors|sys.dm_os_buffer_pool_extension_configuration|file_id|多対一|  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-cached-page-count-for-each-database"></a>A. 各データベースのキャッシュ ページ数を返す  
 次の例では、各データベースについて、読み込まれたページ数を返します。  
  
```  
SELECT COUNT(*)AS cached_pages_count  
    ,CASE database_id   
        WHEN 32767 THEN 'ResourceDb'   
        ELSE db_name(database_id)   
        END AS database_name  
FROM sys.dm_os_buffer_descriptors  
GROUP BY DB_NAME(database_id) ,database_id  
ORDER BY cached_pages_count DESC;  
```  
  
### <a name="b-returning-cached-page-count-for-each-object-in-the-current-database"></a>B. 現在のデータベース内の各オブジェクトのキャッシュ ページ数を返す  
 次の例では、現在のデータベース内の各オブジェクトについて、読み込まれたページ数を返します。  
  
```  
SELECT COUNT(*)AS cached_pages_count   
    ,name ,index_id   
FROM sys.dm_os_buffer_descriptors AS bd   
    INNER JOIN   
    (  
        SELECT object_name(object_id) AS name   
            ,index_id ,allocation_unit_id  
        FROM sys.allocation_units AS au  
            INNER JOIN sys.partitions AS p   
                ON au.container_id = p.hobt_id   
                    AND (au.type = 1 OR au.type = 3)  
        UNION ALL  
        SELECT object_name(object_id) AS name     
            ,index_id, allocation_unit_id  
        FROM sys.allocation_units AS au  
            INNER JOIN sys.partitions AS p   
                ON au.container_id = p.partition_id   
                    AND au.type = 2  
    ) AS obj   
        ON bd.allocation_unit_id = obj.allocation_unit_id  
WHERE database_id = DB_ID()  
GROUP BY name, index_id   
ORDER BY cached_pages_count DESC;  
```  
  
## <a name="see-also"></a>参照  
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 
 [SQL Server オペレーティング システム関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Resource データベース](../../relational-databases/databases/resource-database.md)   
 [sys.dm_os_buffer_pool_extension_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql.md)  
  
  


