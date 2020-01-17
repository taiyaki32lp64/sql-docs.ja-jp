---
title: FTP でのスナップショットの配信 | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], FTP snapshots
- FTP snapshots [SQL Server replication]
- snapshot replication [SQL Server], FTP
ms.assetid: 99872c4f-40ce-4405-8fd4-44052d3bd827
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c6ec9ac5c4e868a9022a11cc153c9638cab737dc
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710994"
---
# <a name="deliver-a-snapshot-through-ftp"></a>FTP でのスナップショットの配信
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、FTP でスナップショットを配信する方法について説明します。  

既定では、スナップショットは、UNC (Universal Naming Convention) 共有として定義されたフォルダーに格納されます。 レプリケーションでは、UNC 共有ではなく、FTP (File Transfer Protocol) 共有を指定することもできます。 FTP を使用するには、FTP サーバーを構成してから、FTP を使用するためのパブリケーションと 1 つ以上のサブスクリプションを構成する必要があります。 FTP サーバーの構成方法の詳細については、インターネット インフォメーション サービス (IIS) のドキュメントを参照してください。 パブリケーションに対して FTP 情報を指定すると、そのパブリケーションに対するサブスクリプションでは、既定で FTP を使用します。 IIS が動作しているコンピューターがファイアウォールによってディストリビューターから分離されている場合、FTP は Web 同期との組み合わせでのみ使用されます。 この場合、FTP を使用してディストリビューター、および IIS を実行中のコンピューターからスナップショットを転送できます (スナップショットは常に HTTPS を使用してサブスクライバーに転送されます)。  
  
> [!IMPORTANT]  
>  FTP 共有では、FTP パスワードを格納する必要があり、このパスワードがプレーン テキストでサブスクライバー (Web 同期が使用されている場合は、IIS が動作しているコンピューター) から FTP サーバーに送信されるため、FTP 共有ではなく Microsoft Windows 認証と UNC 共有を使用することをお勧めします。 また、1 つのアカウントがスナップショット共有へのアクセスを制御するため、フィルター選択されたマージ パブリケーションへのサブスクライバーだけに、スナップショット ファイルのデータ パーティションからスナップショット ファイルへのアクセス権が与えられていることを確認することはできません。  
  

## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
  
-   スナップショット エージェントには、指定したディレクトリに対する書き込み権限が必要です。また、ディストリビューション エージェントまたはマージ エージェントには、読み取り権限が必要です。 プル サブスクリプションを使用する場合は、共有ディレクトリを UNC (汎用名前付け規則) パス (\\\ftpserver\home\snapshots など) として指定する必要があります。 詳細については、「[Secure the Snapshot Folder](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)」(スナップショット フォルダーのセキュリティ保護) をご覧ください。  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   ファイル転送プロトコル (FTP) を使用してスナップショット ファイルを転送するには、まず、FTP サーバーを構成する必要があります。 詳細については、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] インターネット インフォメーション サービス (IIS) のマニュアルを参照してください。  
  
###  <a name="Security"></a> セキュリティ  
 セキュリティを強化するため、インターネット経由の FTP スナップショット配信を使用する際には仮想プライベート ネットワーク (VPN) を実装することをお勧めします。 詳細については、「[Publish Data over the Internet Using VPN](../../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md)」(VPN を使用したインターネット経由のデータのパブリッシュ) をご覧ください。  
  
 セキュリティの推奨方法としては、FTP サーバーに対する匿名ログインを許可しないことをお勧めします。 スナップショット エージェントには、指定したディレクトリに対する書き込み権限が必要です。また、ディストリビューション エージェントまたはマージ エージェントには、読み取り権限が必要です。 プル サブスクリプションを使用する場合は、共有ディレクトリを UNC (汎用名前付け規則) パス (\\\ftpserver\home\snapshots など) として指定する必要があります。 詳細については、「[Secure the Snapshot Folder](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)」(スナップショット フォルダーのセキュリティ保護) をご覧ください。  
  
 可能であれば、実行時に資格情報の入力を求めるメッセージを表示します。 資格情報をスクリプト ファイルに保存する場合、ファイルをセキュリティ保護する必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 FTP サーバーの構成が完了したら、 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで、そのサーバーのディレクトリとセキュリティの情報を指定します。 このダイアログ ボックスへのアクセス方法の詳細については、「[パブリケーション プロパティの表示および変更](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」を参照してください。  
  
#### <a name="to-specify-ftp-information"></a>FTP 情報を指定するには  
  
1.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの次のいずれかのページで、 **[ファイル転送プロトコル (FTP) を使用したスナップショット ファイルのダウンロードをサブスクライバーに許可する]** を選択します。  
  
    -   **[FTP スナップショット]** ページ。スナップショット パブリケーション、トランザクション パブリケーション、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] より前のバージョンを実行しているパブリッシャーのマージ パブリケーションの場合。  
  
    -   **[FTP スナップショットとインターネット]** ページ。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降を実行しているパブリッシャーからのマージ パブリケーションの場合。  
  
