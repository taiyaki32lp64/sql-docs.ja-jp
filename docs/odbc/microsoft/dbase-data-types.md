---
title: dBASE データ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], data types
- data types [ODBC], DBase driver
- dbase data types [ODBC]
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: a0e31e6b-d02b-4ee2-9b37-5baf6a11c0a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1753e0d50655205bc6f459548f2ef2b77d5cc885
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096451"
---
# <a name="dbase-data-types"></a>dBASE データ型
次の表では、dBASE データ型を ODBC SQL データ型にマップする方法を示します。 すべての ODBC SQL データ型がサポートされていることに注意してください。  
  
|dBASE データ型|ODBC データ型|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|[DATE]|SQL_DATE|  
|FLOAT [1]|SQL_DOUBLE|  
|論理|SQL_BIT|  
|メモ|SQL_LONGVARCHAR|  
|数値 (BCD)|SQL_DOUBLE|  
|OLEOBJECT[1]|SQL_LONGBINARY|  
  
 DBASE バージョン 5 には [1] 有効です。*x*  
  
 DBASE の有効桁数 III を行うと数値でを 2 桁の指数部で dBASE IV 番号 3 桁の指数。 数値はテキストとして格納されている、ため、数値に変換されます。 変換する数値が収まらない場合、フィールドに、予期しない結果が発生する可能性があります。  
  
 DBASE で、precision と scale 数値データ型を指定するのには、中に、ODBC の dBASE ドライバーではサポートされません。 ODBC の dBASE ドライバーは、常に、15 の有効桁数と小数点数値データ型の場合は 0 を返します。  
  
 ODBC の SQL_DOUBLE データ型を ODBC dBASE ドライバーのマップを使用して、数値データ型で作成された列です。 したがって、この列のデータは丸め処理の対象は。 この動作は、Binary Coded Decimal (BCD) である dBASE (型 N) に入力を数値データのない同じです。  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC SQL データ型を返します。 付録 d のすべての変換、 *ODBC プログラマ リファレンス*このトピックで前述した ODBC SQL データ型はサポートされます。  
  
 次の表は、データ型、dBASE の制限事項を示します。  
  
|データの種類|説明|  
|---------------|-----------------|  
|CHAR|0 の char 型の列を作成または指定されていない長さが実際に 254 バイト列を返します。|  
|暗号化データ|DBASE ドライバーでは、dBASE テーブルをサポートしません。|  
|論理|DBASE ドライバーは、論理列にインデックスを作成することはできません。|  
|メモ|メモ列の最大長は、65,500 バイトです。|  
  
 データ型の複数の制限事項が記載[データ型の制限事項](../../odbc/microsoft/data-type-limitations.md)します。
