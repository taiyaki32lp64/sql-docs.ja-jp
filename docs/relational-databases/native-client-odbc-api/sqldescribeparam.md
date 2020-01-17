---
title: SQLDescribeParam |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDescribeParam function
ms.assetid: 396e74b1-5d08-46dc-b404-2ef2003e4689
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aa74f982a5ff1894651d68f06689cba476a16452
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73787107"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL ステートメントのパラメーターを記述するために、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、準備された ODBC ステートメントハンドルで SQLDescribeParam が呼び出されたときに、[!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT ステートメントを構築して実行します。 この結果セットのメタデータにより、準備されたステートメント内のパラメーターの特性が決まります。 SQLDescribeParam は、SQLExecute または SQLExecDirect が返す可能性のあるエラーコードを返すことができます。  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] で始まるデータベースエンジンの機能強化により、SQLDescribeParam は予想される結果についてより正確な説明を取得できます。 これらのより正確な結果は、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で SQLDescribeParam によって返される値とは異なる場合があります。 詳細については、「[メタデータの検出](../../relational-databases/native-client/features/metadata-discovery.md)」を参照してください。  
  
 また、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]の新しい*Parametersizeptr*は、 [ODBC 仕様](https://go.microsoft.com/fwlink/?LinkId=207044)で定義されている、対応するパラメーターマーカーの列または式のサイズの定義に合わせて値を返すようになりました。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client では、 *Parametersizeptr*は、型の**SQL_DESC_OCTET_LENGTH**の対応する値、または型の SQLBindParameter に指定された関係のない列サイズの値になる可能性があります。この値は無視する必要があります (**SQL_INTEGER**など)。  
  
 ドライバーは、次の状況での SQLDescribeParam の呼び出しをサポートしていません。  
  
-   FROM 句を含む [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE ステートメントまたは DELETE ステートメントを SQLExecDirect した後。  
  
-   ODBC ステートメントまたは [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが HAVING 句にパラメーターを含んでいる場合、または SUM 関数の結果と比較される場合。  
  
-   ODBC ステートメントまたは [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがパラメーターを含んでいるサブクエリに依存している場合。  
  
-   ODBC SQL ステートメントが、比較の両方の式、LIKE、定量化された述語内にパラメーター マーカーを含んでいる場合。  
  
-   クエリのいずれかのパラメーターが関数に対するパラメーターである場合。  
  
-   コメント (/* \*/) が [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドに含まれている場合。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのバッチを処理する場合、ドライバーはバッチ内の最初のステートメントの後にあるステートメント内のパラメーターマーカーに対して SQLDescribeParam を呼び出すことをサポートしていません。  
  
 SQLDescribeParam では、準備されたストアドプロシージャのパラメーターを記述するときに、システムストアドプロシージャ[sp_sproc_columns](../../relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql.md)を使用してパラメーターの特性を取得します。 sp_sproc_columns は、現在のユーザーデータベース内のストアドプロシージャのデータをレポートできます。 完全に修飾されたストアドプロシージャ名を準備すると、データベース間で SQLDescribeParam を実行できるようになります。 たとえば、システムストアドプロシージャ[sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)を準備し、任意のデータベースで次のように実行できます。  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 準備が正常に完了した後に SQLDescribeParam を実行すると、 **master**データベースに接続したときに空の行セットが返されます。 次のように準備された同じ呼び出しは、現在のユーザーデータベースに関係なく SQLDescribeParam を成功させます。  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 大きな値のデータ型の場合、 *DataTypePtr*で返される値は SQL_VARCHAR、SQL_VARBINARY、または SQL_NVARCHAR です。 大きな値のデータ型パラメーターのサイズが "無制限" であることを示すために、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは*Parametersizeptr*を0に設定します。 実際のサイズ値は、標準の**varchar**パラメーターに対して返されます。  
  
> [!NOTE]  
>  パラメーターが SQL_VARCHAR、SQL_VARBINARY、SQL_WVARCHAR のいずれかのパラメーターの最大サイズに既にバインドされている場合は、"無制限" ではなく、バインドされたパラメーターのサイズが返されます。  
  
 サイズが "無制限" の入力パラメーターをバインドするには、実行時データを使用する必要があります。 "無制限" サイズの出力パラメーターをバインドすることはできません ( [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)が結果セットに対して行うように、出力パラメーターからデータをストリーミングする方法はありません)。  
  
 出力パラメーターの場合は、バッファーをバインドする必要があります。値が大きすぎる場合はバッファーがいっぱいになり、SQL_SUCCESS_WITH_INFO メッセージが "文字列データの右側が切り捨てられました。" という警告と共に返されます。 その後、切り捨てられたデータが破棄されます。  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam とテーブル値パラメーター  
 アプリケーションでは、SQLDescribeParam を使用して、準備されたステートメントのテーブル値パラメーター情報を取得できます。 詳細については、「準備された[ステートメントのテーブル値パラメーターのメタデータ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)」を参照してください。  
  
 一般的なテーブル値パラメーターの詳細については、「[テーブル値パラメーター &#40;の&#41;ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)」を参照してください。  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>SQLDescribeParam による機能強化された日付と時刻のサポート  
 日付型または時刻型に対して返される値を次に示します。  
  
||*DataTypePtr*|*ParameterSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|------------------------|------------------------|  
|DATETIME|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8、10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19、21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26、28..34|0..7|  
  
 詳細については、「[日付と&#40;時刻&#41;の機能強化 ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)」を参照してください。  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>SQLDescribeParam による大きな CLR UDT のサポート  
 **SQLDescribeParam**は、大きな CLR ユーザー定義型 (udt) をサポートしています。 詳細については、「 [LARGE CLR ユーザー定義&#40;型&#41;ODBC](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLDescribeParam 関数](https://go.microsoft.com/fwlink/?LinkId=59339)   
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
