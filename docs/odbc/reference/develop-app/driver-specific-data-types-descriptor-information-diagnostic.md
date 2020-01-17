---
title: ドライバー固有の型のデータ、記述子では、診断 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver-specific diagnostic values [ODBC]
- diagnostic information [ODBC], driver-specific values
- ODBC drivers [ODBC], driver-specific diagnostic values
ms.assetid: ad4c76d3-5191-4262-b47c-5dd1d19d1154
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa17a5552855916798c78e0e7d371b58e58a401e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046924"
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>ドライバー固有のデータ型、記述子の種類、情報の種類、診断型、および属性
ドライバーは、次のドライバー固有の値を割り当てることができます。  
  
-   **SQL データ型を表すインジケーター**使用されます*ParameterType*で**SQLBindParameter**し*DataType*で**SQLGetTypeInfo**によって返されると**SQLColAttribute**、 **SQLColumns**、 **SQLDescribeCol**、 **SQLGetTypeInfo**、 **SQLDescribeParam**、 **SQLProcedureColumns**、および**SQLSpecialColumns**します。  
  
-   **記述子フィールド**使用されます*FieldIdentifier*で**SQLColAttribute**、 **SQLGetDescField**、および**SQLSetDescField**.  
  
-   **診断フィールド**使用されます*DiagIdentifier*で**SQLGetDiagField**と**SQLGetDiagRec**します。  
  
-   **情報の種類**使用されます*情報の種類*で**SQLGetInfo**します。  
  
-   **接続とステートメント属性**使用されます*属性*で**SQLGetConnectAttr**、 **SQLGetStmtAttr**、 **SQLSetConnectAttr**、および**SQLSetStmtAttr**します。  
  
 これらの項目ごとは、値の 2 つのセットがあります: odbc の予約の値と値のドライバーで使用するために予約されています。 ドライバー固有の値を実装する前にドライバー ライターは、Open Group から各ドライバー固有の型、フィールド、または属性の値を要求する必要があります。 新しいドライバーは、開発用には、次の表で説明されている範囲を使用します。 次に示す範囲内にない不明な値が使用されている場合、ODBC 3.8 ドライバー マネージャーはエラーを生成しません。 ただし、以降のバージョンのドライバー マネージャーは、不明な値が受信した範囲にない場合、エラーを生成可能性があります。  
  
 これらの値は、ODBC 関数に渡される、ドライバーが、値が有効かどうかを確認する必要があります。 ドライバーは SQLSTATE HYC00 を返します (省略可能な機能が実装されていません) の他のドライバーに適用されるドライバー固有の値。  
  
 ODBC 3.8 以降、ドライバーの作成者は、予約済みの範囲内でドライバー固有の属性に割り当てることができます。  
  
> [!NOTE]  
>  ODBC 3.8 ドライバー マネージャーで検証も旧バージョンとの互換性のため、これらの範囲を適用します。 ただし、今後のバージョンのドライバー マネージャーを適用して、可能性があります。  
  
|属性の型|ODBC データ型|基本ドライバー固有の範囲|ドライバー固有の範囲の制限|ドライバー固有の値範囲ベースの ODBC 定数|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|SQL データ型を表すインジケーター|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|記述子フィールド|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|診断フィールド|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|情報の種類|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|接続属性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|ステートメント属性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  ドライバーのドキュメントでは、ドライバー固有のデータ型、記述子フィールド、診断フィールド、情報の種類、ステートメント属性、および接続属性を記述する必要があります。 これらの値は、ODBC 関数に渡される、ドライバーが、値が有効かどうかを確認する必要があります。 ドライバーは SQLSTATE HYC00 を返します (省略可能な機能が実装されていません) の他のドライバーに適用されるドライバー固有の値。  
  
 基本の値は、ドライバーの開発を容易に定義されます。 たとえば、ドライバー固有の診断属性は、次の形式で定義できます。  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
