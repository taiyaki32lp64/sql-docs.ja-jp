---
title: 'C から SQL へ: 年月の間隔 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
- data conversions from C to SQL types [ODBC], year-month intervals
ms.assetid: a0eb7b55-9db0-4375-9210-bddec4593880
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3db8d61bacefa8588db4c0081c6be591d7ffdacf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019278"
---
# <a name="c-to-sql-year-month-intervals"></a>C から SQL へ: 年月の間隔
年月の間隔の ODBC C データ型の識別子は次のとおりです。  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 次の表は、ODBC SQL データ型の年-月には、間隔 C のデータを変換することがありますを示します。 列とテーブルの用語の詳細については、次を参照してください。 [C から SQL データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)します。  
  
|SQL 型識別子|テスト|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR [a]<br /><br /> [A] SQL_VARCHAR<br /><br /> [A] SQL_LONGVARCHAR|列のバイト長 > バイト長の文字を =<br /><br /> 列のバイト長 < 文字バイト長 [a]<br /><br /> データの値がリテラルの有効期間です。|n/a<br /><br /> 22001<br /><br /> 22015|  
|[A] SQL_WCHAR<br /><br /> SQL_WVARCHAR [a]<br /><br /> SQL_WLONGVARCHAR[a]|列の文字の長さ > データの文字の長さを =<br /><br /> 列の文字の長さ < [a] のデータの文字長<br /><br /> データの値がリテラルの有効期間です。|n/a<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_DECIMAL [b]|単一フィールドの間隔の変換は整数の桁に切り捨てを実行できませんでした。<br /><br /> 変換の結果が整数の桁に切り捨て|n/a<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|すべてのフィールドに変換されたデータ値<br /><br /> データ値の 1 つまたは複数のフィールドが変換中に切り詰められました。|n/a<br /><br /> 22015|  
  
 [a] すべての C interval データ型は、文字データ型に変換できます。  
  
 [b] interval 構造体の型フィールドが、間隔が 1 つのフィールド (SQL_YEAR または SQL_MONTH) の場合、C の間隔の種類を (SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_DECIMAL、または SQL_NUMERIC) の任意の正確な数値に変換できます。  
  
 間隔 C 型の既定の変換では、対応する年-月間隔 SQL 型にします。  
  
 ドライバーでは、間隔 C データ型からデータを変換するとき長さ/インジケーター値を無視し、データ バッファーのサイズが間隔 C データ型のサイズであると仮定します。 長さまたはインジケーターの値が渡さ、 *StrLen_or_Ind*引数**SQLPutData**とで指定したバッファー、 *StrLen_or_IndPtr* 引数**SQLBindParameter**します。 データ バッファーを指定した、 *DataPtr*引数**SQLPutData**と*ParameterValuePtr*引数**SQLBindParameter**.
