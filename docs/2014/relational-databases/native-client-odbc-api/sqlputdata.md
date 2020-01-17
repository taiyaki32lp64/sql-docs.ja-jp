---
title: SQLPutData |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLPutData function
ms.assetid: d39aaa5b-7fbc-4315-a7f2-5a7787e04f25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e15353cd9f4c4a837fe5978d00259ad5460d50d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046627"
---
# <a name="sqlputdata"></a>SQLPutData
  SQLPutData を使用して、65,535 バイトを超えるデータを送信するときに、次の制限が適用されます (の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]4.21) または 400 KB を sql_longvarchar (SQL Server バージョン 6.0 以降) 用のデータを (`text`)、SQL_WLONGVARCHAR (`ntext`) またはSQL_LONGVARBINARY (`image`) 列。  
  
-   参照先のパラメーターは、 *insert_value* INSERT ステートメントでします。  
  
-   参照先のパラメーターは、*式*UPDATE ステートメントの SET 句でします。  
  
 実行するサーバーのブロック単位でデータを提供する SQLPutData 呼び出しのシーケンスを取り消す[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]バージョン 6.5 以前のバージョンを使用する場合に、列の値の部分的な更新を発生します。 `text`、 `ntext`、または`image`SQLCancel が呼び出されたときに参照された列は、中間のプレース ホルダーの値に設定されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 以前のバージョンへの接続をサポートしません。  
  
## <a name="diagnostics"></a>診断  
 1 つである[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 固有の SQLSTATE SQLPutData:  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|22026|文字列データの長さが合致しません|送信するバイトのデータの長さが指定されている場合、アプリケーションによってなどを SQL_LEN_DATA_AT_EXEC で (*n*)、 *n*経由でアプリケーションによって指定されたバイトの合計数、0 より大きいSQLPutData は、指定した長さと一致する必要があります。|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData とテーブル値パラメーター  
 SQLPutData は、テーブル値パラメーターの可変の行バインドを使用する場合、アプリケーションによって使用されます。 *StrLen_Or_Ind*パラメーターは、次の行またはテーブル値パラメーターのデータの行のデータを収集するドライバーの準備ができたこと、またはそれ以上の行が使用できることを示します。  
  
-   値が 0 を超える場合は、次の行の値のセットを使用できることを示します。  
  
-   値が 0 の場合は、送信される行がなくなったことを示します。  
  
-   値が 0 未満の場合は、エラーが発生し、"文字列長またはバッファー長が正しくありません" というメッセージで SQLState HY090 の診断レコードが記録されます。  
  
 *DataPtr*パラメーターは無視されますが、NULL 以外の値に設定する必要があります。 詳細については、可変の行バインドのセクションをご覧ください。[バインドと Data Transfer of Table-Valued パラメーターおよび列の値](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)します。  
  
 場合*StrLen_Or_Ind* SQL_DEFAULT_PARAM または 0 から SQL_PARAMSET_SIZE までの数値以外の任意の値を持つ (つまり、 *ColumnSize* SQLBindParameter のパラメーター)、エラーになります。 このエラーには、SQL_ERROR が返される SQLPutData が発生します。SQLSTATE = HY090、"無効な文字列長またはバッファー長"。  
  
 テーブル値パラメーターの詳細については、次を参照してください。[テーブル値パラメーター &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)します。  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>SQLPutData による機能強化された日付と時刻のサポート  
 日付/時刻型のパラメーターの値で説明したように変換[C から SQL への変換](../native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)。  
  
 詳細については、次を参照してください。[日付と時刻の強化&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)します。  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>SQLPutData による大きな CLR UDT のサポート  
 `SQLPutData` は、大きな CLR ユーザー定義型 (UDT) をサポートしています。 詳細については、次を参照してください。 [Large CLR User-Defined 型&#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)します。  
  
## <a name="see-also"></a>参照  
 [SQLPutData 関数](https://go.microsoft.com/fwlink/?LinkId=59365)   
 [ODBC API 実装の詳細](odbc-api-implementation-details.md)  
  
  
