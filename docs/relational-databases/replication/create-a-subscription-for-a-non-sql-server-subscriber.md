---
title: SQL 以外のサブスクライバーのサブスクリプションの作成
description: SQL Server Management Studio (SSMS) または Transact-SQL (T-SQL) を使用して、SQL Server で SQL Server 以外のサブスクライバーのサブスクリプションを作成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], non-SQL Server Subscribers
- Subscribers [SQL Server replication], non-SQL Server Subscribers
- non-SQL Server Subscribers, subscriptions
ms.assetid: 5020ee68-b988-4d57-8066-67d183e61237
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b64985281c98d15399e7cd561a05746e0634f057
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322019"
---
# <a name="create-a-subscription-for-a-non-sql-server-subscriber"></a>SQL Server 以外のサブスクライバーのサブスクリプションの作成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、SQL Server 以外のサブスクライバーのサブスクリプションを作成する方法について説明します。 トランザクション レプリケーションとスナップショット レプリケーションでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーに対するデータのパブリッシュがサポートされています。 サポートされるサブスクライバー プラットフォームの詳細については、「 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)を使用して、SQL Server 以外のサブスクライバーのサブスクリプションを作成する方法について説明します。  
  
 **このトピックの内容**  
  
-   **SQL Server 以外のサブスクライバーのサブスクリプションを作成するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーのサブスクリプションを作成するには、以下の操作を実行します。  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディストリビューターに、適切なクライアント ソフトウェアおよび OLE DB プロバイダーをインストールし、これらを構成します。 詳細については、「 [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md) 」および「 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)」を参照してください。  
  
2.  パブリケーションの新規作成ウィザードを使用して、パブリケーションを作成します。 Oracle データベースからパブリケーションを作成する方法については、「[Publisher で文書を作成するには](../../relational-databases/replication/publish/create-a-publication.md)」および「[Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)」(Oracle データベースからパブリケーションを作成する) を参照してください。 パブリケーションの新規作成ウィザードで、以下のオプションを指定します。  
  
    -   **[パブリケーションの種類]** ページで、 **[スナップショット パブリケーション]** または **[トランザクション パブリケーション]** を選択します。  
  
    -   **[スナップショット エージェント]** ページで、 **[スナップショットをすぐに作成する]** チェック ボックスをオフにします。  
  
         [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーに対してパブリケーションが有効になったら、スナップショットを作成し、スナップショット エージェントが[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーに適したスナップショットおよび初期化スクリプトを生成することを確認します。  
  
3.  **[パブリケーションのプロパティ - \<PublicationName>]** ダイアログ ボックスを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーのパブリケーションを有効にします。 この手順の詳細については、「 [Publication Properties, Subscription Options](../../relational-databases/replication/publication-properties-subscription-options.md) 」を参照してください。  
  
4.  サブスクリプションの新規作成ウィザードを使用して、サブスクリプションを作成します。 この手順の詳細については、このトピック内で説明します。  
  
5.  (省略可能) サブスクライバー側のテーブルを保持するには、 **pre_creation_cmd** アーティクル プロパティを変更します。 この手順の詳細については、このトピック内で説明します。  
  
6.  パブリケーションのスナップショットを生成します。 この手順の詳細については、このトピック内で説明します。  
  
7.  サブスクリプションを同期します。 詳細については、「 [プッシュ サブスクリプションの同期](../../relational-databases/replication/synchronize-a-push-subscription.md)」をご覧ください。  
  
#### <a name="to-enable-a-publication-for-non-sql-server-subscribers"></a>SQL Server 以外のサブスクライバーのパブリケーションを有効にするには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  パブリケーションを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[サブスクリプション オプション]** ページで、 **[SQL Server 以外のサブスクライバーを許可]** オプションに対して **[True]** の値を選択します。 このオプションを選択した場合、パブリケーションと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーとの互換性を確保するために、プロパティの数が変更されます。  
  
    > [!NOTE]  
    >  **[True]** を選択すると、 **pre_creation_cmd** アーティクル プロパティの値が 'drop' に設定されます。 この設定では、アーティクルのテーブル名と一致するテーブルがサブスクライバーにある場合、レプリケーションによってそのテーブルが削除されます。 サブスクライバーにある既存のテーブルを保持するには、アーティクルごとに [sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) ストアド プロシージャを使用し、次のように **pre_creation_cmd**の値に 'none' を指定します。 `sp_changearticle @publication= 'MyPublication', @article= 'MyArticle', @property='pre_creation_cmd', @value='none'`  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] パブリケーションの新しいスナップショットを作成するように要求されます。 この時点で作成しない場合は、次に示す作成手順を後で使用してください。  
  
#### <a name="to-create-a-subscription-for-a-non-sql-server-subscriber"></a>SQL Server 以外のサブスクライバーのサブスクリプションを作成するには  
  
1.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
2.  適切なパブリケーションを右クリックして、 **[新しいサブスクリプション]** をクリックします。  
  
3.  **[ディストリビューション エージェントの場所]** ページで、 **[ディストリビューター &lt;Distributor&gt; ですべてのエージェントを実行する]** が選択されていることを確認します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーは、サブスクライバーでのエージェントの実行をサポートしていません。  
  
4.  **[サブスクライバー]** ページで、 **[サブスクライバーの追加]** をクリックし、次に **[SQL Server 以外のサブスクライバーの追加]** をクリックします。  
  
5.  **[SQL Server 以外のサブスクライバーの追加]** ダイアログ ボックスで、サブスクライバーの種類を選択します。  
  
6.  **[データ ソース名]** に値を入力します。  
  
    -   Oracle の場合、これは構成した Transparent Network Substrate (TNS) 名です。  
  
    -   IBM の場合は、任意の名前にすることができます。 通常は、サブスクライバーのネットワーク アドレスを指定します。  
  
     この手順で入力したデータ ソース名と手順 9. で指定した資格情報は、このウィザードでは検証されません。 これらは、サブスクリプションに対してディストリビューション エージェントが実行されるまで、レプリケーションで使用されません。 クライアント ツール (Oracle の場合には **sqlplus** など) を使用してサブスクライバーに接続することにより、すべての値がテストされていることを確認します。 詳細については、「 [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md) 」および「 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)」を参照してください。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] これで、ウィザードの **[サブスクライバー]** ページで、サブスクライバーが **[サブスクライバー]** 列に表示され、読み取り専用の **[(既定の転送先)]** が **[サブスクリプション データベース]** 列に表示されます。  
  
    -   Oracle の場合、1 つのサーバーに 1 つのデータベースしか作成できないため、データベースを指定する必要はありません。  
  
    -   IBM DB2 の場合、データベースは DB2 接続文字列の **Initial Catalog** プロパティで指定されます。DB2 接続文字列は、後述する **[追加の接続オプション]** フィールドに入力できます。  
  
