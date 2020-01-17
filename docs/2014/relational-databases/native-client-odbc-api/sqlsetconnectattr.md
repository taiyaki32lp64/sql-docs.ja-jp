---
title: SQLSetConnectAttr |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSetConnectAttr function
ms.assetid: d21b5cf1-3724-43f7-bc96-5097df0677b4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1b48f9ee2e7ee3092e3f31fd6ef97e91c5cd9db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207104"
---
# <a name="sqlsetconnectattr"></a>SQLSetConnectAttr
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、SQL_ATTR_CONNECTION_TIMEOUT の設定が無視されます。  
  
 SQL_ATTR_TRANSLATE_LIB も無視されます。他の変換ライブラリの指定はサポートされていません。 Microsoft ODBC driver for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用するように、アプリケーションを簡単に移植できるようにするには、SQL_ATTR_TRANSLATE_LIB で設定される値をドライバー マネージャーのバッファーにコピーしたり、そこからコピーしたりするようにします。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、REPEATABLE READ トランザクション分離レベルが SERIALIZABLE として実装されます。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で、新しいトランザクション分離レベル属性 SQL_COPT_SS_TXN_ISOLATION のサポートが導入されました。 SQL_COPT_SS_TXN_ISOLATION を SQL_TXN_SS_SNAPSHOT に設定すると、トランザクションがスナップショット分離レベルで実行されることが報告されます。  
  
> [!NOTE]  
>  SQL_ATTR_TXN_ISOLATION は、SQL_TXN_SS_SNAPSHOT 以外のすべての分離レベルを設定する場合に使用できます。 スナップショット分離を使用する場合は、SQL_COPT_SS_TXN_ISOLATION を使用して SQL_TXN_SS_SNAPSHOT を設定する必要があります。 ただし、スナップショット分離レベルは SQL_ATTR_TXN_ISOLATION または SQL_COPT_SS_TXN_ISOLATION のどちらを使用しても取得することはできます。  
  
 ODBC ステートメントの属性を接続属性に昇格すると、予期しない結果が生じることがあります。 結果セットの処理にサーバー カーソルを必要とするステートメント属性は、接続属性に昇格できます。 たとえば、ODBC ステートメント属性 SQL_ATTR_CONCURRENCY に既定値の SQL_CONCUR_READ_ONLY よりも制限の厳しい値を設定すると、ドライバーはその接続で送信されるすべてのステートメントに動的カーソルを使用します。 この接続から送信されるステートメントで ODBC カタログ関数を実行すると、SQL_SUCCESS_WITH_INFO とカーソルの動作が読み取り専用に変更されたことを示す診断レコードが返されます。 この接続で、COMPUTE 句を含む Transact-SQL の SELECT ステートメントを実行すると、ステートメントの実行に失敗します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、sqlncli.h で定義されているドライバー固有の ODBC 接続属性の拡張機能が多数サポートされています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが、接続前に属性を設定しておくことを必要とする場合や、既に設定されている属性に対する新たな設定を無視する場合があります。 次の表に、その制限事項を示します。  
  
