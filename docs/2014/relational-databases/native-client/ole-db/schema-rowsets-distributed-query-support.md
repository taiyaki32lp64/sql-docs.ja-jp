---
title: 分散スキーマ行セット内のクエリのサポート |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 24411ceb757414f1a70f0f10bdf5b2c7660e2cd8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667598"
---
# <a name="distributed-query-support-in-schema-rowsets"></a>スキーマ行セットでの分散クエリのサポート
  サポートするために[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]分散クエリ、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー **IDBSchemaRowset**インターフェイスは、リンク サーバー上のメタデータを返します。  
  
 DBPROPSET_SQLSERVERSESSION の SSPROP_QUOTEDCATALOGNAMES プロパティが VARIANT_TRUE の場合、カタログ名には引用符で囲んだ識別子 ("my.catalog" など) を指定できます。 カタログ、スキーマ行セットの出力を制限する場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、リンク サーバーとカタログの名前を含む 2 つの部分名を認識します。 次の表に、スキーマ行セットとして 2 つの部分のカタログ名を指定する_linked_server_ **.** _カタログ_名前付きのリンク サーバーの適切なカタログへの出力を制限します。  
  
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
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、リンク サーバーとして登録されている OLE DB データ ソースの一覧を返す、LINKEDSERVERS スキーマ行セットを定義します。  
  
## <a name="see-also"></a>参照  
 [スキーマ行セットのサポート &#40;OLE DB&#41;](schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 行セット&#40;OLE DB&#41;](schema-rowsets-linkedservers-rowset.md)  
  
  
