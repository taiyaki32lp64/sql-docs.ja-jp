---
title: C から SQL への変換 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], C to SQL
ms.assetid: 7ac098db-9147-4883-8da9-a58ab24a0d31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8179b9452852777bb6d2a06018d0bf86598a5bf8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63207020"
---
# <a name="conversions-from-c-to-sql"></a>C から SQL への変換
  このトピックでは、C 型から変換する際に考慮する問題を示します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日付/時刻型です。  
  
 次の表で説明する変換は、クライアントで行われる変換に当てはまります。 パラメーターに対して、サーバーで定義されているのとは異なる、秒の小数部の有効桁数をクライアントで指定した場合、クライアントでの変換は成功しても、`SQLExecute` または `SQLExecuteDirect` を呼び出すとサーバーがエラーを返します。 具体的には、ODBC では、秒の小数部の切り捨てがエラーとして処理されますが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では丸め処理が行われます。たとえば、`datetime2(6)` を `datetime2(2)` に変換するときに丸め処理が行われます。 datetime 列の値は 1/300 秒単位に丸められ、smalldatetime 列では、サーバーによって秒が 0 に設定されます。  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
||SQL_TYPE_DATE|SQL_TYPE_TIME|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_SS_TIMSTAMPOFFSET|SQL_CHAR|SQL_WCHAR|  
|SQL_C_DATE|1|-|-|1,6|1,5,6|1,13|1,13|  
|SQL_C_TIME|-|1|1|1,7|1,5,7|1,13|1,13|  
|SQL_C_SS_TIME2|-|1,3|1,10|1,7|1,5,7|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIME2_STRUCT)|なし|なし|1,10,11|なし|なし|なし|なし|  
|SQL_C_TYPE_TIMESTAMP|1,2|1,3,4|1,4,10|1,10|1,5,10|1,13|1,13|  
|SQL_C_SS_TIMESTAMPOFFSET|1,2,8|1,3,4,8|1,4,8,10|1,8,10|1,10|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIMESTAMPOFFSET_STRUCT)|なし|なし|なし|なし|1,10,11|なし|なし|  
|SQL_C_CHAR/SQL_WCHAR (date)|9|9|9|9,6|9,5,6|なし|なし|  
|SQL_C_CHAR/SQL_WCHAR (time2)|9|9,3|9,10|9,7,10|9,5,7,10|なし|なし|  
|SQL_C_CHAR/SQL_WCHAR (datetime)|9,2|9,3,4|9,4,10|9,10|9,5,10|なし|なし|  
|SQL_C_CHAR/SQL_WCHAR (datetimeoffset)|9,2,8|9,3,4,8|9,4,8,10|9,8,10|9,10|なし|なし|  
|SQL_C_BINARY(SQL_DATE_STRUCT)|1,11|なし|なし|なし|なし|なし|なし|  
|SQL_C_BINARY(SQL_TIME_STRUCT)|なし|なし|なし|なし|なし|なし|なし|  
|SQL_C_BINARY(SQL_TIMESTAMP_STRUCT)|なし|なし|なし|なし|なし|なし|なし|  
  
## <a name="key-to-symbols"></a>記号の説明  
  