|SQL Server の属性|設定タイミング (サーバーへの接続前または接続後)|  
|--------------------------|----------------------------------------------|  
|SQL_COPT_SS_ANSI_NPW|[指定日付より前]|  
|SQL_COPT_SS_APPLICATION_INTENT|[指定日付より前]|  
|SQL_COPT_SS_ATTACHDBFILENAME|[指定日付より前]|  
|SQL_COPT_SS_BCP|[指定日付より前]|  
|SQL_COPT_SS_BROWSE_CONNECT|[指定日付より前]|  
|SQL_COPT_SS_BROWSE_SERVER|[指定日付より前]|  
|SQL_COPT_SS_CONCAT_NULL|[指定日付より前]|  
|SQL_COPT_SS_CONNECTION_DEAD|After|  
|SQL_COPT_SS_ENCRYPT|[指定日付より前]|  
|SQL_COPT_SS_ENLIST_IN_DTC|After|  
|SQL_COPT_SS_ENLIST_IN_XA|After|  
|SQL_COPT_SS_FALLBACK_CONNECT|[指定日付より前]|  
|SQL_COPT_SS_FAILOVER_PARTNER|[指定日付より前]|  
|SQL_COPT_SS_INTEGRATED_SECURITY|[指定日付より前]|  
|SQL_COPT_SS_MARS_ENABLED|[指定日付より前]|  
|SQL_COPT_SS_MULTISUBMIT_FAILOVER|[指定日付より前]|  
|SQL_COPT_SS_OLDPWD|[指定日付より前]|  
|SQL_COPT_SS_PERF_DATA|After|  
|SQL_COPT_SS_PERF_DATA_LOG|After|  
|SQL_COPT_SS_PERF_DATA_LOG_NOW|After|  
|SQL_COPT_SS_PERF_QUERY|After|  
|SQL_COPT_SS_PERF_QUERY_INTERVAL|After|  
|SQL_COPT_SS_PERF_QUERY_LOG|After|  
|SQL_COPT_SS_PRESERVE_CURSORS|[指定日付より前]|  
|SQL_COPT_SS_QUOTED_IDENT|接続前/接続後|  
|SQL_COPT_SS_TRANSLATE|接続前/接続後|  
|SQL_COPT_SS_TRUST_SERVER_CERTIFICATE|[指定日付より前]|  
|SQL_COPT_SS_TXN_ISOLATION|接続前/接続後|  
|SQL_COPT_SS_USE_PROC_FOR_PREP|接続前/接続後|  
|SQL_COPT_SS_USER_DATA|接続前/接続後|  
|SQL_COPT_SS_WARN_ON_CP_ERROR|[指定日付より前]|  
  
 同じセッション、データベース、または [!INCLUDE[tsql](../../includes/tsql-md.md)] の状態に対して接続前の属性および同等の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コマンドを使用すると、予期しない動作が発生する場合があります。 例えば以下のようにします。  
  
```  
SQLSetConnectAttr(SQL_COPT_SS_QUOTED_IDENT, SQL_QI_ON) // turn ON via attribute  
SQLDriverConnect(...);  
SQLExecDirect("SET QUOTED_IDENTIFIER OFF") // turn OFF via Transact-SQL  
SQLSetConnectAttr(SQL_ATTR_CURRENT_CATALOG, ...) // restores to pre-connect attribute value  
```  
  
## <a name="sqlcoptssansinpw"></a>SQL_COPT_SS_ANSI_NPW  
 SQL_COPT_SS_ANSI_NPW 属性は、比較や連結における NULL 値、文字データ型の埋め込み、および警告の処理に対して、ISO 標準の処理を有効または無効にします。 詳細については、「SET ANSI_NULLS」、「SET ANSI_PADDING」、「SET ANSI_WARNINGS」、および「SET CONCAT_NULL_YIELDS_NULL」を参照してください。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_AD_ON|既定値です。 接続では、NULL 比較、埋め込み、警告、および NULL 連結に ANSI の既定動作が使用されます。|  
|SQL_AD_OFF|接続では、NULL、文字データ型の埋め込み、および警告の処理に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で定義された処理を使用します。|  
  
 接続プールを使用する場合は、SQLSetConnectAttr ではなく、接続文字列で SQL_COPT_SS_ANSI_NPW を設定する必要があります。 接続プールを使用している場合、接続が確立された後にこの属性を変更しようとすると、何も通知されずに失敗します。  
  
## <a name="sqlcoptssapplicationintent"></a>SQL_COPT_SS_APPLICATION_INTENT  
 アプリケーションがサーバーに接続するときのワークロードのタイプを宣言します。 設定可能な値は `Readonly` および `ReadWrite` です。 以下に例を示します。  
  
```  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_APPLICATION_INTENT, TEXT("Readonly"), SQL_NTS)  
```  
  
 既定値は `ReadWrite` です。 詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のネイティブ クライアントのサポート[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]Ag を参照してください[SQL Server ネイティブ クライアントをサポートして高可用性、ディザスター リカバリーのため](../native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)します。  
  
## <a name="sqlcoptssattachdbfilename"></a>SQL_COPT_SS_ATTACHDBFILENAME  
 SQL_COPT_SS_ATTACHDBFILENAME 属性は、アタッチ可能なデータベースのプライマリ ファイルの名前を指定します。 このデータベースがアタッチされ、接続の既定のデータベースとして使用されます。 Sql_copt_ss_attachdbfilename 属性を使用するには、接続属性 SQL_ATTR_CURRENT_CATALOG の値として、データベースの名前を指定またはデータベース内のパラメーターを = する必要があります、 [SQLDriverConnect](sqldriverconnect.md)します。 データベースが以前にアタッチされていた場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はそのデータベースを再アタッチしません。  
  