2.  **[FTP サーバー名]** 、 **[ポート番号]** 、 **[FTP ルート フォルダーからのパス]** 、 **[ログイン]** 、および **[パスワード]** の値を指定します。  
  
     たとえば、FTP サーバーのルートが \\\ftpserver\home で、スナップショットを \\\ftpserver\home\snapshots に格納する場合は、 **[FTP ルート フォルダーからのパス]** には「\snapshots\ftp」と指定します (レプリケーションでは、スナップショット ファイルが作成されるときにスナップショット フォルダーのパスに "ftp" が追加されます)。  
  
3.  スナップショット エージェントが、手順 2. で指定したディレクトリにスナップショット ファイルを書き込むように指定します。 たとえば、スナップショット エージェントがスナップショット ファイルを \\\ftpserver\home\snapshots\ftp に書き込むようにするには、次のいずれかの場所に \\\ftpserver\home\snapshots というパスを指定する必要があります。  
  
    -   このパブリケーションに関連付けられているディストリビューターの既定のスナップショットの場所。    
    -   このパブリケーションの代替スナップショット フォルダーの場所。 スナップショットが圧縮されている場合、別の場所が必要です。  

スナップショット フォルダーの場所のプロパティ変更の詳細については、[スナップショットのオプション](../snapshot-options.md)に関する記事を参照してください。
  

4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 FTP サーバーでスナップショット ファイルを使用するためのオプションを設定できます。この FTP 設定は、レプリケーション ストアド プロシージャを使用してプログラムから変更できます。 使用されるプロシージャは、パブリケーションの種類によって異なります。 FTP によるスナップショット配信は、プル サブスクリプションでのみ使用できます。  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションで FTP スナップショット配信を有効にするには  
  
1.  パブリッシャーのパブリケーション データベースに対して、 [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)を実行します。 `@publication` を指定し、`@enabled_for_internet` に **true** を指定します。次のパラメーターに適切な値を指定します。  
  
    -   `@ftp_address` - スナップショットの配信に使用する FTP サーバーのアドレス。  
  
    -   (省略可) `@ftp_port` - FTP サーバーで使用されるポート。  
  
    -   (省略可) `@ftp_subdirectory` - FTP ログインに割り当てられる既定の FTP ディレクトリのサブディレクトリ。 たとえば、FTP サーバーのルートが \\\ftpserver\home のときに、スナップショットを \\\ftpserver\home\snapshots に保存するには、`@ftp_subdirectory` に **\snapshots\ftp** と指定します (スナップショット ファイルが作成されるときに、スナップショット フォルダーのパスに "ftp" が付加されます)。  
  
    -   (省略可) `@ftp_login` - FTP サーバーに接続するときに使用されるログイン アカウント。  
  
    -   (省略可) `@ftp_password` - FTP ログイン用のパスワード。  
  
     これにより、FTP を使用するパブリケーションが作成されます。 詳細については、「 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)」を参照してください。  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-merge-publication"></a>マージ パブリケーションで FTP スナップショット配信を有効にするには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)を実行します。 `@publication` を指定し、`@enabled_for_internet` に **true** を指定します。次のパラメーターに適切な値を指定します。  
  
    -   `@ftp_address` - スナップショットの配信に使用する FTP サーバーのアドレス。  
  
    -   (省略可) `@ftp_port` - FTP サーバーで使用されるポート。  
  
    -   (省略可) `@ftp_subdirectory` - FTP ログインに割り当てられる既定の FTP ディレクトリのサブディレクトリ。 たとえば、FTP サーバーのルートが \\\ftpserver\home のときに、スナップショットを \\\ftpserver\home\snapshots に保存するには、`@ftp_subdirectory` に **\snapshots\ftp** と指定します (スナップショット ファイルが作成されるときに、スナップショット フォルダーのパスに "ftp" が付加されます)。  
  
    -   (省略可) `@ftp_login` - FTP サーバーに接続するときに使用されるログイン アカウント。  
  
    -   (省略可) `@ftp_password` - FTP ログイン用のパスワード。  
  
     これにより、FTP を使用するパブリケーションが作成されます。 詳細については、「 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)」を参照してください。  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication-that-uses-ftp-snapshot-delivery"></a>FTP スナップショット配信を使用するスナップショット パブリケーションまたはトランザクション パブリケーションへのプル サブスクリプションを作成するには  
  
