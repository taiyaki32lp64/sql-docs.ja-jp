---
title: dm_db_persisted_sku_features (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_persisted_sku_features_TSQL
- sys.dm_db_persisted_sku_features
- dm_db_persisted_sku_features_TSQL
- dm_db_persisted_sku_features
dev_langs:
- TSQL
helpviewer_keywords:
- editions [SQL Server]
- sys.dm_db_persisted_sku_features dynamic management view
ms.assetid: b4b29e97-b523-41b9-9528-6d4e84b89e09
author: stevestein
ms.author: sstein
ms.openlocfilehash: f689541d455f4f7e6da4cc68742519a74f671506
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981833"
---
# <a name="sysdm_db_persisted_sku_features-transact-sql"></a>sys.dm_db_persisted_sku_features (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] の一部の機能は、[!INCLUDE[ssDE](../../includes/ssde-md.md)] がデータベースファイルに情報を格納する方法を変更します。 これらの機能は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の特定のエディションでのみ使用できます。 これらの機能を備えたデータベースを、それらをサポートしない [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディションに移動することはできません。 現在のデータベースで有効になっているエディション固有の機能を一覧表示するには、sys.dm_db_persisted_sku_features 動的管理ビューを使用します。
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降)。
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|feature_name|**sysname**|データベースでは有効になっているが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションでサポートされるとは限らない機能の外部名。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の使用可能なすべてのエディションにデータベースを移行するには、この機能を削除する必要があります。|  
|feature_id|**int**|機能に関連付けられている機能 ID。 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]。|  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="remarks"></a>Remarks  
 特定のエディションで制限されている機能がデータベースで使用されていない場合、ビューは行を返しません。  
  
 sys.dm_db_persisted_sku_features では、次のデータベース変更機能が特定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のエディションに限定されていることがあります。  
  
-   **Changecapture**: データベースで変更データキャプチャが有効になっていることを示します。 変更データキャプチャを削除するには、 [sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md)ストアドプロシージャを使用します。 詳細については、「[変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)」を参照してください。  
  
-   **Columnstoreindex**: 少なくとも1つのテーブルに列ストアインデックスがあることを示します。 この機能をサポートしていない [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディションにデータベースを移動できるようにするには、 [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)または[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)ステートメントを使用して、列ストアインデックスを削除します。 詳細については、「[列ストアインデックス](../../relational-databases/indexes/columnstore-indexes-overview.md)」を参照してください。  
  
    **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降)。  
  
-   **Compression**: 少なくとも1つのテーブルまたはインデックスで、データ圧縮または vardecimal ストレージ形式が使用されていることを示します。 この機能をサポートしていない [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディションにデータベースを移動できるようにするには、 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)ステートメントまたは[alter INDEX](../../t-sql/statements/alter-index-transact-sql.md)ステートメントを使用して、データ圧縮を解除します。 vardecimal ストレージ形式を削除するには、sp_tableoption ステートメントを使用します。 詳細については、「 [Data Compression](../../relational-databases/data-compression/data-compression.md)」を参照してください。  
  
-   複数の**fsコンテナ**: データベースが複数の FILESTREAM コンテナーを使用することを示します。 データベースには、複数のコンテナー (ファイル) を含む FILESTREAM ファイルグループがあります。 詳細については、「[FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)」を参照してください。  
  
-   **Inmemoryoltp**: データベースがインメモリ oltp を使用することを示します。 データベースには、MEMORY_OPTIMIZED_DATA ファイル グループがあります。 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
  **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降)。 
  
-   **Partitioning** パーティション テーブル、パーティション インデックス、パーティション構成、またはパーティション関数が、データベースに含まれていることを示します。 Enterprise Edition と Developer Edition 以外の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディションにデータベースを移動できるようにするには、テーブルを単一パーティションに変更するだけでは不十分です。 パーティション テーブルを削除する必要があります。 テーブルにデータが含まれている場合は、SWITCH PARTITION を使用して、各パーティションを非パーティション テーブルに変換します。 その後、パーティション テーブル、パーティション構成、およびパーティション関数を削除します。  
  
-   **TransparentDataEncryption** 透過的なデータ暗号化を使用してデータベースが暗号化されていることを示します。 透過的なデータ暗号化を削除するには、ALTER DATABASE ステートメントを使用します。 詳細については、「[透過的なデータ暗号化 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)」をご覧ください。  

> [!NOTE]
> Service Pack [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 1 以降では、**TransparentDataEncryption** を除くこれらの機能が使用されています。 複数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で利用可能であり、Enterprise edition または Developer edition のみに限定されません。

 特定のエディションでのみ使用できる機能がデータベースで使用されているかどうかを確認するには、データベースで次のステートメントを実行します。  
  
```sql  
SELECT feature_name FROM sys.dm_db_persisted_sku_features;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [データベース関連の動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [エディションと SQL Server 2016 のサポートされる機能](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [エディションと SQL Server 2017 のサポートされる機能](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  
