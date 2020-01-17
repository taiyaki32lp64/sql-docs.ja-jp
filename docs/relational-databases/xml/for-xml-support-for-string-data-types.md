---
title: 文字列データ型の FOR XML のサポート | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- strings [SQL Server], XML
ms.assetid: bf069da8-de1e-44d2-a1fb-ade383076ac1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0ad8310f5938d757c30732cf6b1a78a9770254e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943324"
---
# <a name="for-xml-support-for-string-data-types"></a>文字列データ型の FOR XML のサポート
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  FOR XML で XML が生成されるときに、データ内の空白文字はエンティティに変換されます。  
  
 次の例では、サンプル テーブル **T** を作成し、ライン フィード、キャリッジ リターン、およびタブ文字が含まれたサンプル データを挿入します。 SELECT ステートメントは、このテーブルからサンプル データを取得します。  
  
```  
CREATE TABLE T  
(  
  c1 int identity primary key,  
  c2 varchar(100)  
);  
go  
  
INSERT T (c2) VALUES ('Special character 0xD for carriage return ' + convert(varchar(10), 0xD) + ' after carriage return');  
INSERT T (c2) VALUES ('Special character 0x9 for tab ' + convert(varchar(10), 0x9) + ' after tab' );  
INSERT T (c2) VALUES ('Special character 0xA for line feed ' + convert(varchar(10), 0xA) + ' after line feed');  
go  
SELECT *   
FROM T  
FOR XML AUTO;  
go  
```  
  
 結果を次に示します。  
  
```  
 <T c1="1" c2="Special character 0xD for carriage return   
 after carriage return" />  
 <T c1="2" c2="Special character 0x9 for tab     after tab" />  
 <T c1="3" c2="Special character 0xA for line feed   
after line feed" />  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   1 行目のキャリッジ リターンは、&#xD というエンティティに変換されます。  
  
-   2 行目のタブ文字は、&#x09 というエンティティに変換されます。  
  
-   3 行目のライン フィード文字は、&#xA というエンティティに変換されます。  
  
## <a name="see-also"></a>参照  
 [各種 SQL Server データ型の FOR XML サポート](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
