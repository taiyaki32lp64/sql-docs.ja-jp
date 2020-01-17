---
title: リンク サーバーの作成 (SQL Server データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.linkedserver.properties.general.f1
- sql12.swb.linkedserver.properties.security.f1
- sql12.swb.linkedserver.properties.provider.f1
- sql12.swb.linkedserver.properties.options.f1
helpviewer_keywords:
- linked servers [SQL Server], creating
ms.assetid: 3228065d-de8f-4ece-a9b1-e06d3dca9310
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a288f5c9f42e282694b864e4493d02dcd6cfa3a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62743499"
---
# <a name="create-linked-servers-sql-server-database-engine"></a>リンク サーバーの作成 (SQL Server データベース エンジン)
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してリンク サーバーを作成し、別の [!INCLUDE[tsql](../../includes/tsql-md.md)]からデータにアクセスする方法について説明します。 リンク サーバーを作成すると、複数のソースのデータを操作できます。 リンク サーバーは別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスである必要はありませんが、そのようにするのが一般的です。  
  
##  <a name="Background"></a> 背景情報  
 リンク サーバーを使用すると、OLE DB データ ソースに対する異種の分散クエリの利用が可能になります。 リンク サーバーを作成すると、このサーバーに対して分散クエリを実行でき、クエリを使用して複数のデータ ソースのテーブルを結合できます。 リンク サーバーを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスとして定義した場合は、リモート ストアド プロシージャを実行できます。  
  
 リンク サーバーの機能と必須の引数は大きく異なることがあります。 このトピックでは、一般的な例を紹介しますが、すべてのオプションについて説明しているわけではありません。 詳細については、「 [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)からデータにアクセスする方法について説明します。  
  
##  <a name="Security"></a> セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 使用する場合[!INCLUDE[tsql](../../includes/tsql-md.md)]、ステートメントが必要です`ALTER ANY LINKED SERVER`メンバーシップまたはサーバーに対する権限、 **setupadmin**固定サーバー ロール。 使用する場合[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]必要`CONTROL SERVER`権限またはメンバーシップ、 **sysadmin**固定サーバー ロール。  
  
##  <a name="Procedures"></a> リンク サーバーを作成する方法  
 次のいずれかを使用できます。  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-sql-server-management-studio"></a>SQL Server Management Studio を使用して別の SQL Server インスタンスへのリンク サーバーを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、オブジェクト エクスプローラーを開きます。次に、 **[サーバー オブジェクト]** を展開し、 **[リンク サーバー]** を右クリックして、 **[新しいリンク サーバー]** をクリックします。  
  
2.  **[全般]** ページの **[リンク サーバー]** ボックスに、リンク先の **SQL Server** インスタンスの名前を入力します。  
  
     **SQL Server**  
     リンク サーバーを [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに指定します。 この方法で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リンク サーバーを定義する場合、 **[リンク サーバー]** にはサーバーのネットワーク名を指定する必要があります。 さらに、サーバーから取得されるテーブルは、リンク サーバーのログイン用に定義されている既定のデータベースから取得されます。  
  
     **[その他のデータ ソース]**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外の OLE DB サーバーの種類を指定します。 このオプションをクリックすると、その下にあるオプションを指定できるようになります。  
  
     **プロバイダー**  
     リスト ボックスから OLE DB データ ソースを選択します。 OLE DB プロバイダーは、特定の PROGID を使用してレジストリに登録されます。  
  
     **[製品名]**  
     リンク サーバーとして追加する OLE DB データ ソースの製品名を入力します。  
  
     **データ ソース**  
     OLE DB プロバイダーで解釈されるデータ ソースの名前を入力します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続する場合は、インスタンス名を入力します。  
  
     **[プロバイダー文字列]**  
     データ ソースに対応する OLE DB プロバイダーの一意なプログラム識別子 (PROGID) を入力します。 有効なプロバイダー文字列の例については、「 [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)からデータにアクセスする方法について説明します。  
  
     **場所**  
     OLE DB プロバイダーで解釈されるデータベースの場所を入力します。  
  
     **Catalog**  
     OLE DB プロバイダーへの接続を作成するときに使用するカタログの名前を入力します。  
  
     リンク サーバーに接続できるかどうかをテストするには、オブジェクト エクスプローラーでリンク サーバーを右クリックし、 **[接続テスト]** をクリックします。  
  
    > [!NOTE]  
    >  **SQL Server** インスタンスが既定のインスタンスの場合は、 **SQL Server**インスタンスをホストするコンピューターの名前を入力します。 **SQL Server** が名前付きインスタンスの場合は、コンピューターの名前とインスタンスの名前を入力します (例: **Accounting\SQLExpress**)。  
  
3.  **[サーバーの種類]** 領域で **[SQL Server]** をクリックし、リンク サーバーが別の **SQL Server** インスタンスであることを指定します。  
  
4.  **[セキュリティ]** ページで、元の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がリンク サーバーに接続するときに使用するセキュリティ コンテキストを指定します。 ユーザーがドメイン ログインを使用して接続するドメイン環境では、 **[ログインの現在のセキュリティ コンテキストを使用する]** を選択することが最適な場合が多くあります。 ユーザーが **SQL Server** ログインを使用して元の **SQL Server** に接続する場合は、 **[このセキュリティ コンテキストを使用する]** をクリックして、リンク サーバーでの認証に必要な資格情報を指定することが最適です。  
  
     **[ローカル ログイン]**  
     リンク サーバーに接続できるローカル ログインを指定します。 ローカル ログインは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証ログインまたは Windows 認証ログインのいずれかを使用するログインにすることができます。 この一覧を使用して、特定のログインへの接続を制限することも、一部のログインが別のログインとして接続できるように設定することもできます。  
  
     **Impersonate**  
     ローカル ログインからリンク サーバーにユーザー名とパスワードを渡します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証の場合、まったく同じ名前とパスワードを持つログインがリモート サーバーに存在する必要があります。 Windows ログインの場合、ログインがリンク サーバー上で有効である必要があります。  
  
     権限借用を使用するには、委任の要件を満たすように構成する必要があります。  
  
     **[リモート ユーザー]**  
     リモート ユーザーを使用して、 **[ローカル ログイン]** で定義されないユーザーをマップします。 **リモート ユーザー** は、リモート サーバーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証ログインである必要があります。  
  
     **[リモート パスワード]**  
     リモート ユーザーのパスワードを指定します。  
  
     **[追加]**  
     新しいローカル ログインを追加します。  
  
     **[削除]**  
     既存のローカル ログインを削除します。  
  
     **[接続を許可しない]**  
     一覧で定義されていないログインについて、接続を許可しないように指定します。  
  
     **[セキュリティ コンテキストを使用しない]**  
     一覧で定義されていないログインについて、セキュリティ コンテキストを使用せずに接続を作成するように指定します。  
  
     **[ログインの現在のセキュリティ コンテキストを使用する]**  
     一覧で定義されていないログインについて、ログインの現在のセキュリティ コンテキストを使用して接続を作成するように指定します。 Windows 認証を使用してローカル サーバーに接続する場合は、リモート サーバーへの接続に Windows 資格情報を使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用してローカル サーバーに接続する場合は、リモート サーバーへの接続にログイン名とパスワードを使用します。 この場合、まったく同じ名前とパスワードを持つログインがリモート サーバーに存在する必要があります。  
  
     **[このセキュリティ コンテキストを使用する]**  
     一覧で定義されていないログインについて、 **[リモート ログイン]** ボックスおよび **[パスワード]** ボックスで指定したログインとパスワードを使用して接続を作成するように指定します。 リモート ログインは、リモート サーバーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証ログインである必要があります。  
  
5.  必要に応じてサーバー オプションを表示または指定する場合は、 **[サーバー オプション]**  ページをクリックします。  
  
     **[照合順序互換]**  
     リンク サーバーに対する分散クエリの実行に影響を与えます。 このオプションを true に設定した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、文字セットと照合順序 (並べ替え順) に関して、リンク サーバー内のすべての文字がローカル サーバーと互換性があると見なします。 これにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からプロバイダーに文字を含む列の比較を送信できるようになります。 このオプションが設定されていない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では文字列を含む列の比較の評価は常にローカルで行われます。  
  
     このオプションは、リンク サーバーに対応するデータ ソースがローカル サーバーと同じ文字セットと並べ替え順を持っていることが確認できている場合のみ設定します。  
  
     **[データ アクセス]**  
     分散クエリ アクセスに対してリンク サーバーを有効または無効にします。  
  
     **RPC**  
     指定されたサーバーからの RPC を有効にします。  
  
     **[RPC 出力]**  
     指定されたサーバーへの RPC を有効にします。  
  
     **[リモート照合順序を使用]**  
     リモート列とローカル サーバーのどちらの照合順序を使用するかを指定します。  
  
     true の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ソースに対してはリモート列の照合順序を使用し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のデータ ソースに対しては [照合順序名] で指定した照合順序を使用します。  
  
     false の場合、分散クエリは常にローカル サーバーの既定の照合順序を使用します。[照合順序名] とリモート列の照合順序は無視されます。 既定値は false です。  
  
     **[照合順序名]**  
     [リモート照合順序を使用] が true、かつ、データ ソースが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ソースでない場合に、リモート データ ソースが使用する照合順序の名前を指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]がサポートしている照合順序名のいずれかを指定する必要があります。  
  
     このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外の OLE DB データ ソースにアクセスし、その照合順序が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序のいずれかと一致する場合に使用します。  
  
     リンク サーバーは、そのサーバー内のすべての列で使用される単一の照合順序をサポートしている必要があります。 リンク サーバーが、単一のデータ ソース内で複数の照合順序をサポートしている、またはリンク サーバーの照合順序が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序のいずれかと一致するかどうかが判断できない場合は、このオプションを設定しないでください。  
  
     **[接続タイムアウト]**  
     リンク サーバーに接続する場合のタイムアウト値です (秒単位)。  
  
     0 の場合は、 **sp_configure** の [remote login timeout](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md) オプションの既定値が使用されます。  
  
     **[クエリ タイムアウト]**  
     リンク サーバーに対するクエリのタイムアウト値です (秒単位)。  
  
     0 の場合は、 **sp_configure** の [remote query timeout](../../database-engine/configure-windows/configure-the-remote-query-timeout-server-configuration-option.md) オプションの既定値が使用されます。  
  
     **[分散トランザクションのプロモーションを有効化]**  
     このオプションを使用して、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 分散トランザクション コーディネーター (MS DTC) トランザクションにより、サーバー間のプロシージャのアクションを保護します。 このオプションが TRUE の場合、リモート ストアド プロシージャを呼び出すと分散トランザクションが開始され、トランザクションは MS DTC に参加します。 詳細については、「 [sp_serveroption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-serveroption-transact-sql)からデータにアクセスする方法について説明します。  
  
6.  クリックして **OK**です。  
  
##### <a name="to-view-the-provider-options"></a>プロバイダー オプションを表示するには  
  
-   プロバイダーを使用可能にするオプションを表示するには、 **プロバイダー オプション** ページを使用します。  
  
     すべてのプロバイダーで同じオプションを使用できるとは限りません。 たとえば、インデックスを利用できるデータ型と利用できないデータ型があります。 このダイアログ ボックスを使用することで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がプロバイダーの機能を認識できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は一般的なデータ プロバイダーをインストールしますが、データを提供する製品が変わると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でインストールされたプロバイダーが最新機能をすべてサポートしているとは限りません。 データを提供する製品の機能の詳細については、その製品のマニュアルを参照してください。  
  
     **[動的パラメーター]**  
     プロバイダーが、パラメーター化クエリに "?" パラメーター マーカー構文を使用できることを示します。 このオプションは、プロバイダーが **ICommandWithParameters** インターフェイスをサポートしており、パラメーター化マーカーとして "?" をサポートしている場合にのみ設定してください。 このオプションを設定すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はプロバイダーに対してパラメーター化クエリを実行できます。 プロバイダーに対してパラメーター化クエリを実行できることにより、特定のクエリではパフォーマンスが向上します。  
  
     **[入れ子になったクエリ]**  
     プロバイダーが、入れ子になった  `SELECT` ステートメントを FROM 句内で使用できることを示します。 このオプションを設定すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は SELECT ステートメントを FROM 句の中で入れ子にする必要のある特定のクエリをプロバイダーに委任できます。  
  
     **[レベル 0 のみ]**  
     プロバイダーに対して起動できるのはレベル 0 の OLE DB インターフェイスだけです。  
  
     **[InProcess 許可]**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、インプロセス サーバーとしてプロバイダーのインスタンスを作成できます。 このオプションを設定しない場合、既定の動作として、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス外でプロバイダーのインスタンスが作成されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のプロセス外でプロバイダーのインスタンスが作成されると、プロバイダーでエラーが発生しても、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスは影響を受けません。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のプロセス外でインスタンスが作成されたプロバイダーでは、長い列 (`text`、`ntext`、または `image`) を参照する更新や挿入はできません。  
  
     **[トランザクション更新以外]**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、 **ITransactionLocal** を利用できない場合でも更新を実行できます。 このオプションがオンの場合、プロバイダーはトランザクションをサポートしないので、プロバイダーに対する更新を回復することはできません。  
  
     **[アクセス パスとしてのインデックス]**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はプロバイダーのインデックスを使用してデータをフェッチしようとします。 既定では、インデックスはメタデータにのみ使用され、開かれることはありません。  
  
     **[アドホック アクセス禁止]**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、OLE DB プロバイダーに対して OPENROWSET 関数と OPENDATASOURCE 関数を使用したアドホック アクセスは許可されません。 このオプションを設定しない場合も、アドホック アクセスは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により禁止されます。  
  
     **['Like' 演算子をサポートします]**  
     プロバイダーが LIKE キーワードを使用したクエリをサポートしていることを示します。  
  
###  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用してリンク サーバーを作成するには、[sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql) ステートメント、[CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql) ステートメント、および [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql) ステートメントを使用します。  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-transact-sql"></a>Transact-SQL を使用して別の SQL Server インスタンスへのリンク サーバーを作成するには  
  
1.  クエリ エディターで、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを入力して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] という名前の `SRVR002\ACCTG`インスタンスにリンクします。  
  
    ```sql  
    USE [master]  
    GO  
    EXEC master.dbo.sp_addlinkedserver   
        @server = N'SRVR002\ACCTG',   
        @srvproduct=N'SQL Server' ;  
    GO  
  
    ```  
  