1.  サブスクライバー側のサブスクリプション データベースに対して、 [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)を実行します。 `@publisher` および `@publication` を指定します。  
  
    -   サブスクライバー側のサブスクリプション データベースに対して、 [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)を実行します。 `@publisher`、`@publisher_db`、`@publication` を指定し、`@job_login` および `@job_password` にサブスクライバーでディストリビューション エージェントを実行するときの [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 資格情報を指定し、`@use_ftp` に **true** を指定します。  
  
2.  パブリッシャー側のパブリケーション データベースに対して [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) を実行し、プル サブスクリプションを登録します。 詳細については、「 [プル サブスクリプションの作成](../../../relational-databases/replication/create-a-pull-subscription.md)」をご覧ください。  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication-that-uses-ftp-snapshot-delivery"></a>FTP スナップショット配信を使用するマージ パブリケーションへのプル サブスクリプションを作成するには  
  
1.  サブスクライバー側のサブスクリプション データベースに対して、 [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)を実行します。 `@publisher` および `@publication` を指定します。  
  
2.  サブスクライバー側のサブスクリプション データベースに対して、 [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)を実行します。 `@publisher`、`@publisher_db`、`@publication` を指定し、`@job_login` および `@job_password` にサブスクライバーでディストリビューション エージェントを実行するときの Windows 資格情報を指定し、`@use_ftp` に `true` を指定します。  
  
3.  パブリッシャー側のパブリケーション データベースに対して [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) を実行し、プル サブスクリプションを登録します。 詳細については、「 [プル サブスクリプションの作成](../../../relational-databases/replication/create-a-pull-subscription.md)」をご覧ください。  
  
#### <a name="to-change-one-or-more-ftp-snapshot-delivery-settings-for-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションの FTP スナップショット配信の設定を変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)を実行します。 `@property` に次のいずれかの値を指定し、この新しい設定値を `@value` に指定します。  
  
    -   `ftp_address ` - スナップショットの配信に使用する FTP サーバーのアドレス。  
  
    -   `ftp_port` - FTP サーバーで使用されるポート。  
  
    -   `ftp_subdirectory` - FTP スナップショットに使用する既定の FTP ディレクトリのサブディレクトリ。  
  
    -   `ftp_login` - FTP サーバーへの接続に使用されるログイン。  
  
    -   `ftp_password` - FTP ログイン用のパスワード。  
  
2.  (省略可) 変更する各 FTP 設定について手順 1. を実行します。  
  
3.  (省略可) FTP スナップショット配信を無効にするには、パブリッシャー側のパブリケーション データベースに対して [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) を実行します。 `@property` の値に `enabled_for_internet` を、`@value` の値に `false` を指定します。  
  
#### <a name="to-change-ftp-snapshot-delivery-settings-for-a-merge-publication"></a>マージ パブリケーションの FTP スナップショット配信の設定を変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)を実行します。 `@property` に次のいずれかの値を指定し、この新しい設定値を `@value` に指定します。  
  
    -   `ftp_address` - スナップショットの配信に使用する FTP サーバーのアドレス。  
  
    -   `ftp_port` - FTP サーバーで使用されるポート。  
  
    -   `ftp_subdirectory` - FTP スナップショットに使用する既定の FTP ディレクトリのサブディレクトリ。  
  
    -   `ftp_login` - FTP サーバーへの接続に使用されるログイン。  
  
    -   `ftp_password` - FTP ログイン用のパスワード。  
  
2.  (省略可) 変更する各 FTP 設定について手順 1. を実行します。  
  
3.  (省略可) FTP スナップショット配信を無効にするには、パブリッシャー側のパブリケーション データベースに対して [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) を実行します。 `@property` の値に `enabled_for_internet` を、`@value` の値に `false` を指定します。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、サブスクライバーが FTP を使用してスナップショット データにアクセスできるマージ パブリケーションを作成します。 サブスクライバーは、FTP 共有にアクセスするときにセキュリティで保護された VPN 接続を使用する必要があります。 **sqlcmd** スクリプト変数を使用して、ログインとパスワードの値が入力されます。 詳細については、「[Use sqlcmd with Scripting Variables](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)」(sqlcmd でのスクリプト変数の使用) をご覧ください。  
  
 [!code-sql[HowTo#sp_createmergepub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_1.sql)]  
  
 次の例では、マージ パブリケーションに対するサブスクリプションを作成します。ここでは、サブスクライバーが FTP を使用してスナップショットを取得します。 サブスクライバーは、FTP 共有にアクセスするときにセキュリティで保護された VPN 接続を使用する必要があります。 **sqlcmd** スクリプト変数を使用して、ログインとパスワードの値が入力されます。 詳細については、「[Use sqlcmd with Scripting Variables](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)」(sqlcmd でのスクリプト変数の使用) をご覧ください。  
  
 [!code-sql[HowTo#sp_createmergepullsub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_2.sql)]  
  
 [!code-sql[HowTo#sp_createmergepullsubagent_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_3.sql)]  
  
## <a name="see-also"></a>参照  
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [パブリケーションとアーティクルのプロパティの変更](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [スナップショットを使用したサブスクリプションの初期化](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
