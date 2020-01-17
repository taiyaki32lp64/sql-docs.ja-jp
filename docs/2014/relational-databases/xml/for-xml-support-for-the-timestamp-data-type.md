---
title: timestamp データ型に対する FOR XML サポート | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type
ms.assetid: 4e1920e1-e7a4-4069-965e-3f6039a6099e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 094cd2859c9973c2d91145de5960d4752800ce1a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287677"
---
# <a name="for-xml-support-for-the-timestamp-data-type"></a>timestamp データ型に対する FOR XML サポート
  FOR XML 変換では、 **timestamp** 型の値は、 **varbinary(8)** データとして扱われ、常に、Base 64 エンコードされます。 必要に応じて、XSD スキーマまたは XDR スキーマでこの型が反映されます。  
  
```  
drop table t  
go  
create table t  
(c1 int,  
 c2 timestamp)  
go  
  
insert t values(1, null)  
go  
select * from t  
for xml auto, xmldata  
go  
```  
  
 結果を次に示します。  
  
```  
<Schema name="Schema1"   
        xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:datatypes">  
  <ElementType name="t" content="empty" model="closed">  
    <AttributeType name="c1" dt:type="i4" />  
    <AttributeType name="c2" dt:type="bin.base64" />  
    <attribute type="c1" />  
    <attribute type="c2" />  
  </ElementType>  
</Schema>  
<t xmlns="x-schema:#Schema1" c1="1" c2="AAAAAAAAH04=" />  
```  
  
## <a name="see-also"></a>関連項目  
 [各種 SQL Server データ型の FOR XML サポート](for-xml-support-for-various-sql-server-data-types.md)  
  
  
