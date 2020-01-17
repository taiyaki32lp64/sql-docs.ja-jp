---
title: スパース列のサポート (OLE DB) |Microsoft Docs
description: スパース列のサポート (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 701b2d9e7a6d51b7fa13f797c6c5c9de75bed5d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993861"
---
# <a name="sparse-columns-support-ole-db"></a>スパース列のサポート (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  このトピックでは、スパース列をサポートするため SQL Server の OLE DB ドライバーについて説明します。 スパース列の詳細については、「 [OLE DB Driver for SQL Server」の「スパース列のサポート](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md)」を参照してください。 サンプルについては、「[スパース列に対する列およびカタログ メタデータの表示 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md)」を参照してください。  
  
## <a name="ole-db-statement-metadata"></a>OLE DB ステートメント メタデータ  
 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 以降では、新しい DBCOLUMNFLAGS フラグ値である DBCOLUMNFLAGS_SS_ISCOLUMNSET を使用できます。 この値は、**column_set** 値である列に対して設定する必要があります。 DBCOLUMNFLAGS フラグは、IColumnsInfo:: GetColumnsInfo の*dwFlags*パラメーターと IColumnsRowset:: GetColumnsRowset によって返される行セットの DBCOLUMN_FLAGS 列を使用して取得できます。  
  
## <a name="ole-db-catalog-metadata"></a>OLE DB カタログ メタデータ  
 DBSCHEMA_COLUMNS に、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有の列が 2 つ追加されています。  
  
|列名|データ型|値およびコメント|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|列がスパース列の場合は VARIANT_TRUE、それ以外の場合は VARIANT_FALSE になります。|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|列がスパース **column_set** 列の場合は VARIANT_TRUE、それ以外の場合は VARIANT_FALSE になります。|  
  
 また、2 つのスキーマ行セットが追加されています。 これらの行セットは、構造は DBSCHEMA_COLUMNS と同じですが、返される内容が異なります。 DBSCHEMA_COLUMNS_EXTENDED は、スパース列かどうか、**column_set** のメンバーかどうかに関係なく、すべての列を返します。 DBSCHEMA_SPARSE_COLUMN_SET は、スパース **column_set** のメンバーである列のみを返します。  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>OLE DB DataTypeCompatibility の動作  
 **DataTypeCompatibility = 80** (接続文字列内) の動作は、次のよう[!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]に、クライアントと一致します。  
  
-   新しいスキーマ行セットは表示されず、スキーマ行セットの行セットにそれらのスキーマ行セットの行は含まれません。  
  
-   COLUMNS 行セット内の新しい列は表示されません。  
  
-   DBCOLUMNFLAGS_SS_ISCOLUMNSET が **column_set** 列に対して設定されません。  
  
-   DBCOMPUTEMODE_NOTCOMPUTED が **column_set** 列に対して設定されます。  
  
## <a name="ole-db-support-for-sparse-columns"></a>OLE DB によるスパース列のサポート  
 スパース列をサポートするために、次の OLE DB インターフェイスが OLE DB ドライバーで SQL Server 用に変更されました。  
  
|型またはメンバー関数|[説明]|  
|-----------------------------|-----------------|  
|IColumnsInfo::GetColumnsInfo|*dwFlags* で、新しい DBCOLUMNFLAGS フラグ値である DBCOLUMNFLAGS_SS_ISCOLUMNSET が **column_set** 列に対して設定されます。<br /><br /> DBCOLUMNFLAGS_WRITE が **column_set** 列に対して設定されます。|  
|IColumsRowset:: GetColumnsRowset|DBCOLUMN_FLAGS で、新しい DBCOLUMNFLAGS フラグ値である DBCOLUMNFLAGS_SS_ISCOLUMNSET が **column_set** 列に対して設定されます。<br /><br /> **column_set** 列に対して DBCOLUMN_COMPUTEMODE が DBCOMPUTEMODE_DYNAMIC に設定されます。|  
|IDBSchemaRowset:: GetSchemaRowset|DBSCHEMA_COLUMNS が、SS_IS_COLUMN_SET と SS_IS_SPARSE という 2 つの新しい列を返します。<br /><br /> DBSCHEMA_COLUMNS は、**column_set** のメンバーでない列のみを返します。<br /><br /> 2 つの新しいスキーマ行セットが追加されています。DBSCHEMA_COLUMNS_EXTENDED は、スパース **column_set** のメンバーシップに関係なくすべての列を返します。 DBSCHEMA_SPARSE_COLUMN_SET は、**column_set** のメンバーである列のみを返します。 これらの新しい行セットの列と制限は DBSCHEMA_COLUMNS と同じです。|  
|IDBSchemaRowset:: GetSchemas|IDBSchemaRowset::GetSchemas の使用可能なスキーマ行セットの一覧に、新しい行セットである DBSCHEMA_COLUMNS_EXTENDED と DBSCHEMA_SPARSE_COLUMN_SET の GUID が含まれます。|  
|ICommand::Execute|**select \* from** *table* を使用すると、スパース **column_set** のメンバーでないすべての列と、スパース **column_set** のメンバーであるすべての NULL 以外の列の値を含む XML 列が返されます (存在する場合)。|  
|IOpenRowset::OpenRowset|IOpenRowset:: OpenRowset は、同じテーブルに対して**select \*** クエリを実行し、ICommand:: Execute と同じ列を含む行セットを返します。|  
|ITableDefinition|このインターフェイスには、スパース列や **column_set** 列のための変更はありません。 スキーマを変更する必要のあるアプリケーションでは、適切な [!INCLUDE[tsql](../../../includes/tsql-md.md)] を直接実行する必要があります。|  
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server のプログラミング](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
