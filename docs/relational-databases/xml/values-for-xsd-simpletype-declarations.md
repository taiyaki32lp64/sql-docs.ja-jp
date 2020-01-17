---
title: '&lt;xsd:simpleType&gt; 宣言の値 | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xsd:simpleType declarations
ms.assetid: 557b972d-3af9-40bf-8382-72b05c9de1c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4c19a71b12b16ddd408e7cdd356debc5ec87de43
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096980"
---
# <a name="values-for-ltxsdsimpletypegt-declarations"></a>&lt;xsd:simpleType&gt; 宣言の値
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  次の表に、認識されるすべての XSD 単純型を列挙して、適用される制限の概要を示します。  
  
 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **\<xsd:simpleType>** 宣言で NaN 値がサポートされません。 NaN 値を含むスキーマはサーバーで拒否されます。  
  
|単純型|制限事項|  
|-----------------|----------------|  
|**duration**|年部分は -2^31 ～ 2^31-1 の範囲で指定する必要があります。 月、日、時、分、秒は、いずれも 0 ～ 9999 の範囲で指定する必要があります。 秒部分の小数点以下桁数は 3 桁まで指定できます。|  
|**dateTime**|タイム ゾーンのサブフィールド内の時間部分は、-14 ～ 14 の範囲で指定する必要があります。 年部分は 1 ～ 9999 の範囲で指定する必要があります。 月部分は 1 ～ 12 の範囲で指定する必要があります。 日部分は 1 ～ 31 の範囲で指定し、さらにカレンダーの日付として有効な値である必要があります。 たとえば、1974-02-31 を指定した場合、2 月には 31 日までないので、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では無効な日付として検出され、エラーを返します。<br /><br /> 秒部分は、100 ナノ秒の精度をサポートします。 タイムゾーンは省略可能です。<br /><br /> SQL Server 2005 では、-9999 ～ 9999 の範囲で年がサポートされていました。 SQL Server では、さらに制限された年の範囲がサポートされるようになりました。 詳細については、「 [型指定された XML と型指定されていない XML の比較](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)」を参照してください。|  
|**date**|年部分は 1 ～ 9999 の範囲で指定する必要があります。 月部分は 1 ～ 12 の範囲で指定する必要があります。 日部分は 1 ～ 31 の範囲で指定し、さらにカレンダーの日付として有効な値である必要があります。 たとえば、1974-02-31 を指定した場合、2 月には 31 日までないので、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では無効な日付として検出され、エラーを返します。<br /><br /> SQL Server 2005 では、-9999 ～ 9999 の範囲で年がサポートされていました。 SQL Server では、さらに制限された年の範囲がサポートされるようになりました。 詳細については、「 [型指定された XML と型指定されていない XML の比較](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)」を参照してください。|  
|**gYearMonth**|年部分は -9999 ～ 9999 の範囲で指定する必要があります。|  
|**gYear**|年部分は -9999 ～ 9999 の範囲で指定する必要があります。|  
|**gMonthDay**|月部分は 1 ～ 12 の範囲で指定する必要があります。 日部分は 1 ～ 31 の範囲で指定する必要があります。|  
|**gDay**|日部分は 1 ～ 31 の範囲で指定する必要があります。|  
|**gMonth**|月部分は 1 ～ 12 の範囲で指定する必要があります。|  
|**decimal**|この型の値は SQL 数値型の形式に従っている必要があります。 この型では、内部的には合計 38 桁までの数値が表現されます。そのうち 10 桁は、小数部分の有効桁数として予約されています。|  
|**float**|この型の値は、SQL **real** 型の形式に準拠している必要があります。|  
|**double**|この型の値は、SQL **float** 型の形式に準拠している必要があります。|  
|**string**|この型の値は、SQL **nvarchar(max)** 型の形式に準拠している必要があります。|  
|**anyURI**|この型の値の長さは Unicode 文字 4,000 文字が上限です。|  
  
## <a name="see-also"></a>参照  
 [サーバー上の XML スキーマ コレクションの要件と制限](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
