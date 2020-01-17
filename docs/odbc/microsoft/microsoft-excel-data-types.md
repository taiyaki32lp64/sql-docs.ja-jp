---
title: Microsoft Excel のデータ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5a8385c8efb1ab7dcee651e5acb52062292a0bcc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045017"
---
# <a name="microsoft-excel-data-types"></a>Microsoft Excel のデータ型
次の表では、Microsoft Excel ドライバーのデータ型を ODBC SQL データ型にマップする方法を示します。 Microsoft Excel ドライバーでは、列のデータに基づく Microsoft Excel のテーブル内の列にこれらのデータ型が割り当てられます。  
  
|Microsoft Excel のデータ型|ODBC データ型|  
|-------------------------------|--------------------|  
|通貨|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|論理|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|[TEXT]|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC SQL データ型を返します。 付録 d のすべての変換、 *ODBC プログラマ リファレンス*このトピックで前述した ODBC SQL データ型はサポートされます。  
  
 次の表では、Microsoft Excel のデータ型の制限事項を示します。  
  
|データの種類|説明|  
|---------------|-----------------|  
|暗号化データ|Microsoft Excel ドライバーでは、暗号化されたデータを読み取ることができません。|  
|エラー文字列|Microsoft Excel ドライバーは、Microsoft Excel エラー値の文字の文字列を返すことはできません (#n/a!、#value!!、#REF!、#DIV/0!、#num!!、#NAME? と #NULL!)、代わりに NULL を返しますが。|  
|論理|論理列の値は、0 または 1 のいずれかとして、SQL_C_CHAR バッファーに返されます。|  
|NUMBER|整数型の列が作成された場合は、整数データ型に対して大きすぎる数値を入力することができます、および SQL_DOUBLE に列を変換する可能性があります結果で、整数以外の値を含むデータを挿入することができます。|  
|[TEXT]|列の行に 1 つ以上の Microsoft Excel のデータ型が含まれている場合、Microsoft Excel の ODBC ドライバーは、列に SQL_VARCHAR データ型を割り当てます。 これを 1 つの例外があります: Microsoft Excel の ODBC ドライバーが、SQL_TIMESTAMP データ型を列に割り当て、datetime データ型 (日付、時刻、および DATETIME) の 3 つまたは 2 つだけが、列が含まれる場合。<br /><br /> 0 のテキスト列を作成または指定されていない長さが実際には 255 バイト列を返します。<br /><br /> 文字の文字列リテラルは、(1 ~ 255 の 10 進数) の任意の ANSI 文字を含めることができます。 2 つの連続する単一引用符 (") を使用して、1 つの単一引用符 (') を表します。<br /><br /> SQL_VARCHAR 以外のデータ型の列に NULL を挿入すると、SQL_VARCHAR に変更する列のデータ型が発生します。|  
  
 データ型の複数の制限事項が記載[データ型の制限事項](../../odbc/microsoft/data-type-limitations.md)します。