2.  次のコードを実行して、リンク サーバーを使用しているログインのドメイン資格情報を使用するようにリンク サーバーを構成します。  
  
    ```sql  
    EXEC master.dbo.sp_addlinkedsrvlogin   
        @rmtsrvname = N'SRVR002\ACCTG',   
        @locallogin = NULL ,   
        @useself = N'True' ;  
    GO  
  
    ```  
  
##  <a name="FollowUp"></a>補足情報: リンク サーバーの作成後に行う手順  
  
#### <a name="to-test-the-linked-server"></a>リンク サーバーをテストするには  
  
-   次のコードを実行して、リンク サーバーへの接続をテストします。 この例は、リンク サーバーにあるデータベースの名前を返します。  
  
    ```sql  
    SELECT name FROM [SRVR002\ACCTG].master.sys.databases ;  
    GO  
  
    ```  
  
#### <a name="writing-a-query-that-joins-tables-from-a-linked-server"></a>リンク サーバーのテーブルを結合するクエリの記述  
  
-   4 つの要素で構成される名前を使用して、リンク サーバー上のオブジェクトを参照します。 次のコードを実行して、ローカル サーバー上のすべてのログインとリンク サーバー上の対応するログインの一覧を取得します。  
  
    ```sql  
    SELECT local.name AS LocalLogins, linked.name AS LinkedLogins  
    FROM master.sys.server_principals AS local  
    LEFT JOIN [SRVR002\ACCTG].master.sys.server_principals AS linked  
        ON local.name = linked.name ;  
    GO  
    ```  
  
     リンク サーバー ログインに対して NULL が返される場合は、リンク サーバー上にログインが存在しないことを示します。 リンク サーバーが別のセキュリティ コンテキストを渡すように構成されている場合、またはリンク サーバーが匿名接続を許可する場合を除き、これらのログインではリンク サーバーを使用できません。  
  
## <a name="see-also"></a>関連項目  
 [リンク サーバー &#40;データベース エンジン&#41;](linked-servers-database-engine.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)   
 [sp_serveroption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-serveroption-transact-sql)  
  
  
