---
title: Web 同期の構成 | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- SQL10.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1
helpviewer_keywords:
- Web synchronization, security best practices
- Web synchronization, configuring
ms.assetid: 21f8e4d4-cd07-4856-98f0-9c9890ebbc82
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 95acac097d1c3ec5ffd4989058db0c2927441554
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907235"
---
# <a name="configure-web-synchronization"></a>Web 同期の構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] マージ レプリケーションの Web 同期オプションを使用すると、インターネット経由で HTTPS プロトコルを使用してデータをレプリケートできます。 Web 同期を使用するには、最初に次の構成操作を実行する必要があります。  
  
1.  新しいドメイン アカウントを作成し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインをマップします。  
  
2.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] インターネット インフォメーション サービス (IIS) を実行しているコンピューターで、サブスクリプションが同期されるように構成します。  
  
3.  Web 同期が許可されるようにマージ パブリケーションを構成します。  
  
4.  Web 同期が使用されるように 1 つ以上のサブスクリプションを構成します。  

> [!NOTE]  
>  大量のデータや **varchar(max)** などのサイズの大きなデータ型を含むデータをレプリケートする場合は、このトピックの「大量のデータのレプリケート」を参照してください。  
  
 Web 同期を正しく設定するには、特定の要件やポリシーを満たすためにセキュリティをどのように構成するかを決める必要があります。 先にこれらについて決定し、必要なアカウントを作成してから、IIS、パブリケーション、およびサブスクリプションの構成を開始することをお勧めします。  
  
 以降の手順では、説明を簡単にするために、ローカル アカウントを使用した場合の簡素化されたセキュリティ構成について説明します。 この簡素化された構成は、IIS と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパブリッシャーおよびディストリビューターの両方を同一のコンピューターで実行する環境に適しています。ただし、運用環境ではマルチサーバー トポロジを使用する可能性が高く、その方が推奨されます。 この手順のローカル アカウントは、ドメイン アカウントに置き換えることもできます。  
  
## <a name="creating-new-accounts-and-mapping-sql-server-logins"></a>新しいアカウントの作成と SQL Server ログインのマッピング  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーション リスナー (replisapi.dll) は、レプリケーション Web サイトに関連付けられたアプリケーション プールに指定されているアカウントを借用することでパブリッシャーに接続します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーション リスナーに使用するアカウントには、「[Merge Agent Security](../../relational-databases/replication/merge-agent-security.md)」(マージ エージェント セキュリティ) の「Connect to the Publisher or Distributor」(パブリッシャーまたはディストリビューターへの接続) で説明されている権限が必要です。 このアカウントに必要な権限の概要を以下に示します。  
  
-   パブリケーション アクセス リスト (PAL) のメンバーである。  
  
-   パブリケーション データベースのユーザーに関連付けられたログインにマップされている。  
  
-   ディストリビューション データベース内のユーザーに関連付けられているログインにマップされている。  
  
-   スナップショット共有の読み取り権限を持つ。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーションを初めて使用する場合は、レプリケーション エージェントのアカウントとログインも作成する必要があります。 詳細については、このトピックの「パブリケーションの構成」および「サブスクリプションの構成」を参照してください。  
  
 Web 同期を構成する前に、このトピックの「Web 同期のセキュリティの推奨事項」を一読することをお勧めします。 Web 同期のセキュリティの詳細については、「 [Security Architecture for Web Synchronization](../../relational-databases/replication/security/security-architecture-for-web-synchronization.md)」を参照してください。  
  
## <a name="configuring-the-computer-that-is-running-iis"></a>IIS を実行しているコンピューターの構成  
 Web 同期を使用するには、IIS をインストールして構成する必要があります。 レプリケーション Web サイトの URL がないと、Web 同期を使用するようにパブリケーションを構成できません。  
  
 Web 同期は、バージョン 5.0 以降の IIS でサポートされます。 IIS 7.0 では、Web 同期の構成ウィザードはサポートされていません。 SQL Server 2012 以降では、IIS サーバーで Web 同期コンポーネントを使用する場合は、レプリケーションとともに SQL Server をインストールすることをお勧めします。 これは無料の SQL Server Express edition で構いません。  
  
 Web 同期では SSL は必須です。 証明機関によって発行されたセキュリティ証明書が必要になります。 テストだけが目的の場合は、独自に発行したセキュリティ証明書を使用できます。  
   
  
 **Web 同期用に IIS を構成するには**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:[Web 同期用の IIS の構成](../../relational-databases/replication/configure-iis-for-web-synchronization.md)  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)][ ] :[Web 同期用の IIS 7 の構成](../../relational-databases/replication/configure-iis-7-for-web-synchronization.md)  
  
