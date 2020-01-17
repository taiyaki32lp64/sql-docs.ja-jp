---
title: 'C から SQL へ: 文字 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- character data type [ODBC]
- data conversions from C to SQL types [ODBC], character
- converting data from c to SQL types [ODBC], character
ms.assetid: be66188a-ebdb-4c9e-af72-c379886766fa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f30e0cf7622de5124cb151288417bb508354ce0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037723"
---
# <a name="c-to-sql-character"></a>C から SQL へ: 文字
ODBC C データ型の文字の識別子は次のとおりです。  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 次の表は、ODBC SQL データ型が C の文字データを変換する可能性がありますを示します。 列とテーブルの用語の詳細については、次を参照してください。 [C から SQL データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)します。  
  
> [!NOTE]  
>  文字データが Unicode SQL データに変換されると、Unicode データの長さは偶数である必要があります。  
  
|SQL 型識別子|テスト|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|データのバイト長 < = 列の長さ。<br /><br /> データのバイト長 > 列の長さ。|n/a<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|データの長さを文字 < = 列の長さ。<br /><br /> データの文字長 > 列の長さ。|n/a<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|データを切り捨てることがなく変換<br /><br /> データ変換 [e] 桁の小数部の切り捨て<br /><br /> [E]\(ではなく小数部) の整数桁の数字が失われる結果のデータの変換<br /><br /> データの値が、*数値リテラル*|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|データが数の変換先のデータ型の範囲内<br /><br /> データが数の変換先のデータ型の範囲外です。<br /><br /> データの値が、*数値リテラル*|n/a<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|データが 0 または 1 です。<br /><br /> データが 2 よりも小さいと 1 に等しく、0 より大きい<br /><br /> データが 0 未満またはより大きい、または 2 と等しい<br /><br /> データは、*数値リテラル*|n/a<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(データのバイト長)/2 < = バイト長の列<br /><br /> (データのバイト長)/2 > バイト長の列<br /><br /> データの値が 16 進数の値|n/a<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|データの値が有効な*ODBC の日付リテラル*<br /><br /> データの値が有効な*ODBC タイムスタンプのリテラル*時刻部分が 0 です。<br /><br /> データの値が有効な*ODBC タイムスタンプのリテラル*時刻部分は、0 以外の場合 [a]。<br /><br /> データの値が有効な*ODBC の日付リテラル*または*ODBC タイムスタンプのリテラル*|n/a<br /><br /> n/a<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|データの値が有効な*ODBC 時刻のリテラル*<br /><br /> データの値が有効な*ODBC タイムスタンプのリテラル*; 小数秒の部分が 0 [b]<br /><br /> データの値が有効な*ODBC タイムスタンプのリテラル*; 小数秒の部分が 0 以外の場合 [b]<br /><br /> データの値が有効な*ODBC 時刻のリテラル*または*ODBC タイムスタンプのリテラル*|n/a<br /><br /> n/a<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|データの値が有効な*ODBC タイムスタンプのリテラル*; 小数秒の部分を切り捨てることができません<br /><br /> データの値が有効な*ODBC タイムスタンプのリテラル*; 小数秒の部分を切り捨てる<br /><br /> データの値が有効な*ODBC の日付リテラル*[c]<br /><br /> データの値が有効な*ODBC 時刻のリテラル*[d]<br /><br /> データの値が有効な*ODBC の日付リテラル*、 *ODBC 時刻のリテラル*、または*ODBC タイムスタンプのリテラル*|n/a<br /><br /> 22008<br /><br /> n/a<br /><br /> n/a<br /><br /> 22018|  
|すべての SQL interval 型|データの値が有効な*間隔値*; 切り捨ては行われません<br /><br /> データの値が有効な*間隔値*; で、フィールドのいずれかの値は切り捨てられます<br /><br /> データの値がリテラルの有効期間です。|n/a<br /><br /> 22015<br /><br /> 22018|  
  
 [a] タイムスタンプの時刻部分が切り詰められています。  
  
 [b] タイムスタンプの日付部分は無視されます。  
  
 [c]、タイムスタンプの時刻部分は、0 に設定されます。  
  
 [d] タイムスタンプの日付部分は、現在の日付に設定されます。  
  
 [e]/ドライバーのデータ ソースは、効果的に文字列全体が受信されるまでに待機 (への呼び出しで部分の文字データが送信される場合でも**SQLPutData**) 変換を実行する前にします。  
  
 文字データは、数値に変換後の日付、時刻、または SQL データのタイムスタンプは、先頭と末尾の空白は無視されます。  
  
 SQL データのバイナリを文字データを変換するときに、各 2 バイトの文字データはバイナリ データの 1 バイト (8 ビット) に変換されます。 各 2 バイトの文字データは、16 進形式の数を表します。 たとえば、「01」は 00000001 をバイナリに変換され、"FF"は、バイナリで 11111111 に変換されます。  
  
 ドライバーは常に 16 進数のペアをバイト単位に変換し、null 終了バイトを無視します。 このため、文字の文字列の長さが奇数の場合は、(存在する場合、null 終了バイトを除く)、文字列の最後のバイトを変換することはされません。  
  
> [!NOTE]  
>  アプリケーション開発者は、SQL のバイナリ データ型を文字データをバインドしないことお勧めします。 この変換は、通常非効率的で低速です。
