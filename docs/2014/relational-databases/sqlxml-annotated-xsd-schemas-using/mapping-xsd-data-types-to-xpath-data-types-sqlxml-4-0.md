---
title: XPath データ型 (SQLXML 4.0) への XSD データ型のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- XPath queries [SQLXML], mapping data types
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XPath data types [SQLXML]
- XSD schemas [SQLXML], mapping data types
ms.assetid: ced1a95e-18d4-4a5a-8da8-dbb6d58bbd45
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8e0e1f4e2914439c380b3bbf7b6339ee28c6879
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013764"
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>XSD データ型から XPath データ型へのマッピング (SQLXML 4.0)
  XSD スキーマに対して XPath クエリを実行するときに、`xsd:type` 属性に XSD のデータ型が指定されている場合は、XPath でクエリが処理されるときに、指定のデータ型が使用されます。  
  
 ノードの XPath データ型は、次の表に示すように、スキーマ内に指定されている XSD データ型から派生します。 ここでは説明のため、EmployeeID というノードを使用します。  
  
|XSD データ型|XDR データ型|同等の<br /><br /> XPath データ型|SQL Server<br /><br /> SQL Server 変換|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|`Base64Binary`<br /><br /> `HexBinary`|`None`<br /><br /> `bin.base64bin.hex`|`Not applicable`|なし<br /><br /> EmployeeID|  
|`Boolean`|`boolean`|`boolean`|CONVERT(bit, EmployeeID)|  
|`Decimal, integer, float, byte, short, int, long, float, double, unsignedByte, unsignedShort, unsignedInt, unsignedLong`|`number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8`|`number`|CONVERT(float(53), EmployeeID)|  
|`id, idref, idrefsentity, entities, notation, nmtoken, nmtokens, DateTime, string, AnyURI`|`id, idref, idrefsentity, entities, enumeration, notation, nmtoken, nmtokens, char, dateTime, dateTime.tz, string, uri, uuid`|`string`|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|`decimal`|`fixed14.4`|`Not applicable (There is no data type in XPath that is equivalent to the fixed14.4 XDR data type.)`|CONVERT(money, EmployeeID)|  
|`date`|`date`|`string`|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|`time`|`time`<br /><br /> `time.tz`|`string`|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
