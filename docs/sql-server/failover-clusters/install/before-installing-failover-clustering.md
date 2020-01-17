---
title: フェールオーバー クラスタリングをインストールする前に | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.reviewer: ''
ms.prod: sql
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- clusters [SQL Server], preinstallation checklist
- installing failover clusters
- failover clustering [SQL Server], preinstallation checklist
ms.assetid: a655225d-8c54-4b30-95fd-31f588167899
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5d2fe2d80b0f9d54e877d6bc1be9a05c8c34c584
ms.sourcegitcommit: 4c5fb002719627f1a1594f4e43754741dc299346
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2019
ms.locfileid: "72517941"
---
# <a name="before-installing-failover-clustering"></a>フェールオーバー クラスタリングをインストールする前に
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server フェールオーバー クラスターをインストールする前に、SQL Server を実行するハードウェアとオペレーティング システムを選択する必要があります。 また、Windows Server フェールオーバー クラスタリング (WSFC) を構成し、ネットワーク、セキュリティ、およびフェールオーバー クラスターで実行するその他のソフトウェアに関する考慮事項を見直す必要があります。  
  
 Windows クラスターにローカル ディスク ドライブがあり、共有ドライブと同じドライブ文字が 1 つ以上のクラスター ノードでも使用されている場合、そのドライブに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をインストールできません。 この制限は、Windows フェールオーバー クラスター インスタンスの一部であるサーバー上の SQL Server フェールオーバー クラスター インスタンスとスタンドアロン インスタンスの両方に適用されます。
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスタリングの概念、機能、およびタスクについて詳しく学習するには、次のトピックも確認してください。  
  
