---
title: DB-LIBRARY から ODBC への一括コピー |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- converting DB-Library to ODBC bulk copy
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], DB-Library bulk copy
- ODBC, bulk copy operations
- DB-Library bulk copy
ms.assetid: 0bc15bdb-f19f-4537-ac6c-f249f42cf07f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b7e14018ea62edb5dd262b87ddbea467d1872132
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73785189"
---
# <a name="converting-from-db-library-to-odbc-bulk-copy"></a>DB-Library から ODBC への一括コピーの変換
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでサポートされている一括コピー関数は DB-LIBRARY 一括コピー関数に似ているため、DB-LIBRARY 一括コピープログラムを ODBC に変換するのは簡単です。ただし、次のような例外があります。  
  
-   DB-Library アプリケーションでは、DBPROCESS 構造体を指すポインターを一括コピー関数の最初のパラメーターに渡します。 ODBC アプリケーションでは、DBPROCESS ポインターが ODBC 接続ハンドルに置き換わります。  
  
-   DB-LIBRARY アプリケーションは、接続する前に**BCP_SETL**を呼び出し、DBPROCESS での一括コピー操作を有効にします。 ODBC アプリケーションでは、接続ハンドルに対して一括操作を有効にするために接続する前に[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)を呼び出します。  
  
    ```  
    SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP,  
        (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
    ```  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、DB-LIBRARY メッセージとエラーハンドラーがサポートされていません。ODBC 一括コピー関数によって発生したエラーとメッセージを取得するには、 **SQLGetDiagRec**を呼び出す必要があります。 ODBC バージョンの一括コピー関数は、標準的な一括コピーのリターン コードである SUCCEED または FAILED を返しますが、SQL_SUCCESS や SQL_ERROR など、ODBC 形式のリターン コードを返しません。  
  
-   DB-LIBRARY [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)の*varlen*パラメーターに指定された値は、ODBC **bcp_bind**の_cbdata_パラメーターとは異なる解釈になります。  
  
    |指定された条件|DB-LIBRARY の*varlen*値|ODBC *Cbdata*値|  
    |-------------------------|--------------------------------|-------------------------|  
    |NULL 値が指定された場合|0|-1 (SQL_NULL_DATA)|  
    |可変長のデータが指定された場合|-1|-10 (SQL_VARLEN_DATA)|  
    |長さが 0 の文字列またはバイナリ文字列の場合|NA|0|  
  
     DB-LIBRARY では、 *varlen*値-1 は、可変長データが指定されていることを示します。これは、ODBC *CBDATA*で、NULL 値のみが指定されていることを意味します。 DB-LIBRARY のすべての*varlen*仕様 (-1) を SQL_VARLEN_DATA に、および0のすべての*varlen*仕様を SQL_NULL_DATA に変更します。  
  
-   DB-LIBRARY **bcp_colfmt**_file_collen_と ODBC [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)*の cbuserdata*には、上記で説明した**bcp_bind**の_varlen_および*cbdata*パラメーターと同じ問題があります。 -1 の DB-LIBRARY *file_collen*仕様をすべて SQL_VARLEN_DATA に変更*file_collen*し、0を SQL_NULL_DATA に設定します。  
  
-   ODBC [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)関数の*ivalue*パラメーターは void ポインターです。 DB-LIBRARY では、 *Ivalue*は整数でした。 ODBC *Ivalue*の値を void * にキャストします。  
  
-   **Bcp_control**オプション BCPMAXERRS では、一括コピー操作が失敗する前にエラーが発生する個々の行の数を指定します。 BCPMAXERRS の既定値は 0 (最初のエラーの場合は fail) で、ODBC バージョンでは**bcp_control**と10の db-library バージョンでは10です。 既定値の0に依存して一括コピー操作を終了する DB-LIBRARY アプリケーションは、BCPMAXERRS を0に設定するために ODBC **bcp_control**を呼び出すように変更する必要があります。  
  
-   ODBC **bcp_control**関数は、 **bcp_control**の db-library バージョンでサポートされていない次のオプションをサポートしています。  
  
    -   BCPODBC  
  
         TRUE に設定すると、文字形式で保存される**datetime**と**smalldatetime**の値に、ODBC タイムスタンプエスケープシーケンスのプレフィックスとサフィックスが含まれるように指定します。 これは、BCP_OUT 操作に対してのみ適用されます。  
  
         BCPODBC.BCP を FALSE に設定すると、文字列に変換される**datetime**値は次のように出力されます。  
  
        ```  
        1997-01-01 00:00:00.000  
        ```  
  
         BCPODBC.BCP を TRUE に設定すると、同じ**datetime**値が次のように出力されます。  
  
        ```  
        {ts '1997-01-01 00:00:00.000' }  
        ```  
  
    -   BCPKEEPIDENTITY  
  
         TRUE に設定した場合、一括コピー関数で、ID 制約を含む列に対して指定したデータ値が挿入されることを示します。 このオプションを設定しないと、挿入される行に対して新しい ID 値が生成されます。  
  
    -   BCPHINTS  
  
         一括コピーのさまざまな最適化を指定します。 このオプションは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 以前のバージョンでは使用できません。  
  
    -   BCPFILECP  
  
         一括コピー ファイルのコード ページを指定します。  
  
    -   BCPUNICODEFILE  
  
         キャラクター モードの一括コピー ファイルが Unicode ファイルであることを指定します。  
  
-   Odbc の**bcp_colfmt**関数では、odbc SQLCHAR typedef と競合するため、SQLCHAR の*file_type*インジケーターはサポートされません。 **Bcp_colfmt**ではなく sqlcharacter を使用してください。  
  
-   ODBC バージョンの一括コピー関数では、文字列内の**datetime**値と**smalldatetime**値を操作するための形式は、yyyy-mm-dd hh: MM: ss の odbc 形式です。**smalldatetime**の値には、yyyy-mm-dd hh: mm: SS の ODBC 形式を使用します。  
  
     DB-LIBRARY バージョンの一括コピー関数では、いくつかの形式を使用して、文字列内の**datetime**値と**smalldatetime**値を受け取ることができます。  
  
    -   既定の形式は*mmm dd yyyy hh: mmxx*です。ここで*XX*は、AM または PM です。  
  
    -   DB-LIBRARY **dbconvert**関数でサポートされている任意の形式の**datetime**文字列および**smalldatetime**文字列。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントネットワークユーティリティの DB-LIBRARY **[オプション]** タブで **[インターナショナル設定を使用する]** チェックボックスがオンになっている場合、db-library 一括コピー関数は、ロケール設定に定義されている地域の日付形式の日付も受け入れます。クライアントコンピューターのレジストリ。  
  
     DB-LIBRARY 一括コピー関数では、ODBC **datetime**および**smalldatetime**形式は使用できません。  
  
     SQL_SOPT_SS_REGIONALIZE ステートメント属性を SQL_RE_ON に設定すると、ODBC の一括コピー関数はクライアント コンピューターのレジストリのロケール設定に定義された地域別の日付形式のデータを受け取ります。  
  
-   文字形式で**通貨**値を出力する場合、ODBC 一括コピー関数では、有効桁数が4桁、コンマ区切り文字が指定されません。DB-LIBRARY バージョンでは、2桁の有効桁数が指定され、コンマ区切り記号が含まれます。  
  
## <a name="see-also"></a>参照  
 [一括コピー操作&#40;の実行&#41; ODBC](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [一括コピー関数](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
