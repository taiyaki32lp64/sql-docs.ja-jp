---
title: SQL Server インストールにおけるセキュリティの考慮事項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- firewall systems [SQL Server]
- server message blocks [SQL Server]
- disabling protocols
- security [SQL Server], installations
- protocols [SQL Server], disabling
- NetBIOS [SQL Server]
- services [SQL Server], security
- SMB [SQL Server]
- isolating services [SQL Server]
- Setup [SQL Server], security
- low SQL Server installation privileges
- NTFS [SQL Server]
- physical security [SQL Server]
- file system security [SQL Server]
- installing SQL Server, security
ms.assetid: cf96155f-30a8-48b7-8d6b-24ce90dafdc7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eec38b5ecc524f0d3decd02c0832efd1909e8f00
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127888"
---
# <a name="security-considerations-for-a-sql-server-installation"></a>SQL Server インストールにおけるセキュリティの考慮事項
  セキュリティは、あらゆる製品、あらゆる企業にとって重要です。 単純なベスト プラクティスに従うことで、多くのセキュリティの脆弱性を避けることができます。 このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールする前と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をインストールした後の両方で考慮する必要があるセキュリティのベスト プラクティスについて説明します。 特定の機能のセキュリティについては、その機能の参照トピックで説明しています。  
  
## <a name="before-installing-includessnoversionincludesssnoversion-mdmd"></a>をインストールする前に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 サーバー環境をセットアップする場合、次のベスト プラクティスに従ってください。  
  
