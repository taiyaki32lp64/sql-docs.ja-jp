---
title: パラメーター値の設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter values [ODBC]
ms.assetid: 13e5da79-b60c-48d0-b467-773f481ef2a4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0bb1115290f53c19fae1aacb0a976cfcef63e086
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094232"
---
# <a name="setting-parameter-values"></a>パラメーターの値の設定
パラメーターの値を設定するには、アプリケーションは単に、パラメーターにバインドされた変数の値を設定します。 重要ではありませんこの値が設定されている場合、ステートメントが実行される前に設定されている限り、します。 アプリケーションは、変数のバインドの前後に値を設定でき、必要な回数の値を変更することができます。 ステートメントが実行されたときに、ドライバーは単に、変数の現在の値を取得します。 準備されたステートメントが複数回実行されたときに特に有効です。アプリケーションは、ステートメントが実行されるたびに、変数の一部またはすべての新しい値を設定します。 これの例は、次を参照してください。[準備された実行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)、このセクションでは以前のバージョン。  
  
 長さ/インジケーター バッファーがへの呼び出しにバインドされていたかどうか**SQLBindParameter**ステートメントの実行前に、次の値のいずれかを設定する必要があります。  
  
-   バインドされた変数内のデータのバイト長。 変数が文字またはバイナリである場合にのみ、ドライバーはこの長さを確認します。 (*ValueType* SQL_C_CHAR または SQL_C_BINARY)。  
  
-   SQL_NTS します。 データは、null で終わる文字列です。  
  
-   SQL_NULL_DATA します。 データ値が NULL の場合と、ドライバーは、バインドされた変数の値を無視します。  
  
-   SQL_DATA_AT_EXEC または SQL_LEN_DATA_AT_EXEC マクロの結果。 送信されるパラメーターの値は、 **SQLPutData**します。 詳細については、次を参照してください。[長い形式のデータを送信する](../../../odbc/reference/develop-app/sending-long-data.md)、このセクションで後述します。  
  
 次の表では、バインドされた変数とパラメーター値のさまざまなアプリケーションを設定する長さ/インジケーター バッファーの値を示します。  
  
|パラメーター<br /><br /> value|パラメーター<br /><br /> (SQL)<br /><br /> データ型 (data type)|Variable (C)<br /><br /> データ型 (data type)|値します。<br /><br /> バインドされています。<br /><br /> 変数 (variable)|値します。<br /><br /> 長さ/インジケーター<br /><br /> バッファー [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0 [a]|SQL_NTS または 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|[a] 10\0|SQL_NTS または 2|  
|午後 1 時|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13,0,0 [b]|--|  
|午後 1 時|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13: 00:00'} \0 [a]、[c]|SQL_NTS または 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a]「\0」は、null 終端文字を表します。 Null 終了文字が長さ/インジケーター バッファーの値は、SQL_NTS 場合にのみ必要です。  
  
 [この一覧に b] の数値は、TIME_STRUCT 構造体のフィールドに格納されている番号です。  
  
 [c]、文字列は、ODBC の日付のエスケープ句を使用します。 詳細については、次を参照してください。[日付、時刻、およびタイムスタンプのリテラル](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)します。  
  
 [d] ドライバーでは、SQL_NULL_DATA などの特殊な値であるかどうかを確認するには、この値を常に確認する必要があります。  
  
 ドライバーの動作が実行時にパラメーター値とはドライバーによって異なります。 必要に応じて、ドライバーは、SQL データ型、有効桁数、およびパラメーターの小数点以下桁数にバインドされた変数の C データ型とバイト長の値を変換します。 ほとんどの場合、ドライバーは、データ ソースに値を送信します。 場合によっては、テキストとして値の書式設定し、ステートメントをデータ ソースに送信する前に、SQL ステートメントに挿入します。