## <a name="creating-a-web-garden"></a>Web ガーデンの作成  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーション リスナーでは、スレッドごとに同時に 2 つの同期処理がサポートされます。 この制限を超えると、レプリケーション リスナーが応答しなくなる可能性があります。 replisapi.dll に割り当てられるスレッドの数は、アプリケーション プールの "ワーカー プロセスの最大数" プロパティで決まります。 既定では、このプロパティは 1 に設定されます。  
  
 1 つの CPU で同時にサポートできる同期処理の数を増やすには、"ワーカー プロセスの最大数" プロパティの値を大きくします。 CPU ごとのワーカー プロセスの数を増やしてスケールアウトすることを、"Web ガーデン" を作成するといいます。  
  
 Web ガーデンを作成すると、同時に 3 つ以上のサブスクライバーを同期できるようになります。 このとき、replisapi.dll による CPU 使用率も増加するため、サーバーの全体的なパフォーマンスは低下することがあります。 "ワーカー プロセスの最大数" の値を選択するときは、それらのバランスを考慮することが重要です。  
  
#### <a name="to-increase-maximum-worker-processes-in-iis-7"></a>IIS 7 のワーカー プロセスの最大数を増やすには  
  
1.  **インターネット インフォメーション サービス (IIS) マネージャー**で、ローカル サーバーのノードを展開し、 **[アプリケーション プール]** ノードをクリックします。  
  
2.  Web 同期サイトに関連付けられているアプリケーション プールを選択し、 **[アクション]** ペインの **[詳細設定]** をクリックします。  
  
3.  [詳細設定] ダイアログで、 **[モデルの処理]** という見出しの下にある **[ワーカー プロセスの最大数]** というラベルの行をクリックします。 プロパティの値を変更し、 **[OK]** をクリックします。  
  
## <a name="configuring-the-publication"></a>パブリケーションの構成  
 Web 同期を使用するには、標準のマージ トポロジと同じ方法でパブリケーションを作成します。 詳細については、「[Publish Data and Database Objects](../../relational-databases/replication/publish/publish-data-and-database-objects.md)」(データとデータベース オブジェクトのパブリッシュ) をご覧ください。  
  
 パブリケーションを作成した後、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、レプリケーション管理オブジェクト (RMO) のいずれかを使用して、Web 同期を許可するオプションを有効にします。 Web 同期を有効にするには、サブスクライバー接続の Web サーバー アドレスを指定する必要があります。  
  
 初めてパブリッシャーを使用している場合は、ディストリビューターおよびスナップショット共有も構成する必要があります。 各サブスクライバー側のマージ エージェントには、スナップショット共有の読み取り権限が必要です。 詳細については、「[Configure Distribution](../../relational-databases/replication/configure-distribution.md)」(ディストリビューションの構成) と「[Secure the Snapshot Folder](../../relational-databases/replication/security/secure-the-snapshot-folder.md)」(スナップショット フォルダーのセキュリティ保護) をご覧ください。  
  
 **gen** は、websync xml ファイルの予約語です。 **gen**という名前の列を含むテーブルをパブリッシュしようとしないでください。  
  
## <a name="configuring-the-subscription"></a>サブスクリプションの構成  
 パブリケーションを有効にし、IIS を構成した後、プル サブスクリプションを作成し、そのプル サブスクリプションが IIS を使用して同期するように指定します。 (Web 同期はプル サブスクリプションでのみサポートされます)。  
  
## <a name="upgrading-from-an-earlier-version-of-sql-server"></a>以前のバージョンの SQL Server からのアップグレード  
 既存の構成済み Web 同期トポロジがあるときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をアップグレードする場合は、Replisapi.dll の最新バージョンが、Web 同期で使用される仮想ディレクトリにコピーされていることを確認する必要があります。 既定では、Replisapi.dll の最新バージョンは C:\Program Files\Microsoft SQL Server\\<nnn\>\COM にあります。  
  
## <a name="replicating-large-volumes-of-data"></a>大量のデータのレプリケート  
 サブスクライバー コンピューター上で発生する可能性があるメモリの問題を回避できるように、Web 同期では、変更の転送に使用する XML ファイルに既定の最大サイズの 100 MB を使用します。 この制限は、次のレジストリ キーを設定して引き上げることができます。  
  
 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\Replication**  
  
 **WebSyncMaxXmlSize DWORD 2000000**  
  
 このキーに許容される値の範囲は 100 MB ～ 4 GB です。 値は KB 単位で指定します。 このパラメーターに大きな値を設定することで、その量のデータを同期できることが保証されるわけではありません。 サブスクライバー コンピューター上で使用できる連続したメモリの量によって制限することが効果的です。 100 MB を超える値を設定する必要がある場合は、値を段階的に増加させ、サブスクライバー上の一般的なワークロードでメモリの使用量をテストすることをお勧めします。  
  
 XML ファイルの最大サイズが 4 GB でも、バッチ内のそのファイルからの変更がレプリケーションによって同期されます。 データとメタデータの最大バッチ サイズは 25 MB です。 各バッチ内のデータが約 20 MB を超えないようにする必要があります。この場合、メタデータやその他のオーバーヘッドも考慮に入れます。 この制限による影響を次に示します。  
  
-   データとメタデータが 25 MB を超す要因となる列はレプリケートできません。 これは、 **varchar(max)** などのサイズの大きなデータ型を含む行をレプリケートするときに問題になる場合があります。  
  
