---
title: スキーマ行セットでの分散クエリのサポート |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], SQL Server Native Client OLE DB provider
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
ms.assetid: 11354bb6-be42-4d8d-854c-42dd3dc38656
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3c162bbcbf9f9212d6adc3838a06b5eaaac8b13
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73759714"
---
# <a name="schema-rowsets---distributed-query-support"></a>スキーマ行セット - 分散クエリのサポート
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分散クエリをサポートするために、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB provider **IDBSchemaRowset**インターフェイスは、リンクサーバー上のメタデータを返します。  
  
 DBPROPSET_SQLSERVERSESSION の SSPROP_QUOTEDCATALOGNAMES プロパティが VARIANT_TRUE の場合、カタログ名には引用符で囲んだ識別子 ("my.catalog" など) を指定できます。 スキーマ行セットの出力をカタログによって制限する場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、リンクサーバーとカタログ名を含む2つの部分で構成される名前を認識します。 次の表のスキーマ行セットの場合は、2部構成のカタログ名を_linked_server_として指定し**ます。** _カタログ_では、出力が名前付きリンクサーバーの適用可能なカタログに制限されます。  
  
|スキーマ行セット|カタログの制限|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMNS|TABLE_CATALOG|  
|DBSCHEMA_PRIMARY_KEYS|TABLE_CATALOG|  
|DBSCHEMA_TABLES|TABLE_CATALOG|  
|DBSCHEMA_FOREIGN_KEYS|PK_TABLE_CATALOG FK_TABLE_CATALOG|  
|DBSCHEMA_INDEXES|TABLE_CATALOG|  
|DBSCHEMA_COLUMN_PRIVILEGES|TABLE_CATALOG|  
|DBSCHEMA_TABLE_PRIVILEGES|TABLE_CATALOG|  
  
> [!NOTE]  
>  スキーマ行セットをリンク サーバーのすべてのカタログに制限するには、*linked_server* 構文を使用します (ピリオドを区切り文字として名前を指定します)。 この構文は、カタログ名の制限で NULL を指定する場合と同じで、カタログをサポートしないデータ ソースをリンク サーバーが示している場合にも使用されます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、リンクサーバーとして登録されている OLE DB データソースの一覧を返す、スキーマ行セット LINKEDSERVERS を定義します。  
  
## <a name="see-also"></a>参照  
 [スキーマ行セットのサポート &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 行&#40;セット OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