|シンボル|説明|  
|------------|-------------|  
|-|変換はサポートされていません。 "データ型の属性に関する制限に違反しました" というメッセージで SQLSTATE 07006 の診断レコードが生成されます。|  
|1|指定したデータが無効な場合、"datetime 形式が無効です" というメッセージで SQLSTATE 22007 の診断レコードが生成されます。|  
|2|時刻フィールドは 0 である必要があります。0 以外の場合、"分数が切り捨てられました" というメッセージで SQLSTATE 22008 の診断レコードが生成されます。|  
|3|秒の小数部は 0 である必要があります。0 以外の場合、"分数が切り捨てられました" というメッセージで SQLSTATE 22008 の診断レコードが生成されます。|  
|4|日付部分は無視されます。|  
|5|タイム ゾーンには、クライアントのタイム ゾーン設定が設定されます。|  
|6|時刻は 0 に設定されます。|  
|7|日付は現在の日付に設定されます。|  
|8|時間は、クライアントのタイム ゾーンから UTC に変換されます。 この変換中にエラーが発生すると、"Datetime フィールド オーバーフロー" というメッセージで SQLSTATE 22008 の診断レコードが生成されます。|  
|9|文字列は解析され、最初に検出された句読点、および残りの部分があるかどうかに応じて、date 値、datetime 値、datetimeoffset 値、time 値のいずれかに変換されます。 次に、上の表に示した規則のうち、この処理で検出された変換元の型についての規則に従って、文字列は変換先の型に変換されます。 データの解析中にエラーが検出された場合、"キャストした文字コードが正しくありません" というメッセージで SQLSTATE 22018 の診断レコードが生成されます。 datetime 型および smalldatetime 型のパラメーターでは、年がこれらの型でサポートされる範囲外の場合、"datetime 形式が無効です" というメッセージで SQLSTATE 22007 の診断レコードが生成されます。<br /><br /> datetimeoffset では、UTC への変換が必要なくても、値は UTC への変換後の範囲内に収まっている必要があります。 TDS とサーバーは datetimeoffset 値の時刻を常に UTC 用に正規化するので、クライアントは、時刻部分が、UTC への変換後にサポートされる範囲内に収まっていることを確認する必要があるためです。 値が、サポートされている UTC の範囲内に収まっていない場合、"datetime 形式が無効です" というメッセージで SQLSTATE 22007 の診断レコードが生成されます。|  
|10|データの損失を伴う切り捨てが行われると、"時間の形式が正しくありません" というメッセージで SQLSTATE 22008 の診断レコードが生成されます。 サーバーが使用する UTC の範囲で表すことができる範囲の外に値がある場合にも、このエラーが発生します。|  
|11|データのバイト長が、SQL 型が要求する構造体のサイズと等しくない場合、"数値が範囲を超えています" というメッセージで SQLSTATE 22003 の診断レコードが生成されます。|  
|12|データのバイト長が 4 バイトまたは 8 バイトの場合、データは、生の TDS smalldatetime 形式または datetime 形式でサーバーに送信されます。 データのバイト長が SQL_TIMESTAMP_STRUCT のサイズと完全に一致する場合、データは、datetime2 用の TDS 形式に変換されます。|  
|13|データの損失を伴う切り捨てが行われると、"文字列データの右側が切り捨てられました" というメッセージで SQLSTATE 22001 の診断レコードが生成されます。<br /><br /> 秒の小数部桁数 (スケール) は、以下に従って変換先列のサイズから決定されます。<br /><br /> **種類:** SQL_C_TYPE_TIMESTAMP<br /><br /> 暗黙の小数点以下桁数<br /><br /> 0<br /><br /> 19<br /><br /> 暗黙の小数点以下桁数<br /><br /> 1..9<br /><br /> 21..29<br /><br /> ただし、SQL_C_TYPE_TIMESTAMP では、データを損失することなく秒の小数部を 3 桁で表すことができる場合で、かつ、列のサイズが 23 以上である場合、ちょうど 3 桁になるように秒の小数部が生成されます。 この動作により、以前の ODBC ドライバーを使用して開発されたアプリケーションの下位互換性が保証されます。<br /><br /> テーブルの範囲よりサイズが大きい列の場合は、9 桁と見なされます。 この変換では、秒の小数点以下桁数が 9 桁まで許容されます。これは、ODBC で許容される最大桁数です。<br /><br /> 列サイズ 0 は、ODBC では可変長文字型のサイズが無制限であることを意味します (SQL_C_TYPE_TIMESTAMP の 3 桁ルールが適用されなければ 9 桁)。 固定長文字型の列サイズ 0 を指定すると、エラーになります。|  
|なし|既存の [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以前のバージョンの動作が維持されます。|  
  
## <a name="see-also"></a>関連項目  
 [日付と時刻の強化&#40;ODBC&#41;](date-and-time-improvements-odbc.md)  
  
  