|値|説明|  
|-----------|-----------------|  
|文字列への SQLPOINTER|この文字列には、アタッチするデータベースのプライマリ ファイル名を指定します。 ファイル名には、ファイルの完全なパスを含めます。|  
  
## <a name="sqlcoptssbcp"></a>SQL_COPT_SS_BCP  
 SQL_COPT_SS_BCP 属性は、接続で一括コピー関数を有効にします。 詳細については、次を参照してください。[一括コピー関数](../native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)します。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_BCP_OFF|既定値です。 接続では一括コピー関数を使用できません。|  
|SQL_BCP_ON|接続では一括コピー関数を使用できます。|  
  
## <a name="sqlcoptssbrowseconnect"></a>SQL_COPT_SS_BROWSE_CONNECT  
 この属性を使用して返される結果セットをカスタマイズする[SQLBrowseConnect](sqlbrowseconnect.md)します。 SQL_COPT_SS_BROWSE_CONNECT 属性は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の列挙されたインスタンスから詳細情報が返されるかどうかを指定します。 この詳細情報には、サーバーがクラスター サーバーかどうか、さまざまなインスタンスの名前、およびバージョン番号などが含まれます。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_MORE_INFO_NO|既定値です。 サーバーの一覧を返します。|  
|SQL_MORE_INFO_YES|**SQLBrowseConnect**サーバーのプロパティの拡張文字列を返します。|  
  
## <a name="sqlcoptssbrowseserver"></a>SQL_COPT_SS_BROWSE_SERVER  
 この属性を使用して返される結果セットをカスタマイズする**SQLBrowseConnect**します。 SQL_COPT_SS_BROWSE_SERVER 対象のサーバー名を指定する**SQLBrowseConnect**情報を返します。  
  
|値|説明|  
|-----------|-----------------|  
|computername|**SQLBrowseConnect**のインスタンスの一覧を返します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定したコンピューター上です。 二重の円記号 (\\\\) サーバー名は使用しない必要があります (たとえばの代わりに\\\MyServer、MyServer を使用する必要があります)。|  
|NULL|既定値です。 **SQLBrowseConnect**ドメイン内のすべてのサーバー情報を返します。|  
  
## <a name="sqlcoptssconcatnull"></a>SQL_COPT_SS_CONCAT_NULL  
 SQL_COPT_SS_CONCAT_NULL 属性は、文字列を連結するときの NULL 処理に対して、ISO 標準の処理を有効または無効にします。 詳細については、「SET CONCAT_NULL_YIELDS_NULL」を参照してください。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_CN_ON|既定値です。 接続では、文字列を連結するときの NULL の処理に対して、ISO の既定の動作を使用します。|  
|SQL_CN_OFF|接続では、文字列を連結するときの NULL の処理に対して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で定義されている動作を使用します。|  
  
## <a name="sqlcoptssencrypt"></a>SQL_COPT_SS_ENCRYPT  
 接続の暗号化を制御します。  
  
 暗号化にはサーバー上の証明書が使用されます。 接続属性 SQL_COPT_SS_TRUST_SERVER_CERTIFICATE が SQL_TRUST_SERVER_CERTIFICATE_YES に設定されるか、接続文字列に "TrustServerCertificate=yes" が含まれていない限り、この証明書は証明機関によって検証される必要があります。 この両方の条件を満たしている場合、サーバー上に証明書が存在しなければ、そのサーバーによって生成および署名された証明書を使用して、接続を暗号化できます。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_EN_ON|接続が暗号化されます。|  
|SQL_EN_OFF|接続は暗号化されません。 既定値です。|  
  
## <a name="sqlcoptssenlistindtc"></a>SQL_COPT_SS_ENLIST_IN_DTC  
 クライアントは、Microsoft 分散トランザクション コーディネーター (MS DTC) OLE DB を呼び出す**itransactiondispenser::begintransaction** MS DTC トランザクションを開始し、MS DTC トランザクション オブジェクトを作成するメソッドを表す、トランザクションです。 次に、アプリケーションを呼び出す`SQLSetConnectAttr`にトランザクション オブジェクトを ODBC 接続に関連付けるには、sql_copt_ss_enlist_in_dtc にします。 関連のあるすべてのデータベース操作は、MS DTC トランザクションで保護されます。 アプリケーション呼び出し`SQLSetConnectAttr`sql_dtc_done を指定して、接続の DTC の関連付けを終了するとします。  
  
