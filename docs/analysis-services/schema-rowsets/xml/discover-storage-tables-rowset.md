---
title: "DISCOVER_STORAGE_TABLES 行セット |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 13df6f10-8efe-4fe9-83a6-96d108809ed1
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d882e8b20949a656c1402af084a6e017c33b444f
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="discoverstoragetables-rowset"></a>DISCOVER_STORAGE_TABLES 行セット
  クライアントは、テーブル モードまたは SharePoint モードで動作している Analysis Services データベースに含まれているテーブルを調べることができます。  
  
## <a name="rowset-columns"></a>行セットの列  
 **DISCOVER_STORAGE_TABLES**行セットには、次の列が含まれています。  
  
|**列名**|**型インジケーター**|**[データ型]**|**Description**|  
|---------------------|------------------------|----------------|---------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**||テーブルを含んでいるデータベースの名前を指定します。<br /><br /> **DISCOVER_STORAGE_TABLES**この列を使用して行セットを制限することができます。 この列を使用せずに行セットを制限した場合、現在のデータベースが使用されます。|  
|**CUBE_NAME**|**DBTYPE_WSTR**||テーブルを含んでいるキューブまたはモデルを指定します。<br /><br /> **DISCOVER_STORAGE_TABLES**この列を使用して行セットを制限することができます。|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**||メジャー グループの名前。|  
|**PARTITION_NAME**|**DBTYPE_WSTR**||パーティションの名前。|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||ディメンションの名前。|  
|**TABLE_ID**|**DBTYPE_WSTR**||テーブルの属性を格納するために使用されるテーブルの ID。|  
|**TABLE_PARTITIONS_COUNT**|**DBTYPE _ WSTR**||テーブルのパーティション数。|  
|**HINT_TABLE_TYPE**|**DBTYPE _ WSTR**||テーブル型のヒント。|  
|**ROWS_COUNT**|**DBTYPE_UI4**||パーティション内の行の数。|  
|**RIVIOLATION_COUNT**|**DBTYPE_UI4**||参照整合性違反の行数。|  
  
## <a name="restriction-columns"></a>制限の列  
 **DISCOVER_STORAGE_TABLES**行セットは、次の表に示されている列で制限できます。  
  
|**列名**|**型インジケーター**|**制限の状態**|  
|---------------------|------------------------|---------------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|省略可。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|省略可。|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|省略可|  
|**PARTITION_NAME**|**DBTYPE_WSTR**|省略可|  
  
## <a name="example"></a>例  
 次のコード サンプルは、現在の接続の既定のデータベースから、ストレージ テーブルとその行数の一覧を返します。  
  
```  
SELECT TABLE_ID, ROWS_COUNT  
FROM $system.DISCOVER_STORAGE_TABLES  
ORDER BY TABLE_ID DESC  
  
```  
  
## <a name="see-also"></a>参照  
 [Analysis Services のスキーマ行セット](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  