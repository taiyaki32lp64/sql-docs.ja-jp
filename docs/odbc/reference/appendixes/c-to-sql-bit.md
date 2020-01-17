---
title: 'C から SQL へ: ビット |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], bit
- bit data type [ODBC]
- data conversions from C to SQL types [ODBC], bit
ms.assetid: 267c9fa9-599e-4ee6-b51b-0cae43f09183
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8cc5e26b30816d0989dca90566a1a5de008b71c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019421"
---
# <a name="c-to-sql-bit"></a>C から SQL へ: ビット
ODBC C データ型の識別子を示します。  
  
 SQL_C_BIT  
  
 次の表は、ODBC SQL データ型のビット C のデータを変換する可能性がありますを示します。 列とテーブルの用語の詳細については、次を参照してください。 [C から SQL データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)します。  
  
|SQL 型識別子|テスト|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR<br /><br /> SQL_WCHAR SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|なし|n/a|  
|SQL_DECIMAL SQL_NUMERIC<br /><br /> SQL_TINYINT SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT<br /><br /> SQL_REAL 使用できます。<br /><br /> SQL_DOUBLE|なし|n/a|  
|SQL_BIT|なし|n/a|  
  
 ドライバーでは、ビット C データ型からデータを変換するときに長さ/インジケーター値を無視し、データ バッファーのサイズがビット C データ型のサイズであると仮定します。 長さまたはインジケーターの値が渡さ、 *StrLen_or_Ind*引数**SQLPutData**とで指定したバッファー、 *StrLen_or_IndPtr* 引数**SQLBindParameter**します。 データ バッファーを指定した、 *DataPtr*引数**SQLPutData**と*ParameterValuePtr*引数**SQLBindParameter**.