|値|説明|  
|-----------|-----------------|  
|DTC object*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にエクスポートするトランザクションを指定する MS DTC OLE トランザクション オブジェクトです。|  
|SQL_DTC_DONE|トランザクションの末尾を区切ります。|  
  
## <a name="sqlcoptssenlistinxa"></a>SQL_COPT_SS_ENLIST_IN_XA  
 クライアントが Open Group を呼び出し、XA トランザクション XA 準拠のトランザクション プロセッサ (TP) を開始する**tx_begin**関数。 次に、アプリケーションを呼び出す`SQLSetConnectAttr`XA トランザクションを ODBC 接続に関連付ける場合は TRUE、SQL_COPT_SS_ENLIST_IN_XA にパラメーターにします。 関連のあるすべてのデータベース操作は、XA トランザクションで保護されます。 XA の関連付けの ODBC 接続を終了するには、クライアントが呼び出す必要があります`SQLSetConnectAttr`SQL_COPT_SS_ENLIST_IN_XA にパラメーターを FALSE にします。 詳細については、分散トランザクション コーディネーターのマニュアルを参照してください。  
  
## <a name="sqlcoptssfallbackconnect"></a>SQL_COPT_SS_FALLBACK_CONNECT  
 この属性は現在サポートされていません。  
  
## <a name="sqlcoptssfailoverpartner"></a>SQL_COPT_SS_FAILOVER_PARTNER  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベース ミラーリングで使用するフェールオーバー パートナーの名前を指定または取得する場合に使用します。この属性値には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への最初の接続を確立する前に、NULL で終わる文字列を指定する必要があります。  
  
 この属性を使用して接続を確立するには後からアプリケーションに照会できます[SQLGetConnectAttr](sqlgetconnectattr.md)フェールオーバー パートナーの id を確認します。 プライマリ サーバーのフェールオーバー パートナーが存在しないと、この属性は空文字列を返します。 アプリケーションでは最後に判別したバックアップ サーバーをキャッシュできますが、この情報は最初に接続を確立したとき、または接続がリセットされたとき (接続がプールされている場合) にだけ更新されることに注意する必要があります。接続が長期にわたると、この情報は古くなることがあります。  
  
 詳細については、「[データベース ミラーリングの使用](../native-client/features/using-database-mirroring.md)」を参照してください。  
  
## <a name="sqlcoptssintegratedsecurity"></a>SQL_COPT_SS_INTEGRATED_SECURITY  
 SQL_COPT_SS_INTEGRATED_SECURITY 属性は、サーバー ログインでアクセス違反を検出するために Windows 認証を使用することを強制します。 Windows 認証を使用すると、ドライバーがの一部として提供されるユーザー id とパスワードの値を無視**SQLConnect**、 [SQLDriverConnect](sqldriverconnect.md)、または[SQLBrowseConnect](sqlbrowseconnect.md)処理します。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_IS_OFF|既定値です。 ログインでユーザー ID とパスワードの検証に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用します。|  
|SQL_IS_ON|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に対するユーザーのアクセス権の検証に Windows 認証を使用します。|  
  
## <a name="sqlcoptssmarsenabled"></a>SQL_COPT_SS_MARS_ENABLED  
 この属性は、複数のアクティブな結果セット (MARS) を有効または無効にします。 既定では、MARS は無効になっています。 この属性は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続を確立する前に設定する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続が開かれると、MARS の設定 (有効または無効) は接続が閉じられるまで維持されます。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_MARS_ENABLED_NO|既定値です。 複数のアクティブな結果セット (MARS) を無効にします。|  