8.  **[ディストリビューション エージェント セキュリティ]** ページで、サブスクライバーの横のプロパティ ボタン ( **[...]** ) をクリックし、 **[ディストリビューション エージェント セキュリティ]** ダイアログ ボックスにアクセスします。  
  
9. **[ディストリビューション エージェント セキュリティ]** ダイアログ ボックスで、以下の操作を行います。  
  
    -   **[プロセス アカウント]** 、 **[パスワード]** 、および **[パスワードの確認入力]** フィールドで、ディストリビューション エージェントの実行、およびディストリビューターへのローカル接続に使用される [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントおよびパスワードを入力します。  
  
         アカウントには、ディストリビューション データベースの固定データベース ロール **db_owner** のメンバーであること、パブリケーション アクセス リスト (PAL) のメンバーであること、スナップショット共有での読み取り権限、および OLE DB プロバイダーのインストール ディレクトリでの読み取り権限など、最小限の権限が必要です。 PAL の詳細については、「[Secure the Publisher (パブリッシャーのセキュリティ保護)](../../relational-databases/replication/security/secure-the-publisher.md)」を参照してください。  
  
    -   **[サブスクライバーに接続]** の、 **[ログイン]** 、 **[パスワード]** 、および **[パスワードの確認入力]** フィールドで、サブスクライバーへの接続に使用するログインとパスワードを入力します。 このログインは、あらかじめ構成され、サブスクリプション データベースでオブジェクトを作成できる十分な権限を持っている必要があります。  
  
    -   **[追加の接続オプション]** フィールドで、接続文字列の形式でサブスクライバーの接続オプションを指定します (Oracle では追加オプションは必要ありません)。 各オプションはセミコロンで区切る必要があります。 以下に、DB2 接続文字列の例を示します (読みやすいように改行しています)。  
  
        ```  
        Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
        PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
        Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
        Persist Security Info=False;Connection Pooling=True;  
        ```  
  
         文字列内のオプションの多くは、接続する DB2 サーバーに固有のものですが、 **Process Binary as Character** オプションは常に **False**に設定する必要があります。 サブスクリプション データベースを識別するため、 **Initial Catalog** オプションに値が必要です。  
  
10. **[同期スケジュール]** ページで、 **[エージェント スケジュール]** メニューからディストリビューション エージェントのスケジュールを選択します (スケジュールは通常、 **[連続実行する]** です)。  
  
11. **[サブスクリプションの初期化]** ページで、サブスクリプションを初期化するかどうか、および初期化する場合はいつ行うのかを指定します。  
  
    -   すべてのオブジェクトを作成し、サブスクリプション データベースに必要なすべてのデータを追加した場合にのみ、 **[初期化]** チェック ボックスをオフにします。  
  
    -   このウィザードが完了した後に、ディストリビューション エージェントからサブスクライバーへスナップショット ファイルを転送するには、 **[次の場合に初期化]** 列のドロップダウン リスト ボックスから **[今すぐ]** を選択します。 エージェントの次回の実行時にファイルが転送されるようにするには、 **[初回同期時]** を選択します。  
  
12. **[ウィザードのアクション]** ページで、必要に応じてサブスクリプションのスクリプトを作成します。 詳細については、「[レプリケーションのスクリプト作成](../../relational-databases/replication/scripting-replication.md)」を参照してください。  
  
#### <a name="to-retain-tables-at-the-subscriber"></a>サブスクライバー側のテーブルを保持するには  
  
-   既定では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーに対してパブリケーションを有効にすると、 **pre_creation_cmd** アーティクル プロパティが 'drop' に設定されます。 この設定では、アーティクルのテーブル名と一致するテーブルがサブスクライバーにある場合、レプリケーションによってそのテーブルが削除されます。 サブスクライバーにある既存のテーブルを保持するには、アーティクルごとに [sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) ストアド プロシージャを使用し、次のように **pre_creation_cmd**の値に 'none' を指定します。 [https://login.microsoftonline.com/consumers/](`sp_changearticle @publication= 'MyPublication', @article= 'MyArticle', @property='pre_creation_cmd', @value='none'`)  
  
#### <a name="to-generate-a-snapshot-for-the-publication"></a>パブリケーションのスナップショットを生成するには  
  
1.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
2.  パブリケーションを右クリックし、 **[スナップショット エージェントの状態の表示]** をクリックします。  
  
3.  **[スナップショット エージェントの状態の表示 - \<Publication>]** ダイアログ ボックスで **[開始]** をクリックします。  
  
 スナップショット エージェントによるスナップショットの生成が完了すると、"[100%] 17 個のアーティクルのスナップショットが生成されました。" などのメッセージが表示されます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 レプリケーション ストアド プロシージャを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーに対するプッシュ サブスクリプションをプログラムから作成できます。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
#### <a name="to-create-a-push-subscription-for-a-transactional-or-snapshot-publication-to-a-non-sql-server-subscriber"></a>SQL Server 以外のサブスクライバーに対する、トランザクション パブリケーションまたはスナップショット パブリケーションのプッシュ サブスクリプションを作成するには  
  
1.  パブリッシャーとディストリビューターの両方に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーの最新の OLE DB プロバイダーをインストールします。 OLE DB プロバイダーのレプリケーションの要件については、「 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)」、 [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md)」、「 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)」を参照してください。  
  
