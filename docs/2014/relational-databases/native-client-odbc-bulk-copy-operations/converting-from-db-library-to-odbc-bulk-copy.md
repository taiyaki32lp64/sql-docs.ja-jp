---
title: Db-library から ODBC 一括コピーへの変換 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9694a5f54d740e298b9c6af4ab3169a3eb8ab14
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067628"
---
# <a name="converting-from-db-library-to-odbc-bulk-copy"></a>DB-Library から ODBC への一括コピーの変換
  一括コピー関数でサポートされているため、簡単には、Db-library 一括コピー プログラムを ODBC に変換する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、次の例外を Db-library の一括コピー関数に似ています。  
  
-   DB-Library アプリケーションでは、DBPROCESS 構造体を指すポインターを一括コピー関数の最初のパラメーターに渡します。 ODBC アプリケーションでは、DBPROCESS ポインターが ODBC 接続ハンドルに置き換わります。  
  
-   Db-library アプリケーション呼び出し**BCP_SETL**接続、DBPROCESS での一括コピー操作を有効にする前にします。 ODBC アプリケーションを呼び出す代わりに[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md)接続接続ハンドルでの一括操作を有効にする前に。  
  
    ```  
    SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP,  
        (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
    ```  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが Db-library のメッセージとエラー ハンドラーをサポートしていません。 呼び出す必要があります**SQLGetDiagRec**エラーと ODBC の一括コピー関数によって生成されたメッセージを取得します。 ODBC バージョンの一括コピー関数は、標準的な一括コピーのリターン コードである SUCCEED または FAILED を返しますが、SQL_SUCCESS や SQL_ERROR など、ODBC 形式のリターン コードを返しません。  
  
-   DB ライブラリの指定した値[bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)*varlen*パラメーターの解釈は、ODBC とは異なる**bcp_bind**_cbData_パラメーター。  
  
    |示された状態|Db-library *varlen*値|ODBC *cbData*値|  
    |-------------------------|--------------------------------|-------------------------|  
    |NULL 値が指定された場合|0|-1 (SQL_NULL_DATA)|  
    |可変長のデータが指定された場合|-1|-10 (SQL_VARLEN_DATA)|  
    |長さが 0 の文字列またはバイナリ文字列の場合|NA|0|  
  
     Db-library で、 *varlen* -1 の値は、可変長のデータが指定されていることを示します、ODBC で*cbData*は NULL 値のみが指定されていることを意味する解釈されます。 Db-library 変更*varlen* SQL_VARLEN_DATA を-1 といずれかの仕様*varlen* SQL_NULL_DATA に 0 が指定します。  
  
-   DB ライブラリ**bcp\_colfmt**_ファイル\_collen_と ODBC [bcp_colfmt](../native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)*cbUserData*が、同じ問題として、 **bcp_bind**_varlen_と*cbData*上記のパラメーター。 Db-library 変更*file_collen* SQL_VARLEN_DATA を-1 といずれかの仕様*file_collen* SQL_NULL_DATA に 0 が指定します。  
  
-   *IValue*パラメーターは、ODBC の[bcp_control](../native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)関数は void ポインターです。 Db-library では、 *iValue*が整数でした。 ODBC の値をキャスト*iValue*を void *。  
  
-   **Bcp_control** BCPMAXERRS オプションは、一括コピー操作が失敗する前に、個々 の行の数がエラーを持つことができますを指定します。 BCPMAXERRS の既定値は 0 (最初のエラーで失敗します)、Db-library バージョンの**bcp_control** ODBC のバージョンでは 10 です。 呼び出す ODBC 一括コピー操作を終了するには 0 の既定値に依存する Db-library アプリケーションを変更する必要があります**bcp_control** BCPMAXERRS を 0 に設定します。  
  
-   ODBC **bcp_control**関数は、次のオプションの Db-library バージョンでサポートされていない、サポート**bcp_control**:  
  
    -   BCPODBC  
  
         条件を満たすことを指定します。 に設定すると**datetime**と**smalldatetime** ODBC タイムスタンプ エスケープ シーケンスのプレフィックスとサフィックス文字形式で保存された値になります。 これは、BCP_OUT 操作に対してのみ適用されます。  
  
         Bcpodbc を FALSE に設定した、 **datetime**と文字の文字列に変換された値が出力されます。  
  
        ```  
        1997-01-01 00:00:00.000  
        ```  
  
         Bcpodbc を TRUE に、同じ設定**datetime**ように値が出力されます。  
  
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
  
-   ODBC **bcp_colfmt**関数がサポートされていません、 *file_type* SQLCHAR のインジケーター、ODBC SQLCHAR typedef と競合するためです。 代わりに SQLCHARACTER を使用して、 **bcp_colfmt**します。  
  
-   ODBC のバージョンの一括コピー関数を使用するための形式で**datetime**と**smalldatetime**文字の文字列の値は、ODBC の yyyy-mm-dd hh:mm:ss.sss; の形式**smalldatetime**値は、ODBC - yyyy-mm-dd hh:mm:ss の形式を使用します。  
  
     Db-library の一括コピー関数版を受け入れる**datetime**と**smalldatetime**いくつかの形式を使用して文字列内の値。  
  
    -   既定の形式は*mmm dd yyyy hh:mmxx*場所*xx*は AM または PM。  
  
    -   **datetime**と**smalldatetime** DB ライブラリでサポートされている任意の形式で文字列**dbconvert**関数。  
  
    -   ときに、**インターナショナル設定を使用して、** Db-library のチェック ボックスをオン**オプション**のタブ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]クライアント ネットワーク ユーティリティ、Db-library の一括コピー関数も受け入れる、地域の日付クライアント コンピューターのレジストリのロケール設定に定義された日付形式です。  
  
     Db-library の一括コピー関数は、ODBC を受け入れない**datetime**と**smalldatetime**形式。  
  
     SQL_SOPT_SS_REGIONALIZE ステートメント属性を SQL_RE_ON に設定すると、ODBC の一括コピー関数はクライアント コンピューターのレジストリのロケール設定に定義された地域別の日付形式のデータを受け取ります。  
  
-   出力時**money**文字形式、ODBC 一括コピー関数サプライ 4 桁の有効桁数および; なしのコンマ区切り値Db-library バージョンのみの有効桁数 2 桁の数字を指定してください、コンマ区切り記号が含まれます。  
  
## <a name="see-also"></a>参照  
 [一括コピー操作を実行する&#40;ODBC&#41;](performing-bulk-copy-operations-odbc.md)   
 [一括コピー関数](../native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