-   大量のデータをレプリケートする場合に、マージ エージェントのバッチ サイズの調整が必要になることがあります。  
  
 マージ レプリケーションのバッチ サイズは、アーティクルごとの変更のコレクションである *生成結果*で示されます。 1 つのバッチ内の生成結果の数は、マージ エージェントの -**DownloadGenerationsPerBatch** および -**UploadGenerationsPerBatch** パラメーターを使用して指定します。 詳細については、「 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)」を参照してください。  
  
 大量のデータを扱う場合は、バッチ処理の各パラメーターに小さい数を指定します。 最初は値を 10 にして、アプリケーションのニーズとパフォーマンスに応じて調整することをお勧めします。 通常、これらのパラメーターは、エージェント プロファイルで指定します。 プロファイルの詳細については、「 [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md)」を参照してください。  
  
## <a name="security-best-practices-for-web-synchronization"></a>Web 同期のセキュリティの推奨事項  
 Web 同期にはセキュリティ関連の選択項目が多数あります。 次の方法が推奨されます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディストリビューターおよびパブリッシャーは、同じコンピューター上に存在できます (マージ レプリケーションの一般的なセットアップ)。 ただし、IIS は別のコンピューターにインストールする必要があります。  
  
-   SSL (Secure Sockets Layer) を使用して、IIS を実行しているコンピューターとサブスクライバーとの間の接続を暗号化します。 これは、Web 同期では必須です。  
  
-   サブスクライバーから IIS までの接続に基本認証を使用します。 基本認証を使用すると、IIS では、委任を必要とすることなくサブスクライバーの代わりにパブリッシャーやディストリビューターに接続できます。 統合認証を使用する場合は、委任が必要です。  
  
    > [!NOTE]  
    >  基本認証は、資格情報を IIS に渡すための方法です。 基本認証を使用しても、IIS への接続に Windows ドメイン アカウントを指定する機能には影響ありません。  
  
-   スナップショット エージェントを Windows ドメイン アカウントで実行するように指定し、エージェントがそのアカウントとして接続を確立するように指定します (これは既定の構成です)。各マージ エージェントを、サブスクライバー コンピューターを使用するユーザーのドメイン アカウントで実行するように指定し、エージェントがそのアカウントとして接続を確立するように指定します。  
  
     エージェントに必要な権限の詳細については、「 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)」を参照してください。  
  
-   サブスクリプションの新規作成ウィザードの **[Web サーバー情報]** ページでアカウントとパスワードを指定するとき、または [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) の `@internet_url` および `@internet_login` パラメーターの値を指定するときに、マージ エージェントで使用されるドメイン アカウントと同じアカウントを指定します。 このアカウントには、スナップショット共有の読み取り権限が必要です。  
  
-   各パブリケーションでは、IIS 用に個別の仮想ディレクトリを使用する必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーション リスナー (Replisapi.dll) の実行に使用するアカウントは、同期の際にパブリッシャーとディストリビューターに接続するアカウントでもあります。 したがって、パブリッシャーとディストリビューターで SQL ログイン アカウントにマップされている必要があります。 詳細については、「[Configure IIS for Web Synchronization](../../relational-databases/replication/configure-iis-for-web-synchronization.md)」(Web 同期用の IIS の構成) の「Setting Permissions for the SQL Server Replication Listener」(SQL Server レプリケーション リスナーの権限の設定) セクションをご覧ください。  
  
-   IIS を実行しているコンピューターにパブリッシャーからスナップショットを配信するときに、FTP を使用できます。 IIS を実行しているコンピューターからサブスクライバーにスナップショットを配信するときには、常に HTTPS が使用されます。 詳細については、「[FTP によるスナップショットの転送](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)」を参照してください。  
  
-   レプリケーション トポロジ内のサーバーがファイアウォールの内側にあるとき、Web 同期を有効にするために、ファイアウォールのポートを開くことが必要になる場合があります。  
  
    -   サブスクライバー コンピューターは、SSL を使用する HTTPS (通常はポート 443 を使用するように構成されます) 経由で、IIS を実行しているコンピューターに接続します。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバーは、HTTP (通常はポート 80 を使用するように構成されます) 経由の接続を実行することもできます。  
  
    -   通常、IIS を実行しているコンピューターは、ポート 1433 (既定のインスタンス用) を使用してパブリッシャーまたはディストリビューターに接続します。 パブリッシャーまたはディストリビューターが、サーバー上の既定のインスタンスとは別に存在する名前付きインスタンスである場合、その名前付きインスタンスへの接続には通常はポート 1500 が使用されます。  
  
    -   IIS を実行しているコンピューターがファイアウォールによってディストリビューターから分離されており、スナップショットの配信に FTP 共有が使用される場合は、FTP 用のポートが開かれている必要があります。 詳細については、「[Transfer Snapshots Through FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)」(FTP によるスナップショットの転送) をご覧ください。  
  
> [!IMPORTANT]  
>  ファイアウォールのポートを開くと、サーバーが攻撃を受けやすくなります。 ポートを開く前に、ファイアウォール システムについて理解しておいてください。 詳細については、「 [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [マージ レプリケーションの Web 同期](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