2.  パブリッシャー側のパブリケーション データベースに対して、[sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) を実行して、パブリケーションが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバ―をサポートしていることを確認します。  
  
    -   **enabled_for_het_sub** の値が 1 の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーがサポートされます。  
  
    -   **enabled_for_het_sub** の値が 0 の場合、`@property` に **enabled_for_het_sub** を指定し、`@value` に **true** を指定して、[sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) を実行します。  
  
        > [!NOTE]  
        >  **enabled_for_het_sub** を **true**に変更する前に、そのパブリケーションに対する既存のサブスクリプションをすべて削除する必要があります。 パブリケーションで更新サブスクリプションもサポートされる場合、 **enabled_for_het_sub** を **true** に設定することはできません。 **enabled_for_het_sub** を変更すると、他のパブリケーション プロパティにも影響します。 詳細については、「 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)」を参照してください。  
  
3.  パブリッシャー側のパブリケーション データベースに対して、[sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) を実行します。 `@publication`、`@subscriber`、`@destination_db` に対して値 `(default destination)`、`@subscription_type` に対して値 **push**、`@subscriber_type` に対して値 3 (OLE DB プロバイダーを指定) を指定します。  
  
4.  パブリッシャー側のパブリケーション データベースに対して、[sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) を実行します。 次の指定を行います。  
  
    -   `@subscriber` および `@publication` パラメーター。  
  
    -   `@subscriber_db` に対して **(既定の転送先)** の値。  
  
    -   `@subscriber_provider`、`@subscriber_datasrc`、`@subscriber_location`、`@subscriber_provider_string`、`@subscriber_catalog` に対して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のデータ ソースのプロパティ。  
  
    -   `@job_login` および `@job_password` に対して、ディストリビューターでのディストリビューション エージェントの実行に使用される [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 資格情報。  
  
       > [!NOTE]  
       > Windows 統合認証を使用して行われる接続では、常に `@job_login` および `@job_password` で指定した Windows 資格情報が使用されます。 ディストリビューション エージェントは、常に Windows 統合認証を使用してディストリビューターにローカル接続します。 既定では、エージェントは Windows 統合認証を使用してサブスクライバーに接続します。  
  
    -   `@subscriber_security_mode` に対して値 **0**、`@subscriber_login` および `@subscriber_password` に対して OLE DB プロバイダーのログイン情報。  
  
    -   このサブスクリプションでのディストリビューション エージェント ジョブのスケジュール。 詳細については、「 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)」を参照してください。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャー側でプッシュ サブスクリプションを作成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md)   
 [その他の SQL Server 以外のサブスクライバー](../../relational-databases/replication/non-sql/other-non-sql-server-subscribers.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [レプリケーション セキュリティの推奨事項](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
