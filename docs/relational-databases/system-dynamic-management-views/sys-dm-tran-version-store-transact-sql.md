---
title: sys.dm_tran_version_store (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_TSQL
- sys.dm_tran_version_store
- dm_tran_version_store
- dm_tran_version_store_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d993cd06d555a9d4136274b35242477df1b304e9
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262605"
---
# <a name="sysdmtranversionstore-transact-sql"></a>sys.dm_tran_version_store (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  バージョン ストア内のすべてのバージョン レコードを表示する仮想テーブルを返します。 **sys.dm_tran_version_store** 、全体のバージョン ストアがクエリし、バージョン ストアが非常に大きくなることがあるため、効率的ではありません。  
  
 バージョン管理された各レコードは、いくつかの追跡または状態情報と共にバイナリ データとして格納されます。 データベース テーブル内のレコードと同様、バージョン ストア レコードは 8,192 バイトのページに格納されます。 レコードが 8,192 バイトを超える場合は、2 つのレコードに分割されます。  
  
 バージョン レコードはバイナリであるため、異なるデータベース照合順序の異なる問題はありません。 使用**sys.dm_tran_version_store**バージョン ストア内に存在する、バイナリ表現での行の以前のバージョンを検索します。  
  
  
## <a name="syntax"></a>構文  
  
```  
sys.dm_tran_version_store  
```  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|レコードのバージョンを生成するトランザクションのシーケンス番号。|  
|**version_sequence_num**|**bigint**|バージョン レコードのシーケンス番号。 この値は、バージョンを生成するトランザクション内で一意です。|  
|**database_id**|**int**|バージョン レコードのデータベース ID。|  
|**rowset_id**|**bigint**|レコードの行セット ID。|  
|**status**|**tinyint**|2 つのレコードにバージョン レコードに分割されているかどうかを示します。 値が 0 の場合、レコードは 1 ページに格納されています。 値が 1 の場合は、レコードが 2 つの異なるページに格納されている 2 つのレコードに分割されます。|  
|**min_length_in_bytes**|**smallint**|(バイト単位)、レコードの最小長。|  
|**record_length_first_part_in_bytes**|**smallint**|バージョン レコードの最初の部分の長さ (バイト単位)。|  
|**record_image_first_part**|**varbinary(8000)**|バージョン レコードの最初の部分のバイナリ イメージ。|  
|**record_length_second_part_in_bytes**|**smallint**|(バイト単位) のバージョン レコードの 2 番目の部分の長さ。|  
|**record_image_second_part**|**varbinary(8000)**|バージョン レコードの 2 番目の部分のバイナリ イメージ。|  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   
  
## <a name="examples"></a>使用例  
 次の例では、4 つの同時実行トランザクションが存在するテスト シナリオを使用します。これらのトランザクションはそれぞれトランザクション シーケンス番号 (XSN) で識別され、ALLOW_SNAPSHOT_ISOLATION オプションと READ_COMMITTED_SNAPSHOT オプションが ON に設定されているデータベース内で実行されます。 実行されるトランザクションは次のとおりです。  
  
-   XSN-57。SERIALIZABLE 分離での更新操作です。  
  
-   Xsn-58 では、xsn-57 と同じです。  
  
-   Xsn-59 では、スナップショット分離下で選択操作です。  
  
-   Xsn-60 では、xsn-59 と同じです。  
  
 次のクエリを実行します。  
  
```  
SELECT  
    transaction_sequence_num,  
    version_sequence_num,  
    database_id rowset_id,  
    status,  
    min_length_in_bytes,  
    record_length_first_part_in_bytes,  
    record_image_first_part,  
    record_length_second_part_in_bytes,  
    record_image_second_part  
  FROM sys.dm_tran_version_store;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
transaction_sequence_num version_sequence_num database_id  
------------------------ -------------------- -----------  
57                      1                    9             
57                      2                    9             
57                      3                    9             
58                      1                    9             
  
rowset_id            status min_length_in_bytes  
-------------------- ------ -------------------  
72057594038321152    0      12                   
72057594038321152    0      12                   
72057594038321152    0      12                   
72057594038386688    0      16                   
  
record_length_first_part_in_bytes  
---------------------------------  
29                                 
29                                 
29                                 
33                                 
  
record_image_first_part                                               
--------------------------------------------------------------------  
0x50000C0073000000010000000200FCB000000001000000270000000000          
0x50000C0073000000020000000200FCB000000001000100270000000000          
0x50000C0073000000030000000200FCB000000001000200270000000000          
0x500010000100000002000000030000000300F800000000000000002E0000000000  
  
record_length_second_part_in_bytes record_image_second_part  
---------------------------------- ------------------------  
0                                  NULL  
0                                  NULL  
0                                  NULL  
0                                  NULL  
```  
  
 この出力は、XSN-57 で 1 つのテーブルから 3 つの行バージョンが作成され、XSN-58 で他のテーブルから 1 つの行バージョンが作成されたことを示しています。  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [トランザクション関連の動的管理ビューおよび関数  &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