-   [物理的なセキュリティの強化](#physical_security)  
  
-   [ファイアウォールの使用](#firewalls)  
  
-   [サービスの分離](#isolated_services)  
  
-   [安全なファイル システムの構成](#sa_with_least_privileges)  
  
-   [NetBIOS とサーバー メッセージ ブロックの無効化](#disabled_protocols)  
  
-   [ドメイン コントローラーへの SQL Server のインストール](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md#Install_DC)  
  
###  <a name="physical_security"></a> Enhance Physical Security  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセキュリティは、物理的な分離と論理的な分離に基づいています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストールの物理的なセキュリティを強化するには、次のタスクを実行します。  
  
-   無許可の人が入れない部屋にサーバーを配置します。  
  
-   データベースをホストするコンピューターを物理的に保護された場所に配置します。水位報知器および火災報知器や消火システムによって監視された、鍵がかかるコンピューター ルームが理想的です。  
  
-   データベースは、企業イントラネットの安全なゾーンにインストールします。SQL Server をインターネットに直接接続しないでください。  
  
-   すべてのデータを定期的にバックアップし、バックアップを安全な場所に保存します。  
  
###  <a name="firewalls"></a> Use Firewalls  
 ファイアウォールは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストールのセキュリティを確保するために重要です。 次のガイドラインに従った場合、ファイアウォールが最も効果的になります。  
  
-   ファイアウォールをサーバーとインターネットの間に配置します。 ファイアウォールを有効にします。 ファイアウォールがオフになっている場合はオンにします。 ファイアウォールがオンになっている場合は、オフにしないでください。  
  
-   ファイアウォールでネットワークをセキュリティ ゾーンに分割します。 すべてのトラフィックをブロックした後、必要なトラフィックのみを選択的に許可します。  
  
-   多層環境では、複数のファイアウォールを使用してスクリーン サブネットを作成します。  
  
-   Windows ドメイン内にサーバーをインストールする場合は、Windows 認証を可能にする内部ファイアウォールを構成します。  
  
-   アプリケーションで分散トランザクションを使用する場合は、別々の MS DTC インスタンスの間で [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散トランザクション コーディネーター (MS DTC) トラフィックが許可されるように、ファイアウォールの構成が必要になる場合があります。 また、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]などのリソース マネージャーと MS DTC の間でトラフィックが許可されるようにファイアウォールを構成する必要もあります。  
  
 Windows ファイアウォールの既定の設定に関する詳細と、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、および [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]に影響する TCP ポートの説明については、「 [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」をご覧ください。  
  
###  <a name="isolated_services"></a> Isolate Services  
 サービスを分離すると、いずれかのサービスが停止した場合でも、その他のサービスに影響が及ぶのを防ぐことができます。 サービスを分離する場合は、次のガイドラインを考慮してください。  
  
-   各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを個別の Windows アカウントで実行します。 可能な場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスごとに権限の低い個別の Windows またはローカル ユーザー アカウントを使用します。 詳細については、「 [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
###  <a name="sa_with_least_privileges"></a> Configure a Secure File System  
 正しいファイル システムを使用することで、セキュリティは向上します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールには、次の作業を行う必要があります。  
  
-   NTFS ファイル システム (NTFS) を使用します。 NTFS は、FAT ファイル システムに比べて安定性と復旧性が高いことから、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールのファイル システムとして推奨されています。 また、NTFS では、ファイルとディレクトリのアクセス制御リスト (ACL) や暗号化ファイル システム (EFS) によるファイル暗号化などのセキュリティ オプションを使用できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール時に NTFS が検出されると、レジストリ キーとファイルに対して適切な ACL が設定されます。 これらの権限は変更しないでください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の今後のリリースでは、FAT ファイル システムを使用するコンピューターへのインストールはサポートされない可能性があります。  
  
    > [!NOTE]  
    >  EFS を使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を実行しているアカウントの ID でデータベース ファイルが暗号化されます。 ファイルの暗号化を解除できるのはこのアカウントだけです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を実行するアカウントを変更する場合は、まず以前のアカウントでファイルの暗号化を解除してから、新しいアカウントでそれらのファイルを再度暗号化する必要があります。  
  
-   重要なデータ ファイルには、RAID (Redundant Array of Independent Disks) を使用します。  
  
###  <a name="disabled_protocols"></a> Disable NetBIOS and Server Message Block  
 境界領域ネットワーク内のサーバーでは、NetBIOS とサーバー メッセージ ブロック (SMB) を含め、不要なプロトコルをすべて無効にする必要があります。  
  
 NetBIOS には次のポートを使用します。  
  
-   UDP/137 (NetBIOS ネーム サービス)  
  
-   UDP/138 (NetBIOS データグラム サービス)  
  
-   TCP/139 (NetBIOS セッション サービス)  
  
 SMB には次のポートを使用します。  
  
-   TCP/139  
  
-   TCP/445  
  
 Web サーバーとドメイン ネーム システム (DNS) サーバーは NetBIOS と SMB をいずれも必要としません。 これらのサーバーでは、両方のプロトコルを無効にしてユーザー列挙の脅威を緩和します。  
  
###  <a name="Install_DC"></a> ドメイン コントローラーへの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール  
 セキュリティ上の理由から、ドメイン コントローラーには [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] をインストールしないことをお勧めします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ時にインストールが中止されることはありませんが、次の制限事項が適用されます。  
  
-   ローカル サービス アカウントを使用して、ドメイン コントローラー上で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを実行することはできません。  
  
-   コンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールした後で、そのコンピューターをドメイン メンバーからドメイン コントローラーに変更することはできません。 ホスト コンピューターをドメイン コントローラーに変更する前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をアンインストールする必要があります。  
  
-   コンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールした後で、そのコンピューターをドメイン コントローラーからドメイン メンバーに変更することはできません。 ホスト コンピューターをドメイン メンバーに変更する前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をアンインストールする必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスは、クラスター ノードがドメイン コントローラーの場合はサポートされません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、読み取り専用ドメイン コントローラーにセキュリティ グループを作成したり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントを準備したりすることはできません。 この場合、セットアップは失敗します。  
  
## <a name="during-or-after-installation-of-includessnoversionincludesssnoversion-mdmd"></a>のインストール中またはインストール後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 インストール後にアカウントと認証モードに関する次のベスト プラクティスに従うと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストールのセキュリティを強化できます。  
  
 **サービス アカウント**  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスは、可能な限り低い権限で実行します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを、権限の低い Windows ローカル ユーザー アカウントまたはドメイン ユーザー アカウントに関連付けます。  
  
-   詳細については、「 [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
 **認証モード**  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]との接続には Windows 認証が必要です。  
  
-   Kerberos 認証を使用する。 詳細については、「 [Kerberos 接続用のサービス プリンシパル名の登録](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)」を参照してください。  
  
 **強力なパスワード**  
  
-   `sa` アカウントには、必ず強力なパスワードを割り当てます。  
  
-   パスワードの強度と有効期限に関するパスワード ポリシー チェックを必ず有効にします。  
  
-   すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに、必ず強力なパスワードを使用します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] のセットアップ時に、ログインは BUILTIN\Users グループに追加されます。 これにより、コンピューターの認証されたすべてのユーザーが public ロールのメンバーとして [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] のインスタンスにアクセスできるようになります。 BUILTIN\Users ログインを安全に削除して、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] アクセスを、個別のログインを持つコンピューター ユーザーまたはログインを持つ他の Windows グループのメンバーに制限できます。  
  
## <a name="see-also"></a>参照  
 [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)   
 [ネットワーク プロトコルとネットワーク ライブラリ](../../../2014/sql-server/install/network-protocols-and-network-libraries.md)   
 [Kerberos 接続用のサービス プリンシパル名の登録](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)  
  
  
