---
title: XA トランザクションについて |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 574e326f-0520-4003-bdf1-62d92c3db457
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6e7f602107e828ee0bd985345ed5e641d6870558
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027226"
---
# <a name="understanding-xa-transactions"></a>XA トランザクションについて

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] は、Java Platform, Enterprise Edition /JDBC 2.0 のオプションの分散トランザクションをサポートします。 [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) クラスから取得される JDBC 接続は、Java Platform, Enterprise Edition (Java EE) アプリケーション サーバーなどの標準分散トランザクション処理の環境に参加できます。  

> [!WARNING]  
> Microsoft JDBC Driver 4.2 (以降) for SQL には、準備されていないトランザクションを自動ロールバックする既存の機能に関する新しいタイムアウト オプションが含まれています。 詳細については、このトピックで後述する「準備されていない[トランザクションの自動ロールバックに対するサーバー側のタイムアウト設定の構成](../../connect/jdbc/understanding-xa-transactions.md#BKMK_ServerSide)」を参照してください。  

## <a name="remarks"></a>Remarks

分散トランザクションを実装するためのクラスは、次のとおりです。  
  
| クラス                                              | 実装                      | [説明]                                       |
| -------------------------------------------------- | ------------------------------- | ------------------------------------------------- |
| com.microsoft.sqlserver.jdbc.SQLServerXADataSource | javax.sql.XADataSource          | 分散された接続用のクラス ファクトリです。    |
| com.microsoft.sqlserver.jdbc.SQLServerXAResource   | javax.transaction.xa.XAResource | トランザクション マネージャー用のリソース アダプターです。 |
  
> [!NOTE]  
> XA 分散トランザクション接続の既定の分離レベルは Read Committed です。  
  
## <a name="guidelines-and-limitations-when-using-xa-transactions"></a>XA トランザクションを使用する場合のガイドラインと制限  

密に結合されたトランザクションには別途、次のガイドラインが適用されます。  

- XA トランザクションを Microsoft 分散トランザクション コーディネーター (MS DTC) と組み合わせて使用すると、現在のバージョンの MS DTC では、密に結合された XA ブランチ動作がサポートされない場合があります。 たとえば、MS DTC では、XA ブランチ トランザクション ID (XID) と MS DTC トランザクション ID とが一対一でマップされ、疎結合の XA ブランチによって実行される作業どうしが分離されます。  
  
     [MSDTC と密に結合されたトランザクション](https://support.microsoft.com/kb/938653)に関するページの修正プログラムを適用すると、密に結合された XA ブランチのサポートが有効化され、同じグローバル トランザクション ID (GTRID) を持つ複数の XA ブランチが 1 つの MS DTC トランザクション ID にマップされるようになります。 このサポートにより、密に結合された複数の XA ブランチが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] などのリソース マネージャーで相互の変更を認識できるようになります。
  
- アプリケーションは、[SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) フラグによって、XA ブランチ トランザクション ID (BQUAL) が異なり、グローバル トランザクション ID (GTRID) および形式 ID (FormatID) が同じである、密に結合された XA トランザクションを使用できるようになります。 この機能を使用するには、XAResource. start メソッドの flags パラメーターで[SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)を設定する必要があります。
  
    ```java
    xaRes.start(xid, SQLServerXAResource.SSTRANSTIGHTLYCPLD);  
    ```  
  
## <a name="configuration-instructions"></a>構成の手順

以下の手順は、分散トランザクションを処理するために XA データ ソースを Microsoft 分散トランザクション コーディネーター (MS DTC) と組み合わせて使用する場合に必要になります。  

> [!NOTE]  
> JDBC 分散トランザクション コンポーネントは、JDBC Driver のインストール先の xa ディレクトリに含まれます。 これらのコンポーネントには、xa_install.sql および sqljdbc_xa.dll のファイルが含まれます。  

> [!NOTE]  
> SQL Server 2019 public preview CTP 2.0 以降では、JDBC XA 分散トランザクションコンポーネントは SQL Server エンジンに含まれており、システムストアドプロシージャを使用して有効または無効にすることができます。
> 必要なコンポーネントが JDBC ドライバーを使用して XA 分散トランザクションを実行できるようにするには、次のストアドプロシージャを実行します。
>
> EXEC sp_sqljdbc_xa_install
>
> 以前にインストールされたコンポーネントを無効にするには、次のストアドプロシージャを実行します。
>
> EXEC sp_sqljdbc_xa_uninstall

### <a name="running-the-ms-dtc-service"></a>MS DTC サービスを実行する

MS DTC サービスは、Service Manager で **[自動]** とマークされ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの開始時に実行されている必要があります。 XA トランザクションで使用するために MS DTC を有効にするには、次の手順を実行する必要があります。  
  
Windows Vista 以降の場合:  
  
1. **[スタート]** ボタンをクリックして、 **[検索の開始]** ボックスに「**dcomcnfg**」と入力し、Enter キーを押して、 **[コンポーネント サービス]** を開きます。 **[検索の開始]** ボックスに「%windir%\system32\comexp.msc」と入力して **[コンポーネント サービス]** を開くこともできます。  
  
2. [コンポーネント サービス]、[コンピューター]、[マイ コンピューター]、[分散トランザクション コーディネーター] の順に展開します。  
  
3. **[ローカル DTC]** を右クリックし、 **[プロパティ]** を選択します。  
  
4. **[ローカル DTC のプロパティ]** ダイアログ ボックスの **[セキュリティ]** タブをクリックします。  
  
5. **[XA トランザクションを有効にする]** チェック ボックスをオンにし、 **[OK]** をクリックします。 これにより、MS DTC サービスが再開されます。
  
6. 再度 **[OK]** をクリックして **[プロパティ]** ダイアログ ボックスを閉じ、次に **[コンポーネント サービス]** を閉じます。  
  
7. MS DTC の変更が反映されるように、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を停止してから開始します。  

### <a name="configuring-the-jdbc-distributed-transaction-components"></a>JDBC 分散トランザクション コンポーネントを構成する  

次の手順を実行して、JDBC Driver 分散トランザクション コンポーネントを構成できます。  
  
1. JDBC Driver のインストール ディレクトリにある新しい sqljdbc_xa.dll を、分散トランザクションに参加するすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューターの Binn ディレクトリにコピーします。  
  
    > [!NOTE]  
    > 32 ビットの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で XA トランザクションを使用する場合は、x64 プロセッサ上に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされていても、x86 フォルダーの sqljdbc_xa.dll ファイルを使用してください。 x64 プロセッサ上にある 64 ビットの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で XA トランザクションを使用する場合は、x64 フォルダーの sqljdbc_xa.dll ファイルを使用してください。  
  
2. xa_install.sql データベース スクリプトを、分散トランザクションに参加するすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで実行します。 このスクリプトによって、sqljdbc_xa.dll から呼び出される拡張ストアド プロシージャがインストールされます。 これらの拡張ストアド プロシージャは、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] に必要な分散トランザクションと XA サポートを実装します。 このスクリプトは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの管理者として実行する必要があります。  
  
3. JDBC Driver を使用して分散トランザクションに参加する、特定のユーザーに対してアクセス許可を与えるには、そのユーザーを SqlJDBCXAUser ロールに追加します。  
  
1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して同時に構成できる sqljdbc_xa.dll アセンブリのバージョンは 1 つだけです。 アプリケーションで複数バージョンの JDBC Driver を使用し、XA 接続で、同じ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続する必要が生じる場合もあります。 そのような場合は、最新の JDBC Driver に付属する sqljdbc_xa.dll が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにインストールされている必要があります。  
  
現在、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにインストールされている sqljdbc_xa.dll のバージョンは、次の 3 とおりの方法で確認できます。
  
1. 分散トランザクションに参加する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューターの LOG ディレクトリを開きます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の "ERRORLOG" ファイルを選択して開きます。 "ERRORLOG" ファイルで、"'SQLJDBC_XA.dll' バージョンを使用して..." というフレーズを探します。  
  
2. 分散トランザクションに参加する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューターの Binn ディレクトリを開きます。 Sqljdbc_xa アセンブリを選択します。

    - Windows Vista 以降の場合: sqljdbc_xa.dll を右クリックし、[プロパティ] を選択します。 次に **[詳細]** タブをクリックします。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに現在インストールされている sqljdbc_xa.dll のバージョンが **[ファイル バージョン]** フィールドに表示されます。  
  
3. 次のセクションのコード例に従ってログ機能を設定します。 出力ログ ファイルで、"Server XA DLL バージョン:..." というフレーズを探します。  

### <a name="BKMK_ServerSide"></a> 準備されていないトランザクションを自動ロールバックするためのサーバー側のタイムアウト設定を構成します。  

> [!WARNING]  
> このサーバー側のオプションは、Microsoft JDBC Driver 4.2 (以降) for SQL Server の新機能です。 このように動作を更新するには、サーバー上の sqljdbc_xa.dll が更新されていることを確認してください。 クライアント側のタイムアウトの設定について詳しくは、「[XAResource.setTransactionTimeout()](https://docs.oracle.com/javase/8/docs/api/javax/transaction/xa/XAResource.html)」をご覧ください。  

分散トランザクションのタイムアウトの動作を制御する 2 つのレジストリ設定 (DWORD 値) があります。  
  
- **Xadefaulttimeout**(秒単位): ユーザーがタイムアウトを指定しない場合に使用される既定のタイムアウト値。 既定値は 0 です。  
  
- **XAMaxTimeout**(秒単位): ユーザーが設定できるタイムアウトの最大値。 既定値は 0 です。  
  
これらの設定は SQL Server インスタンス固有で、次のレジストリ キーの下に作成する必要があります。  

```bash
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL<version>.<instance_name>\XATimeout  
```

> [!NOTE]  
> 64 ビットのコンピューターで実行されている 32 ビットの SQL Server の場合、レジストリ設定は次のキーの下に作成する必要があります: `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Microsoft SQL Server\MSSQL<version>.<instance_name>\XATimeout`
  
各トランザクションが開始されるとタイムアウト値が設定され、タイムアウトになるとトランザクションは SQL Server からロールバックされます。 タイムアウトは、これらのレジストリ設定と、ユーザーによる XAResource.setTransactionTimeout() での指定によって決定されます。 これらのタイムアウト値の解釈のいくつかの例を以下に示します。  
  
- `XADefaultTimeout = 0`, `XAMaxTimeout = 0`
  
     既定のタイムアウトは使用されず、クライアントにタイムアウトの最大値は適用されないことを意味します。 この場合、クライアントが XAResource.setTransactionTimeout を使用してタイムアウトを設定する場合にのみ、トランザクションにタイムアウトが適用されます。  
  
- `XADefaultTimeout = 60`, `XAMaxTimeout = 0`
  
     クライアントがタイムアウトを指定しない場合、すべてのトランザクションに 60 秒のタイムアウトが適用されることを意味します。 クライアントがタイムアウトを指定する場合、そのタイムアウト値が使用されます。 タイムアウトの最大値は適用されません。  
  
- `XADefaultTimeout = 30`, `XAMaxTimeout = 60`
  
     クライアントがタイムアウトを指定しない場合、すべてのトランザクションに 30 秒のタイムアウトが適用されることを意味します。 クライアントが何らかのタイムアウトを指定する場合、60 秒 (最大値) 以内であれば、クライアントのタイムアウトが使用されます。  
  
- `XADefaultTimeout = 0`, `XAMaxTimeout = 30`
  
     クライアントがタイムアウトを指定しない場合、すべてのトランザクションに 30 秒のタイムアウト (最大値) が適用されることを意味します。 クライアントが何らかのタイムアウトを指定する場合、30 秒 (最大値) 以内であれば、クライアントのタイムアウトが使用されます。  
  
### <a name="upgrading-sqljdbc_xadll"></a>sqljdbc_xa.dll のアップグレード

新しいバージョンの JDBC Driver をインストールする場合は、新しいバージョンに含まれる sqljdbc_xa.dll を使用して、サーバー上の sqljdbc_xa.dll もアップグレードする必要があります。  
  
> [!IMPORTANT]  
> sqljdbc_xa.dll のアップグレードは、メンテナンス ウィンドウ内で行うか、進行中の MS DTC トランザクションがないときに行ってください。
  
1. [!INCLUDE[tsql](../../includes/tsql-md.md)] **DBCC sqljdbc_xa (FREE)** コマンドを使用して sqljdbc_xa をアンロードします。  
  
2. JDBC Driver のインストール ディレクトリにある新しい sqljdbc_xa.dll を、分散トランザクションに参加するすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューターの Binn ディレクトリにコピーします。  
  
    sqljdbc_xa.dll 内の拡張プロシージャが呼び出されると、新しい DLL が読み込まれます。 新しい定義を読み込むために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動する必要はありません。  
  
### <a name="configuring-the-user-defined-roles"></a>ユーザー定義ロールを構成する

JDBC Driver を使用して分散トランザクションに参加する、特定のユーザーに対してアクセス許可を与えるには、そのユーザーを SqlJDBCXAUser ロールに追加します。 たとえば、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを使用して、'shelby' というユーザー ('shelby' という名前の付いた、SQL の標準的なログイン ユーザー) を SqlJDBCXAUser ロールに追加します。  

```sql
USE master  
GO  
EXEC sp_grantdbaccess 'shelby', 'shelby'  
GO  
EXEC sp_addrolemember [SqlJDBCXAUser], 'shelby'  
```

SQL ユーザー定義ロールは、データベースごとに定義されます。 セキュリティ上の目的で独自のロールを作成するには、各データベースでロールを定義し、データベースごとにユーザーを追加する必要があります。 SqlJDBCXAUser ロールは、マスターに存在する SQL JDBC 拡張ストアド プロシージャへのアクセス許可に使用されるため、master データベースで厳密に定義されています。 まず、個々のユーザーのマスターへのアクセスを許可し、次に、master データベースにログオンしてから、SqlJDBCXAUser ロールへのアクセスを許可する必要があります。  

## <a name="example"></a>例  

```java
import java.net.Inet4Address;
import java.sql.*;
import java.util.Random;
import javax.sql.XAConnection;
import javax.transaction.xa.*;
import com.microsoft.sqlserver.jdbc.*;


public class testXA {

    public static void main(String[] args) throws Exception {

        // Create variables for the connection string.
        String prefix = "jdbc:sqlserver://";
        String serverName = "localhost";
        int portNumber = 1433;
        String databaseName = "AdventureWorks";
        String user = "UserName";
        String password = "*****";

        String connectionUrl = prefix + serverName + ":" + portNumber + ";databaseName=" + databaseName + ";user="
                + user + ";password=" + password;

        Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement()) {
            stmt.executeUpdate("CREATE TABLE XAMin (f1 int, f2 varchar(max))");

        }
        // Create the XA data source and XA ready connection.
        SQLServerXADataSource ds = new SQLServerXADataSource();
        ds.setUser(user);
        ds.setPassword(password);
        ds.setServerName(serverName);
        ds.setPortNumber(portNumber);
        ds.setDatabaseName(databaseName);

        XAConnection xaCon = ds.getXAConnection();
        try (Connection con = xaCon.getConnection()) {

            // Get a unique Xid object for testing.
            XAResource xaRes = null;
            Xid xid = null;
            xid = XidImpl.getUniqueXid(1);

            // Get the XAResource object and set the timeout value.
            xaRes = xaCon.getXAResource();
            xaRes.setTransactionTimeout(0);

            // Perform the XA transaction.
            System.out.println("Write -> xid = " + xid.toString());
            xaRes.start(xid, XAResource.TMNOFLAGS);
            PreparedStatement pstmt = con.prepareStatement("INSERT INTO XAMin (f1,f2) VALUES (?, ?)");
            pstmt.setInt(1, 1);
            pstmt.setString(2, xid.toString());
            pstmt.executeUpdate();

            // Commit the transaction.
            xaRes.end(xid, XAResource.TMSUCCESS);
            xaRes.commit(xid, true);
        }
        xaCon.close();

        // Open a new connection and read back the record to verify that it worked.
        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT * FROM XAMin")) {
            rs.next();
            System.out.println("Read -> xid = " + rs.getString(2));
            stmt.executeUpdate("DROP TABLE XAMin");
        }
    }
}


class XidImpl implements Xid {

    public int formatId;
    public byte[] gtrid;
    public byte[] bqual;

    public byte[] getGlobalTransactionId() {
        return gtrid;
    }

    public byte[] getBranchQualifier() {
        return bqual;
    }

    public int getFormatId() {
        return formatId;
    }

    XidImpl(int formatId, byte[] gtrid, byte[] bqual) {
        this.formatId = formatId;
        this.gtrid = gtrid;
        this.bqual = bqual;
    }

    public String toString() {
        int hexVal;
        StringBuffer sb = new StringBuffer(512);
        sb.append("formatId=" + formatId);
        sb.append(" gtrid(" + gtrid.length + ")={0x");
        for (int i = 0; i < gtrid.length; i++) {
            hexVal = gtrid[i] & 0xFF;
            if (hexVal < 0x10)
                sb.append("0" + Integer.toHexString(gtrid[i] & 0xFF));
            else
                sb.append(Integer.toHexString(gtrid[i] & 0xFF));
        }
        sb.append("} bqual(" + bqual.length + ")={0x");
        for (int i = 0; i < bqual.length; i++) {
            hexVal = bqual[i] & 0xFF;
            if (hexVal < 0x10)
                sb.append("0" + Integer.toHexString(bqual[i] & 0xFF));
            else
                sb.append(Integer.toHexString(bqual[i] & 0xFF));
        }
        sb.append("}");
        return sb.toString();
    }

    // Returns a globally unique transaction id.
    static byte[] localIP = null;
    static int txnUniqueID = 0;

    static Xid getUniqueXid(int tid) {

        Random rnd = new Random(System.currentTimeMillis());
        txnUniqueID++;
        int txnUID = txnUniqueID;
        int tidID = tid;
        int randID = rnd.nextInt();
        byte[] gtrid = new byte[64];
        byte[] bqual = new byte[64];
        if (null == localIP) {
            try {
                localIP = Inet4Address.getLocalHost().getAddress();
            } catch (Exception ex) {
                localIP = new byte[] {0x01, 0x02, 0x03, 0x04};
            }
        }
        System.arraycopy(localIP, 0, gtrid, 0, 4);
        System.arraycopy(localIP, 0, bqual, 0, 4);

        // Bytes 4 -> 7 - unique transaction id.
        // Bytes 8 ->11 - thread id.
        // Bytes 12->15 - random number generated by using seed from current time in milliseconds.
        for (int i = 0; i <= 3; i++) {
            gtrid[i + 4] = (byte) (txnUID % 0x100);
            bqual[i + 4] = (byte) (txnUID % 0x100);
            txnUID >>= 8;
            gtrid[i + 8] = (byte) (tidID % 0x100);
            bqual[i + 8] = (byte) (tidID % 0x100);
            tidID >>= 8;
            gtrid[i + 12] = (byte) (randID % 0x100);
            bqual[i + 12] = (byte) (randID % 0x100);
            randID >>= 8;
        }
        return new XidImpl(0x1234, gtrid, bqual);
    }
}

```

## <a name="see-also"></a>参照  

[JDBC ドライバーを使用したトランザクションの実行](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
