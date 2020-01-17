---
title: スパース列のサポート (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 918574b3-c62e-4937-9e5f-37310dedc8f9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b286ba7bde145a9a3676f38f329a8efbd932a4cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667646"
---
# <a name="sparse-columns-support-ole-db"></a>スパース列のサポート (OLE DB)
  このトピックでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB でのスパース列のサポートについて説明します。 スパース列の詳細については、次を参照してください。 [SQL Server Native Client におけるスパース列のサポート](../features/sparse-columns-support-in-sql-server-native-client.md)します。 サンプルについては、「[スパース列に対する列およびカタログ メタデータの表示 &#40;OLE DB&#41;](../../native-client-ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md)」を参照してください。  
  
## <a name="ole-db-statement-metadata"></a>OLE DB ステートメント メタデータ  
 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 以降では、新しい DBCOLUMNFLAGS フラグ値である DBCOLUMNFLAGS_SS_ISCOLUMNSET を使用できます。 この値は、`column_set` 値である列に対して設定する必要があります。 DBCOLUMNFLAGS フラグを使用して取得できます、 *dwFlags* icolumnsinfo::getcolumnsinfo と icolumnsrowset::getcolumnsrowset によって返される行セットの DBCOLUMN_FLAGS 列のパラメーター。  
  
## <a name="ole-db-catalog-metadata"></a>OLE DB カタログ メタデータ  
 DBSCHEMA_COLUMNS に、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有の列が 2 つ追加されています。  
  
|列名|データ型|値およびコメント|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|列がスパース列の場合は VARIANT_TRUE、それ以外の場合は VARIANT_FALSE になります。|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|列がスパース `column_set` 列の場合は VARIANT_TRUE、それ以外の場合は VARIANT_FALSE になります。|  
  
 また、2 つのスキーマ行セットが追加されています。 これらの行セットは、構造は DBSCHEMA_COLUMNS と同じですが、返される内容が異なります。 DBSCHEMA_COLUMNS_EXTENDED は、スパース列かどうか、`column_set` のメンバーかどうかに関係なく、すべての列を返します。 DBSCHEMA_SPARSE_COLUMN_SET は、スパース `column_set` のメンバーである列のみを返します。  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>OLE DB DataTypeCompatibility の動作  
 `DataTypeCompatibility=80` の (接続文字列内での) 動作は、次のように、[!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] クライアントと変わりません。  
  
-   新しいスキーマ行セットは表示されず、スキーマ行セットの行セットにそれらのスキーマ行セットの行は含まれません。  
  
-   COLUMNS 行セット内の新しい列は表示されません。  
  
-   DBCOLUMNFLAGS_SS_ISCOLUMNSET が `column_set` 列に対して設定されません。  
  
-   DBCOMPUTEMODE_NOTCOMPUTED が `column_set` 列に対して設定されます。  
  
## <a name="ole-db-support-for-sparse-columns"></a>OLE DB によるスパース列のサポート  
 スパース列をサポートするために、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client で次の OLE DB インターフェイスが変更されています。  
  
|型またはメンバー関数|説明|  
|-----------------------------|-----------------|  
|IColumnsInfo::GetColumnsInfo|新しい DBCOLUMNFLAGS フラグ値がある DBCOLUMNFLAGS_SS_ISCOLUMNSET が設定されて`column_set`列*dwFlags*します。<br /><br /> DBCOLUMNFLAGS_WRITE が `column_set` 列に対して設定されます。|  
|IColumsRowset::GetColumnsRowset|DBCOLUMN_FLAGS で、新しい DBCOLUMNFLAGS フラグ値である DBCOLUMNFLAGS_SS_ISCOLUMNSET が `column_set` 列に対して設定されます。<br /><br /> `column_set` 列に対して DBCOLUMN_COMPUTEMODE が DBCOMPUTEMODE_DYNAMIC に設定されます。|  
|IDBSchemaRowset::GetSchemaRowset|DBSCHEMA_COLUMNS には、2 つの新しい列が返されます。SS_IS_COLUMN_SET と SS_IS_SPARSE します。<br /><br /> DBSCHEMA_COLUMNS は、`column_set` のメンバーでない列のみを返します。<br /><br /> 2 つの新しいスキーマ行セットが追加されました。DBSCHEMA_COLUMNS_EXTENDED はすべての列のスパースかどうかに関係なくを返します`column_set`メンバーシップ。 DBSCHEMA_SPARSE_COLUMN_SET は、`column_set` のメンバーである列のみを返します。 これらの新しい行セットの列と制限は DBSCHEMA_COLUMNS と同じです。|  
|IDBSchemaRowset::GetSchemas|IDBSchemaRowset::GetSchemas の使用可能なスキーマ行セットの一覧に、新しい行セットである DBSCHEMA_COLUMNS_EXTENDED と DBSCHEMA_SPARSE_COLUMN_SET の GUID が含まれます。|  
|ICommand::Execute|場合**選択\*から***テーブル*は、スパースのメンバーではないすべての列を返します、 `column_set`XML 列が null 以外のすべての列の値を含むスパースのメンバー `column_set`、存在する場合。|  
|IOpenRowset::OpenRowset|Iopenrowset::openrowset が持つ icommand::execute と同じ列を含む行セットを返します、**選択\*** 同じテーブルにクエリします。|  
|ITableDefinition|このインターフェイスには、スパース列や `column_set` 列のための変更はありません。 スキーマを変更する必要のあるアプリケーションでは、適切な [!INCLUDE[tsql](../../../includes/tsql-md.md)] を直接実行する必要があります。|  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client &#40;OLE DB&#41;](sql-server-native-client-ole-db.md)  
  
  
