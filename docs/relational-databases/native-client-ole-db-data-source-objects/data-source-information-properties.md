---
title: データ ソースの情報のプロパティ |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 7fd80e47-5bd9-41e2-a3d3-091a7c8c5f2b
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5454f7c41a55442c8b68cd57dd71c3859902be97
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535112"
---
# <a name="data-source-information-properties"></a>データ ソース情報のプロパティ
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  プロバイダー固有のプロパティ セット DBPROPSET_SQLSERVERDATASOURCEINFO には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーにより、次のデータ ソース情報プロパティが定義されます。  
  
|プロパティ ID|説明|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|型:VT_BOOL<br /><br /> R/WRead<br /><br /> 既定値:VARIANT_TRUE<br /><br /> 説明:列の照合順序がサポートされているかどうかを判断するために使用します。<br /><br /> VARIANT_TRUE:列レベルの照合順序がサポートされています。<br /><br /> VARIANT_FALSE:列レベルの照合順序がサポートされていません。|  
|SSPROP_UNICODELCID|型:VT_I4 R/WRead<br /><br /> 説明:Unicode ロケール id。<br /><br /> これは、Unicode データの並べ替えに使われるロケールです。|  
|SSPROP_UNICODECOMPARISONSTYLE|型:VT_I4 R/WRead<br /><br /> 説明:Unicode 比較形式です。<br /><br /> Unicode データの並べ替えに使われる並べ替えオプションです。|  
  
 プロバイダー固有のプロパティ セット DBPROPSET_SQLSERVERSTREAM には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーにより、次の追加プロパティが定義されます。  
  
|プロパティ ID|説明|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|型:VT_BSTR R/W[読み取り/書き込み]<br /><br /> 説明:FOR XML クエリの結果が整形式のドキュメントをできない可能性があります。 このプロパティを指定すると、'select ... for XML' クエリの結果はこのプロパティが提供するルート タグにラップされて、整形式の XML ドキュメントが返されます。 クエリがブラウザーから実行されている場合、結果の読み込み時にブラウザーがパーサー エラーを表示する場合があります。 このエラーを回避するために、SQL ISAPI はキーワード ROOT をサポートしています。 このキーワードは SSPROP_STREAM_XMLROOT プロパティにマップされます。|  
  
## <a name="see-also"></a>参照  
 [データ ソース オブジェクト&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