|SQL_MARS_ENABLED_YES|MARS を有効にします。|  
  
 MARS の詳細については、次を参照してください。[複数のアクティブな結果セットのを使用して&#40;MARS&#41;](../native-client/features/using-multiple-active-result-sets-mars.md)します。  
  
## <a name="sqlcoptssmultisubnetfailover"></a>SQL_COPT_SS_MULTISUBNET_FAILOVER  
 異なるサブネット上にある [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 可用性グループ (AG) に対してアプリケーションが接続している場合、この接続プロパティによって、(現在) アクティブなサーバーを迅速に検出し、接続するように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client が構成されます。 以下に例を示します。  
  
```  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_MULTISUBMIT_FAILOVER, SQL_IS_ON, SQL_IS_INTEGER)  
```  
  
 詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のネイティブ クライアントのサポート[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]Ag を参照してください[SQL Server ネイティブ クライアントをサポートして高可用性、ディザスター リカバリーのため](../native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)します。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_IS_ON|フェールオーバーが存在する場合に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client による迅速な再接続が提供されます。|  
|SQL_IS_OFF|フェールオーバーが存在する場合に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client による迅速な再接続は提供されません。|  
  
## <a name="sqlcoptssoldpwd"></a>SQL_COPT_SS_OLDPWD  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] では、SQL Server 認証におけるパスワードの期限切れが導入されました。 クライアントから接続の古いパスワードと新しいパスワードの両方を提供できるようにするために、SQL_COPT_SS_OLDPWD 属性が追加されました。 この属性が設定されている場合、接続文字列には変更された "古いパスワード" が含まれているので、プロバイダーは最初の接続またはそれ以降の接続で接続プールを使用しません。  
  
 詳細については、次を参照してください。[プログラムでパスワードを変更する](../native-client/features/changing-passwords-programmatically.md)します。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_COPT_SS_OLD_PASSWORD|古いパスワードを含む文字列への SQLPOINTER。 この値は書き込み専用で、サーバーへの接続を確立する前に設定する必要があります。|  
  
## <a name="sqlcoptssperfdata"></a>SQL_COPT_SS_PERF_DATA  
 SQL_COPT_SS_PERF_DATA 属性は、パフォーマンス データのログ記録を開始または停止します。 データのログ ファイル名は、データのログ記録を開始する前に設定する必要があります。 詳細については、次の「SQL_COPT_SS_PERF_DATA_LOG」を参照してください。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_PERF_START|ドライバーのパフォーマンス データのサンプリングを開始します。|  
|SQL_PERF_STOP|パフォーマンス データのサンプリングのカウンターを停止します。|  
  
 詳細については、次を参照してください。 [SQLGetConnectAttr](sqlgetconnectattr.md)します。  
  
## <a name="sqlcoptssperfdatalog"></a>SQL_COPT_SS_PERF_DATA_LOG  
 SQL_COPT_SS_PERF_DATA_LOG 属性は、パフォーマンス データの記録に使用するログ ファイル名を割り当てます。 ログ ファイル名は、アプリケーションのコンパイル方法に応じて、ANSI または Unicode 形式の、NULL で終わる文字列になります。 *StringLength*引数は SQL_NTS をする必要があります。  
  
## <a name="sqlcoptssperfdatalognow"></a>SQL_COPT_SS_PERF_DATA_LOG_NOW  
 SQL_COPT_SS_PERF_DATA_LOG_NOW 属性は、ドライバーに対して、統計ログのエントリをディスクに書き込むように指定します。 *StringLength*引数は SQL_NTS をする必要があります。  
  
## <a name="sqlcoptssperfquery"></a>SQL_COPT_SS_PERF_QUERY  
 SQL_COPT_SS_PERF_QUERY 属性は、実行時間の長いクエリ用のログ記録を開始または停止します。 クエリのログ ファイル名は、ログ記録を開始する前に指定する必要があります。 アプリケーションでは、ログ記録の間隔を設定して "実行時間の長いクエリ" を定義できます。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_PERF_START|実行時間の長いクエリのログ記録を開始します。|  
|SQL_PERF_STOP|実行時間の長いクエリのログ記録を停止します。|  
  
 詳細については、次を参照してください。 [SQLGetConnectAttr](sqlgetconnectattr.md)します。  
  
## <a name="sqlcoptssperfqueryinterval"></a>SQL_COPT_SS_PERF_QUERY_INTERVAL  
 SQL_COPT_SS_PERF_QUERY_INTERVAL 属性は、クエリのログ記録のしきい値をミリ秒単位で設定します。 指定のしきい値内に解決しないクエリは、実行時間の長いクエリのログ ファイルに記録されます。 クエリのしきい値に上限はありません。 クエリのしきい値に値 0 が設定されている場合、すべてのクエリがログに記録されます。  
  
## <a name="sqlcoptssperfquerylog"></a>SQL_COPT_SS_PERF_QUERY_LOG  
 SQL_COPT_SS_PERF_QUERY_LOG 属性は、実行時間の長いクエリのデータを記録するログ ファイル名を割り当てます。 ログ ファイル名は、アプリケーションのコンパイル方法に応じて、ANSI または Unicode 形式の、NULL で終わる文字列になります。 *StringLength*引数は、SQL_NTS または文字列のバイト単位の長さ。  
  
## <a name="sqlcoptsspreservecursors"></a>SQL_COPT_SS_PRESERVE_CURSORS  
 この属性を使用して、トランザクションをコミットまたはロールバックするときに接続でカーソルを保持するかどうかを照会および設定できます。 設定値は、SQL_PC_ON または SQL_PC_OFF のどちらかです。 既定値は SQL_PC_OFF です。 この設定を制御するかどうか、ドライバーはカーソルを閉じるを呼び出すときに[SQLEndTran](sqlendtran.md) (または SQLTransact)。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_PC_OFF|既定値です。 トランザクションがコミットまたはロールバックされるときに、カーソルが閉じられますを使用してバックアップ**SQLEndTran**します。|  
|SQL_PC_ON|トランザクションがコミットまたはロールバックされるときに、カーソルは閉じられませんを使用してバックアップ**SQLEndTran**、非同期モードで静的メソッドまたはキーセット カーソルを使用する場合は除きます。 カーソルのデータ設定が完了していないときにロールバックが行われると、そのカーソルは閉じられます。|  
  
## <a name="sqlcoptssquotedident"></a>SQL_COPT_SS_QUOTED_IDENT  
 SQL_COPT_SS_QUOTED_IDENT 属性は、その接続で送信される ODBC ステートメントや Transact-SQL ステートメントにおける引用符で囲まれた識別子の使用を有効または無効にします。 引用符で囲まれた識別子を指定することにより、"My Table" のように識別子に空白が含まれていて通常は無効になるオブジェクト名も、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは許可されます。 詳細については、「SET QUOTED_IDENTIFIER」を参照してください。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_QI_OFF|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続では、送信される [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで、引用符で囲まれた識別子を指定できません。|  
|SQL_QI_ON|既定値です。 接続では、送信される [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで、引用符で囲まれた識別子を使用できます。|  
  
## <a name="sqlcoptsstranslate"></a>SQL_COPT_SS_TRANSLATE  
 SQL_COPT_SS_TRANSLATE 属性を指定すると、MBCS データを交換するときに、ドライバーによってクライアントとサーバーのコード ページ間で文字が変換されます。 属性に格納されたデータのみに影響を与えます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char**、 **varchar**、および**テキスト**列。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_XL_OFF|ドライバーでは、クライアントとサーバー間で文字データを交換する際に、あるコード ページから別のコード ページに文字が変換されません。|  
|SQL_XL_ON|既定値です。 ドライバーでは、クライアントとサーバー間で文字データを交換する際に、あるコード ページから別のコード ページに文字が変換されます。 サーバーにインストールされているコード ページとクライアントで使用されているコード ページが判別され、文字の変換が自動的に構成されます。|  
  
## <a name="sqlcoptsstrustservercertificate"></a>SQL_COPT_SS_TRUST_SERVER_CERTIFICATE  
 SQL_COPT_SS_TRUST_SERVER_CERTIFICATE 属性では、暗号化を使用しているときに、ドライバーによる証明書の検証を有効または無効にできます。 この属性の値は読み書き可能ですが、接続を確立した後に値を設定しても、設定は有効にはなりません。  
  
 クライアント アプリケーションでは、接続を開いた後にこの属性をクエリして、実際に使用されている暗号化と検証の設定を判断できます。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_TRUST_SERVER_CERTIFICATE_NO|既定値です。 証明書の検証を伴わない暗号化が無効です。|  
|SQL_TRUST_SERVER_CERTIFICATE_YES|証明書の検証を伴わない暗号化が有効です。|  
  
## <a name="sqlcoptsstxnisolation"></a>SQL_COPT_SS_TXN_ISOLATION  
 SQL_COPT_SS_TXN_ISOLATION 属性は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固有のスナップショット分離の属性を設定します。 この値は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  固有の値であるため、スナップショット分離は、SQL_ATTR_TXN_ISOLATION を使用して設定することはできません。 ただし、この値は、SQL_ATTR_TXN_ISOLATION または SQL_COPT_SS_TXN_ISOLATION のどちらを使用しても取得することはできます。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_TXN_SS_SNAPSHOT|あるトランザクションで行った変更内容を別のトランザクションから参照できないことを示します。この場合、クエリを再実行しても変更内容を参照することはできません。|  
  
 スナップショット分離の詳細については、次を参照してください。[スナップショット分離を使用した作業](../native-client/features/working-with-snapshot-isolation.md)します。  
  
## <a name="sqlcoptssuseprocforprep"></a>SQL_COPT_SS_USE_PROC_FOR_PREP  
 この属性は現在サポートされていません。  
  
## <a name="sqlcoptssuserdata"></a>SQL_COPT_SS_USER_DATA  
 SQL_COPT_SS_USER_DATA 属性は、ユーザー データのポインターを設定します。 ユーザー データとは、接続ごとに記録されているクライアントが所有するメモリのことです。  
  
 詳細については、次を参照してください。 [SQLGetConnectAttr](sqlgetconnectattr.md)します。  
  
## <a name="sqlcoptsswarnoncperror"></a>SQL_COPT_SS_WARN_ON_CP_ERROR  
 この属性は、コード ページの変換中に損失したデータがある場合に警告を表示するかどうかを指定します。 これは、サーバーから送信されるデータにのみ適用されます。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_WARN_YES|コード ページの変換中にデータの損失が発生した場合に、警告を表示します。|  
|SQL_WARN_NO|(既定値) コード ページの変換中にデータの損失が発生した場合に、警告を表示しません。|  
  
## <a name="sqlsetconnectattr-support-for-service-principal-names-spns"></a>SQLSetConnectAttr によるサービス プリンシパル名 (SPN) のサポート  
 新しい接続属性である SQL_COPT_SS_SERVER_SPN および SQL_COPT_SS_FAILOVER_PARTNER_SPN の値を設定するのには、SQLSetConnectAttr を使用できます。 接続が開いている場合、これらの属性を設定することはできません。接続が開いているときにこれらの属性を設定しようとすると、"現時点での操作は正しくありません。" というメッセージと共に、エラー HY011 が返されます (SQLSetConnectOption こともできますをこれらの値を設定します。)  
  
 Spn の詳細については、次を参照してください。[サービス プリンシパル名&#40;Spn&#41;クライアント接続で&#40;ODBC&#41;](../native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)します。  
  
## <a name="sqlcoptssconnectiondead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 これは読み取り専用属性です。  
  
 SQL_COPT_SS_CONNECTION_DEAD の詳細については、次を参照してください。 [SQLGetConnectAttr](sqlgetconnectattr.md)と[データ ソースに接続する&#40;ODBC&#41;](../native-client-odbc-communication/connecting-to-a-data-source-odbc.md)します。  
  
## <a name="example"></a>例  
 次の例では、パフォーマンス データがログに記録されます。  
  
```  
SQLPERF*     pSQLPERF;  
SQLINTEGER   nValue;  
  
// See if you are already logging. SQLPERF* will be NULL if not.  
SQLGetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA, &pSQLPERF,  
    sizeof(SQLPERF*), &nValue);  
  
if (pSQLPERF == NULL)  
    {  
    // Set the performance log file name.  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG,  
        (SQLPOINTER) "\\My LogDirectory\\MyServerLog.txt", SQL_NTS);  
  
    // Start logging...  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA,  
        (SQLPOINTER) SQL_PERF_START, SQL_IS_INTEGER);  
    }  
else  
    {  
    // Take a snapshot now so that your performance statistics are discernible.  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
    }  
  
    // ...perform some action...  
  
// ...take a performance data snapshot...  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
  
    // ...perform more actions...  
  
// ...take another snapshot...  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
  
// ...and disable logging.  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA,  
    (SQLPOINTER) SQL_PERF_STOP, SQL_IS_INTEGER);  
  
// Continue on...  
```  
  
## <a name="see-also"></a>参照  
 [SQLSetConnectAttr 関数](https://go.microsoft.com/fwlink/?LinkId=59368)   
 [ODBC API 実装の詳細](odbc-api-implementation-details.md)   
 [一括コピー関数](../native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)   
 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql)   
 [SQLPrepare 関数](https://go.microsoft.com/fwlink/?LinkId=59360)   
 [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md)  
  
  
