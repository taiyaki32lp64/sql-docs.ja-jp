---
title: SQLBindParameter |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBindParameter function
ms.assetid: c302c87a-e7f4-4d2b-a0a7-de42210174ac
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aec817b4ea5ada840ce7fe843a42f636b7494219
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73787772"
---
# <a name="sqlbindparameter"></a>SQLBindParameter
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLBindParameter**を使用すると、NATIVE client ODBC ドライバー [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にデータを提供するときに、データ変換の負担をなくすことができます。これにより、アプリケーションのクライアントコンポーネントとサーバーコンポーネントの両方でパフォーマンスが大幅に向上します。 その他に、概数データ型を挿入または更新するときに有効桁数を失うことが少なくなるという利点もあります。  
  
> [!NOTE]  
>  **Char**型と**wchar**型のデータを image 型の列に挿入する場合は、バイナリ形式に変換した後のデータサイズではなく、渡されるデータのサイズが使用されます。  
  
 パラメーター配列の配列要素の 1 つで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバー エラーが発生しても、残りの配列要素に対しては引き続きステートメントが実行されます。 アプリケーションがこのステートメントのパラメーター状態要素の配列をバインドした場合は、その配列を基にして、エラーが発生したパラメーター行を特定できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーを使用する場合は、入力パラメーターのバインド時に SQL_PARAM_INPUT を指定します。 OUTPUT キーワードで定義されたストアド プロシージャ パラメーターをバインドするときは、SQL_PARAM_OUTPUT または SQL_PARAM_INPUT_OUTPUT のみを指定してください。  
  
 [SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md)は、バインドされたパラメーター配列の配列要素によってステートメントの実行でエラーが発生した場合に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC ドライバーと互換性がありません。 また、ODBC ステートメント属性 SQL_ATTR_PARAMS_PROCESSED_PTR は、エラーが発生する前に処理された行数を報告します。 その後、必要に応じてパラメーター状態配列全体をアプリケーションで調査することにより、正常に実行されたステートメント数を検出できます。  
  
## <a name="binding-parameters-for-sql-character-types"></a>SQL 文字型のパラメーターのバインド  
 渡された SQL データ型が文字型の場合、 *Columnsize*は文字数 (バイト数ではない) のサイズになります。 データ文字列の長さが8000を超える場合、 *Columnsize*を**SQL_SS_LENGTH_UNLIMITED**に設定し、SQL 型のサイズに制限がないことを示します。  
  
 たとえば、SQL データ型が**SQL_WVARCHAR**の場合、 *columnsize*を4000より大きくすることはできません。 実際のデータ長が4000より大きい場合は、 **nvarchar (max)** がドライバーによって使用されるように*columnsize*を**SQL_SS_LENGTH_UNLIMITED**に設定する必要があります。  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter とテーブル値パラメーター  
 他のパラメーターの型と同様に、テーブル値パラメーターは SQLBindParameter によってバインドされます。  
  
 テーブル値パラメーターがバインドされた後、そのパラメーターの列もバインドされます。 列をバインドするには、 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)を呼び出して、テーブル値パラメーターの序数に SQL_SOPT_SS_PARAM_FOCUS を設定します。 次に、テーブル値パラメーターの各列に対して SQLBindParameter を呼び出します。 最上位パラメーター バインドに戻るには、SQL_SOPT_SS_PARAM_FOCUS に 0 を設定します。  
  
 テーブル値パラメーターの記述子フィールドへのパラメーターのマッピングの詳細については、「[テーブル値パラメーターと列の値のバインドとデータ転送](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)」を参照してください。  
  
 テーブル値パラメーターの詳細については、「[テーブル値パラメーター &#40;の&#41;ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)」を参照してください。  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>SQLBindParameter による機能強化された日付と時刻のサポート  
 日付型または時刻型のパラメーター値は、「 [C から SQL への変換](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)」で説明されているように変換されます。 **Time**と**datetimeoffset**型のパラメーターには、対応する構造 (**SQL_SS_TIME2_STRUCT**および**SQL_SS_TIMESTAMPOFFSET_STRUCT**) が使用されている場合、 **SQL_C_DEFAULT**または**SQL_C_BINARY**として指定された*ValueType*が必要です。  
  
 詳細については、「[日付と&#40;時刻&#41;の機能強化 ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)」を参照してください。  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>SQLBindParameter による大きな CLR UDT のサポート  
 **SQLBindParameter**は、大きな CLR ユーザー定義型 (udt) をサポートしています。 詳細については、「 [LARGE CLR ユーザー定義&#40;型&#41;ODBC](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLBindParameter 関数](https://go.microsoft.com/fwlink/?LinkId=59328)  
  
  