|トピックの説明|トピック|  
|-----------------------|-----------|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスタリングの概念について説明し、関連するコンテンツとタスクへのリンクを示します。|[Always On フェールオーバー クラスター インスタンス &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー ポリシーの概念について説明し、組織の要件に合うようにフェールオーバー ポリシーを構成するためのリンクを示します。|[Failover Policy for Failover Cluster Instances](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)|  
|既存の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターの維持方法について説明します。|[フェールオーバー クラスター インスタンスの管理とメンテナンス](../../../sql-server/failover-clusters/windows/failover-cluster-instance-administration-and-maintenance.md)|  
|Windows Server フェールオーバー クラスター (WSFC) に [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] をインストールする方法について説明します。|[SQL Server Analysis Services をクラスター化する方法](https://go.microsoft.com/fwlink/p/?LinkId=396548)|  
  
 
  
##  <a name="BestPractices"></a> ベスト プラクティス  
  
-   [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [リリース ノート](https://go.microsoft.com/fwlink/?LinkId=296445)を確認する  
  
-   前提条件となるソフトウェアをインストールします。 セットアップで [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]のインストールまたはアップグレードを行う前に、以下に示す前提条件となるソフトウェアをインストールすると、インストール時間を短縮できます。 各フェールオーバー クラスター ノードでの前提条件となるソフトウェアのインストール、およびその後のノードの再起動は、セットアップを実行する前に 1 回だけ行います。  
  
    -   Windows PowerShell は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップでインストールされなくなりました。 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][!INCLUDE[ssDE](../../../includes/ssde-md.md)] のコンポーネントおよび [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]をインストールするには、Windows PowerShell が必要です。 Windows PowerShell がコンピューターで表示されない場合は、 [Windows Management Framework](https://go.microsoft.com/fwlink/?LinkId=186214) に関するページの手順に従って有効にすることができます。  
  
    -   .NET Framework 3.5 SP1 は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップでインストールされなくなりましたが、古い Windows オペレーティング システムに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をインストールする際に必要になる場合があります。 詳細については、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][リリース ノート](https://go.microsoft.com/fwlink/?LinkId=296445)をインストールするには、Windows PowerShell が必要です。  
  
    -   **[!INCLUDE[msCoName](../../../includes/msconame-md.md)] 更新パッケージ:** セットアップ時に .NET Framework 4 のインストールによるコンピューターの再起動を回避するには、[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] セットアップで [!INCLUDE[msCoName](../../../includes/msconame-md.md)] の更新プログラムをコンピューターにインストールする必要があります。  [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] を Windows 7 SP1 または [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] SP2 にインストールする場合、この更新プログラムは含まれています。 それより前の Windows オペレーティング システムにインストールする場合は、 [Windows Vista および Windows Server 2008 の .NET Framework 4.0 用 Microsoft Update](https://go.microsoft.com/fwlink/?LinkId=198093)からダウンロードしてください。  
  
    -   .NET Framework 4:セットアップでは、クラスター化されたオペレーティング システムに対して .NET Framework 4 がインストールされます。 インストール時間を短縮するには、セットアップを実行する前に .NET Framework 4 をインストールすることを検討してください。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ サポート ファイル。 これらのファイルは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] インストール メディアにある SqlSupport.msi を実行してインストールできます。  
  
-   ウイルス対策プログラムが WSFC クラスターにインストールされていないことを確認します。 詳細については、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] サポート技術情報で [ウイルス対策ソフトウェアによるクラスター サービスの問題](https://go.microsoft.com/fwlink/?LinkId=116986)に関する資料を参照してください。  
  
-   フェールオーバー クラスター インストールのクラスター グループに名前を付けるときは、次の文字を使用しないでください。  
  
    -   小なり演算子 (\<)  
  
    -   大なり演算子 (>)  
  
    -   二重引用符 (")  
  
    -   単一引用符 (')  
  
    -   アンパサンド (&)  
  
     既存のクラスター グループ名に、サポートされていない文字が含まれていないことも確認してください。  
  
-   すべてのクラスター ノードが一意になるように構成します。構成要素は、COM+、ディスク ドライブ文字、管理者グループのユーザーなどです。  
  
-   すべてのノードでシステム ログを消去し、そのシステム ログを再確認します。 続行する前に、そのログにエラー メッセージが記録されていないことを確認します。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターをインストールまたは更新する前に、インストール中に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コンポーネントを使用する可能性のあるすべてのアプリケーションとサービスを無効にします。ただしディスク リソースはオンラインのままにします。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップにより、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クラスター グループと、フェールオーバー クラスターに含まれるディスクとの間に自動的に依存関係が設定されます。 セットアップ前に、ディスクの依存関係を設定しないでください。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターのインストール時に、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ネットワーク リソース名に対応するコンピューター オブジェクト (Active Directory コンピューター アカウント) が作成されます。 [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] クラスターの場合、クラスター名アカウント (クラスター自体のコンピューター アカウント) には、コンピューター オブジェクトを作成する権限が必要です。 詳細については、 [Active Directory でのアカウントの構成](https://technet.microsoft.com/library/cc731002\(WS.10\).aspx)に関する記事を参照してください。  
  
    -   ストレージ オプションとして SMB ファイル共有を使用する場合は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ アカウントにファイル サーバーに対する SeSecurityPrivilege が必要です。 そのためには、ファイル サーバーで [ローカル セキュリティ ポリシー] コンソールを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [監査とセキュリティ ログの管理] **権限に** セットアップ アカウントを追加します。  
  
##  <a name="Hardware"></a> ハードウェア ソリューションの確認  
  
-   クラスター ソリューションに地理的に分散したクラスター ノードが含まれている場合は、ネットワークの待機時間や共有ディスクのサポートなどの項目も確認する必要があります。  
  
    -   [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] と [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]の詳細については、 [フェールオーバー クラスター用ハードウェアの検証](https://go.microsoft.com/fwlink/?LinkId=196817) に関するページおよび「 [Windows Server 2008 フェールオーバー クラスターに関するマイクロソフト サポート ポリシー](https://go.microsoft.com/fwlink/?LinkId=196818)」を参照してください。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をインストールするディスクが圧縮または暗号化されていないことを確認します。 圧縮されたドライブまたは暗号化されたドライブに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をインストールしようとすると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップが失敗します。  
  
-   SAN 構成は、 [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] および [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] の Advanced Server Edition および Datacenter Server Edition でもサポートされます。 Windows Catalog and Hardware Compatibility List の "Cluster/Multi-cluster Device" カテゴリには、SAN 対応のストレージ デバイス セットが一覧表示されます。このデバイス セットはテスト済みであり、複数の WSFC クラスターが接続されている SAN ストレージ装置としてサポートされています。 認定済みのコンポーネントを検索した後で、クラスター検証を実行してください。  
  
-   データ ファイルをインストールするための SMB ファイル共有もサポートされています。 詳細については、「 [データ ファイルのストレージの種類](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)」を参照してください。  
  
    > [!WARNING]  
    >  SMB ファイル共有ストレージとして Windows ファイル サーバーを使用する場合は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ アカウントにファイル サーバーに対する SeSecurityPrivilege が必要です。 そのためには、ファイル サーバーで [ローカル セキュリティ ポリシー] コンソールを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [監査とセキュリティ ログの管理] **権限に** セットアップ アカウントを追加します。  
    >   
    >  Windows ファイル サーバー以外の SMB ファイル共有ストレージを使用する場合は、ファイル サーバー側での設定についてストレージ ベンダーに問い合わせてください。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ではマウント ポイントがサポートされます。  
  
     マウントされたボリューム、つまりマウント ポイントを使用すると、1 つのドライブ文字を使用して多数のディスクまたはボリュームを参照できます。 通常のディスクやボリュームを参照するドライブ文字 D: を使用している場合、ドライブ文字 D: の下のディレクトリとして、新しいディスクまたはボリュームを接続するか "マウント" できます。この場合、新しいディスクまたはボリューム自体にドライブ文字は必要ありません。  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスタリングに関するマウント ポイントの他の考慮事項は次のとおりです。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のセットアップでは、マウントされたドライブの基本ドライブがドライブ文字と関連付けられている必要があります。 フェールオーバー クラスターのインストールでは、この基本ドライブをクラスター化されるドライブにする必要があります。 このリリースでは、ボリューム GUID はサポートされていません。  
  
    -   ドライブ文字を持つ基本ドライブは、フェールオーバー クラスター インスタンス間で共有できません。 フェールオーバー クラスターには、通常、このような制約がありますが、スタンドアロンのサーバーや複数インスタンスのサーバーにはこのような制約はありません。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のクラスター化インストールは、使用可能なドライブ文字数以下に制限されます。 オペレーティング システムのドライブ文字は 1 文字だけで指定し、他のすべてのドライブ文字を通常のクラスター ドライブか、マウント ポイントをホストするクラスター ドライブとして使用できると想定しているので、フェールオーバー クラスターごとの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の最大インスタンス数は 25 になります。  
  
        > [!TIP]  
        >  SMB ファイル共有オプションを使用すると、インスタンス数の上限を 25 より高くできます。 SMB ファイル共有をストレージ オプションとして使用する場合は、最大 50 の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスをインストールできます。  
  
    -   増設ドライブのマウント後のフォーマットはサポートされません。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターのインストールでは、tempdb ファイルをインストールする場合のみローカル ディスクがサポートされます。 tempdb のデータ ファイルおよびログ ファイルに指定されたパスが、すべてのクラスター ノードで有効であることを確認してください。 フェールオーバー中に、tempdb のディレクトリがフェールオーバーのターゲット ノード上で利用できない場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースはオンラインへの移行に失敗します。 詳細については、「 [データ ファイルのストレージの種類](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes) 」および「 [データベース エンジンの構成 - データ ディレクトリ](https://msdn.microsoft.com/library/9b1fa0fc-623b-479a-afc3-4f13bd850487)」を参照してください。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターを iSCSI テクノロジのコンポーネント上に配置する場合は、慎重に行ってください。 詳細については、「 [iSCSI テクノロジ コンポーネント上の SQL Server のサポート](https://go.microsoft.com/fwlink/?LinkId=116960)」を参照してください。  
  
-   詳細については、 [Microsoft クラスタリング用の SQL Server サポート ポリシー](https://go.microsoft.com/fwlink/?LinkId=116958)に関するページを参照してください。  
  
-   適切なクォーラム ドライブ構成の詳細については、 [クォーラムの構成](https://go.microsoft.com/fwlink/?LinkId=196816)に関するページを参照してください。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の元のインストール ファイルおよびクラスターが、異なる複数のドメインに分散している場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターをインストールするには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターに対して使用できる現在のドメインにインストール ファイルをコピーします。  
  
##  <a name="Security"></a> セキュリティに関する注意点の確認  
  
-   暗号化を使用するには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター内のすべてのノードに、WSFC クラスターの完全修飾 DNS 名を使用してサーバー証明書をインストールします。 たとえば、"Test1.DomainName.com" と "Test2.DomainName.com" という名前のノード、および "Virtsql" という名前の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスが存在する 2 ノード クラスターでは、"Virtsql.DomainName.com" の証明書を入手し、test1 ノードと test2 ノードにその証明書をインストールする必要があります。 その後、 **構成マネージャーの** [プロトコル暗号化を設定する] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] チェック ボックスをオンにして、フェールオーバー クラスターでの暗号化を構成できるようになります。  
  
    > [!IMPORTANT]  
    >  **[プロトコル暗号化を設定する]** チェック ボックスは、フェールオーバー クラスター インスタンスに参加しているすべてのノードに証明書をインストールした後でオンにしてください。  
  
-   以前のバージョンとサイド バイ サイドでインストールされている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスは、グローバル ドメイン グループのみで検出されたアカウントを使用する必要があります。 さらに、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスによって使用されるアカウントは、ローカルの Administrators グループに表示されないようにする必要があります。 このガイドラインに沿っていない場合、予期しないセキュリティ動作を招くことになります。  
  
-   フェールオーバー クラスターを作成するには、サービスとしてログオンする権限、およびフェールオーバー クラスター インスタンスのすべてのノード上にあるオペレーティング システムの一部として機能する権限を持つ、ローカルな管理者である必要があります。  
  
-   [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]では、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] サービスで使用するためのサービス SID が自動的に生成されます。 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] の以前のバージョンからアップグレードされた [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]フェールオーバー クラスター インスタンスでは、既存のドメイン グループおよび ACL 構成が保持されます。  
  
-   ドメイン グループは、コンピューターのアカウントと同じドメイン内にある必要があります。 たとえば、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストール先のコンピューターが、MYDOMAIN の子である SQLSVR ドメイン内にある場合は、SQLSVR ドメイン内のグループを指定する必要があります。 SQLSVR ドメインには、MYDOMAIN に属するユーザー アカウントが含まれることもあります。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスタリングは、クラスター ノードがドメイン コントローラーの場合はインストールできません。  
  
-   「 [SQL Server インストールにおけるセキュリティの考慮事項](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)の内容について検討してください。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]で Kerberos 認証を有効にするには、 [サポート技術情報の「](https://support.microsoft.com/kb/319723) SQL Server で Kerberos 認証を使用する方法 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 」を参照してください。  

-   SQL Server フェールオーバー クラスター インスタンス (FCI) では、クラスター ノードをドメイン参加させる必要があります。 次の構成は**サポートされていません**。 
    *   ワークグループ クラスター上の SQL FCI。 
    *   マルチドメイン クラスター上の SQL FCI。   
    *   ドメイン + ワークグループ クラスター上の SQL FCI。 

  
##  <a name="Network"></a> ネットワーク、ポート、およびファイアウォールに関する注意点の確認  
  
-   すべてのプライベート ネットワーク カードの NetBIOS が無効になっていることを確認してから、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを開始します。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のネットワーク名と IP アドレスは、ファイル共有などの、フェールオーバー クラスタリング以外の目的に使用しないでください。 ファイル共有リソースを作成する場合、異なる一意なネットワーク名と IP アドレスをそのリソースに使用する必要があります。  
  
    > [!IMPORTANT]  
    >  データ ドライブでファイル共有を使用すると [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の動作とパフォーマンスに影響することがあるので、ファイル共有の使用はお勧めしません。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でクラスター内の名前付きパイプと TCP/IP Sockets over TCP/IP の両方がサポートされている場合でも、クラスター化された構成では TCP/IP ソケットを使用することをお勧めします。  
  
-   ISA Server は Windows クラスタリングでサポートされていないので、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターでもサポートされないことに注意してください。  
  
-   リモート レジストリ サービスを起動して実行している必要があります。  
  
-   リモート管理が有効になっている必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ポートでは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ネットワークの構成で、ブロックを解除するインスタンスの TCP/IP プロトコルを確認します。 インストール後に TCP を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続する場合は、IPALL に対して TCP ポートを有効にする必要があります。 既定では、SQL Browser は UDP ポート 1434 でリッスンします。  
  
-   フェールオーバー クラスター セットアップ操作には、ネットワーク バインド順序をチェックするルールが含まれています。 バインド順序が正しいように見えても、実際には実体のない無効化された NIC 構成がシステムに存在している場合があります。 実体のない NIC 構成が存在すると、バインド順序に影響が生じ、バインド順序ルールから警告が発行されることがあります。 この状況を回避するには、次の手順で無効なネットワーク アダプターを特定し、削除します。  
  
    1.  コマンド プロンプトで、「set devmgr_Show_Nonpersistent_Devices=1」と入力します。  
  
    2.  「start Devmgmt.msc」と入力し、実行します。  
  
    3.  ネットワーク アダプターの一覧を展開します。 この一覧には、物理的なアダプターのみが表示されているはずです。 無効なネットワーク アダプターがある場合は、セットアップでネットワーク バインド順序ルールに関するエラーが報告されます。 コントロール パネルの [ネットワーク接続] でも、そのアダプターが無効であることが示されます。 コントロール パネルの [ネットワーク接続] に表示される一覧が、devmgmt.msc を実行して示される有効な物理的アダプターの一覧と同じであることを確認します。  
  
    4.  SQL Server セットアップを実行する前に、無効なネットワーク アダプターを削除します。  
  
    5.  セットアップが完了したら、コントロール パネルの [ネットワーク接続] に戻り、現在使用されていないネットワーク アダプターを無効にします。  
  
##  <a name="OS_Support"></a> オペレーティング システムの確認  
 オペレーティング システムが適切にインストールされており、フェールオーバー クラスタリングをサポートするように設定されていることを確認します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の各エディションおよびそれらをサポートするオペレーティング システムの一覧を次の表に示します。  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のエディション|[!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] Enterprise|[!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] Datacenter Server|[!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] Enterprise|[!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] Datacenter Server|  
|---------------------------------------|------------------------------------------------|-------------------------------------------------------|----------------------------------------------|-----------------------------------------------------|  
|[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Enterprise (64 ビット) x64*|はい|はい|可**|可**|  
|[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Enterprise (32 ビット)|はい|はい|||  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Developer (64 ビット)|はい|はい|可**|可**|  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Developer (32 ビット)|はい|はい|||  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Standard (64 ビット)|はい|はい|はい|はい|  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Standard (32 ビット)|はい|はい|||  
  
 *[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クラスターは、WOW モードではサポートされません。 これには、WOW で最初にインストールされた [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターの以前のバージョンからのアップグレードが含まれます。 この場合に使用できる唯一のアップグレード オプションは、新しいバージョンをサイド バイ サイドでインストールしてから移行することです。  
  
 ** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] マルチサブネット フェールオーバー クラスタリングでサポートされます。  
  
##  <a name="MultiSubnet"></a> マルチサブネットの構成に関するその他の注意点  
 以下のセクションでは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] マルチサブネット フェールオーバー クラスターをインストールする場合に留意する要件について説明します。 マルチサブネットを構成する場合は、複数のサブネットにわたってクラスター化されるため、この操作では、複数の IP アドレスが使用され、IP アドレス リソースの依存関係への変更が行われます。  
  
### <a name="includessnoversionincludesssnoversion-mdmd-edition-and-operating-system-considerations"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のエディションとオペレーティング システムに関する注意点  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] マルチサブネット フェールオーバー クラスターをサポートする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のエディションについては、「 [SQL Server 2016 の各エディションがサポートされる機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] マルチサブネット フェールオーバー クラスターを作成するには、まず、複数のサブネット上に [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] マルチサイト フェールオーバー クラスターを作成する必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターでは、Windows Server フェールオーバー クラスターを利用して、フェールオーバー発生時に IP 依存関係の条件が有効であるかどうかを確認します。  
  
-   [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] では、すべてのクラスター サーバーが同じ Active Directory ドメインに属している必要があります。 したがって、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] マルチサブネット フェールオーバー クラスターでは、クラスター ノードが異なるサブネットにある場合でも、それらはすべて同じ Active Directory ドメインに属している必要があります。  
  
#### <a name="ip-address-and-ip-address-resource-dependencies"></a>IP アドレスと IP アドレス リソースの依存関係  
  
1.  IP アドレス リソースの依存関係は、マルチサブネット構成では OR に設定されています。 詳細については、「[新しい SQL Server フェールオーバー クラスターの作成 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)」をご覧ください。  
  
2.  AND-OR の混合 IP アドレスの依存関係はサポートされていません。 たとえば、<\<IP1> AND \<IP2> OR \<IP3> はサポートされていません。  
  
3.  1 つのサブネットに複数の IP アドレスを使用することはサポートされていません。  
  
     同じサブネットに対して構成された複数の IP アドレスを使用する場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 起動中にクライアント接続障害が発生する可能性があります。  
  
#### <a name="related-content"></a>関連コンテンツ  
 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] のマルチサイト フェールオーバーの詳細については、 [Windows Server 2008 R2 フェールオーバー クラスタリングに関するサイト](https://technet.microsoft.com/library/ff182338\(v=WS.10\).aspx) および「 [Design for a Clustered Service or Application in a Multi-Site Failover Cluster (マルチサイト フェールオーバー クラスターでのクラスター化サービスまたはアプリケーションの設計)](https://go.microsoft.com/fwlink/?LinkId=177873)」を参照してください。  
  
##  <a name="WSFC"></a> Windows Server フェールオーバー クラスターの構成  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Cluster Service (WSFC) は、サーバー クラスターの少なくとも 1 つのノード上で構成する必要があります。 また、WSFC と共に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Business Intelligence、または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Standard を実行する必要もあります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise では、16 ノードまでのフェールオーバー クラスターがサポートされています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Business Intelligence および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Standard では、2 ノードのフェールオーバー クラスターがサポートされています。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスのリソース DLL は、WSFC クラスター マネージャーで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースの可用性をチェックするために使用する 2 つの関数をエクスポートします。 詳細については、「 [フェールオーバー クラスター インスタンスのフェールオーバー ポリシー](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)」をご覧ください。  
  
-   WSFC では、IsAlive チェックを使用して、フェールオーバー クラスター インスタンスが実行されていることを確認できる必要があります。 そのため、信頼関係接続を使用して、サーバーに接続する必要があります。 既定では、クラスター サービスを実行するアカウントはクラスター内のノードの管理者として構成されていないため、BUILTIN\Administrators グループには [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]にログインする権限がありません。 これらの設定が変更されるのは、クラスター ノードで権限を変更する場合だけです。  
  
-   ドメイン ネーム サービス (DNS) または Windows インターネット ネーム サービス (WINS) を構成します。 DNS サーバーまたは WINS サーバーは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターがインストールされる環境で実行されている必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップでは、ドメイン ネーム サービスで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] IP インターフェイスの仮想参照を動的に登録する必要があります。 DNS サーバーの構成では、クラスター ノードでオンラインの IP アドレス マップをネットワーク名に動的に登録できるようにする必要があります。 動的登録を完了できないと、セットアップが失敗し、インストールがロールバックされます。 詳細については、 [こちらのサポート技術情報の記事](https://support.microsoft.com/kb/947048)を参照してください。  
  
##  <a name="MSDTC"></a>[!INCLUDE[msCoName](../../../includes/msconame-md.md)] 分散トランザクション コーディネーターのインストール  
 フェールオーバー クラスターに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をインストールする前に、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 分散トランザクション コーディネーター (MSDTC) クラスター リソースを作成する必要があるかどうかを判断します。 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]だけをインストールする場合、MSDTC クラスター リソースは必要ありません。 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] と SSIS やワークステーション コンポーネントをインストールする場合、または分散トランザクションを使用する場合は、MSDTC のインストールが必要です。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]のみのインスタンスには MSDTC は必要ありません。  
  
 [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] と [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]では、MSDTC の複数のインスタンスを 1 つのフェールオーバー クラスターにインストールできます。 インストールされている MSDTC の最初のインスタンスが、MSDTC のクラスターの既定のインスタンスになります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、この MSDTC インスタンスが自動的に使用され、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ローカル クラスター リソース グループにインストールされている MSDTC インスタンスが利用されます。 ただし、個々のアプリケーションはクラスターのすべての MSDTC インスタンスにマップすることができます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]によって選択される MSDTC のインスタンスは、次のいずれかのルールを満たすものです。  
  
-   ローカル グループにインストールされた MSDTC を使用する。  
  
-   MSDTC のマップされたインスタンスを使用する。  
  
-   クラスターの既定の MSDTC インスタンスを使用する。  
  
-   ローカル コンピューターのインストール済み MSDTC インスタンスを使用する。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカル クラスター グループにインストールされている MSDTC インスタンスが失敗すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、既定のクラスター インスタンスまたはローカル コンピューターの MSDTC インスタンスが自動的には使用されません。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] グループから失敗した MSDTC インスタンスを完全に削除して、別の MSDTC インスタンスを使用する必要があります。 同様に、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のマッピングを作成し、マップされる MSDTC インスタンスが失敗した場合は、分散トランザクションも失敗します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で別の MSDTC インスタンスを使用するには、MSDTC インスタンスを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカルのクラスター グループに追加するか、マッピングを削除する必要があります。  
  
### <a name="configure-includemsconameincludesmsconame-mdmd-distributed-transaction-coordinator"></a>[!INCLUDE[msCoName](../../../includes/msconame-md.md)] 分散トランザクション コーディネーターの構成  
 オペレーティング システムをインストールしてクラスターを構成した後で、クラスター アドミニストレーターを使用して、クラスター内で機能するように MSDTC を構成する必要があります。 MSDTC のクラスター化に失敗しても [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップは中断しませんが、MSDTC が適切に構成されていない場合は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のアプリケーション機能に影響が生じる可能性があります。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2016 のインストールに必要なハードウェアおよびソフトウェア](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [システム構成チェッカーの検査パラメーター](../../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [フェールオーバー クラスター インスタンスの管理とメンテナンス](../../../sql-server/failover-clusters/windows/failover-cluster-instance-administration-and-maintenance.md)  
  
  

