---
title: 別のエディションへのアップグレード
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 31d16820-d126-4c57-82cc-27701e4091bc
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 996d0f90a76760c4c02a7a3d2bbf08f8c7ba6981
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258794"
---
# <a name="upgrade-to-a-different-edition-of-sql-server-setup"></a>SQL Server の別のエディションへのアップグレード (セットアップ)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、[!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] のさまざまなエディション間でのエディションのアップグレードをサポートしています。 各エディションでサポートされるアップグレード パスについては、「 [サポートされているバージョンとエディションのアップグレード](../../database-engine/install-windows/supported-version-and-edition-upgrades-2017.md)」をご覧ください。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]インスタンスのエディションのアップグレードを開始する前に、次の記事を確認してください。  

- [エディションと SQL Server 2017 のサポートされる機能](../../sql-server/editions-and-components-of-sql-server-2017.md)  
- [エディションと SQL Server 2016 のサポートされる機能](../../sql-server/editions-and-components-of-sql-server-2016.md)  
- [SQL Server のエディション別の計算容量制限](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)  
- [SQL Server のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
> [!NOTE]  
> **フェールオーバー クラスター インスタンス上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスのノードのいずれかで、エディションのアップグレードを実行するだけです。 このノードはアクティブとパッシブのいずれかになります。エディションのアップグレード中にリソースがオフラインになることはありません。 エディションをアップグレードした後は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを再起動するか、別のノードにフェールオーバーする必要があります。  
  
## <a name="prerequisites"></a>前提条件  
ローカル インストールの場合は、セットアップを管理者として実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をリモート共有からインストールする場合は、そのリモート共有に対する読み取り権限を持つドメイン アカウントを使用する必要があります。  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エディションの変更をアクティブ化するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサービスを再起動する必要があります。 これにより、サービスがオフラインの間、アプリケーションのダウンタイムが発生します。  
  
## <a name="procedure"></a>手順  
  
### <a name="to-upgrade-to-a-different-edition-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] の別のエディションにアップグレードするには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール メディアを挿入します。 ルート フォルダーの setup.exe をダブルクリックするか、構成ツールから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール センターを起動します。 ネットワーク共有からインストールするには、ネットワーク共有上のルート フォルダーに移動し、Setup.exe をダブルクリックします。  
  
2.  [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] の既存のインスタンスを他のエディションにアップグレードするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール センターの **[メンテナンス]** をクリックし、 **[エディションのアップグレード]** をクリックします。  
  
3.  セットアップ サポート ファイルが必要な場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップによってインストールされます。 コンピューターの再起動を求めるメッセージが表示されたら、再起動してから続行します。  
  
4.  システム構成チェッカーにより、コンピューターで検出処理が実行されます。 続行するには、 **[OK]** をクリックします。  
  
5.  [プロダクト キー] ページで、オプション ボタンをクリックして、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の無償のエディションにアップグレードするかどうか、または SQL Server の製品版の PID キーを持っているかどうかを指定します。 詳細については、[SQL Server のエディションとコンポーネント](../../sql-server/editions-and-components-of-sql-server-2017.md)に関するページと、「[サポートされているバージョンとエディションのアップグレード](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)」を参照してください。  
  
6.  [ライセンス条項] ページで使用許諾契約書を読み、使用許諾条件に同意する場合は対応するチェック ボックスをオンにします。 続行するには、 **[次へ]** をクリックします。 セットアップを終了するには、 **[キャンセル]** をクリックします。  
  
7.  [インスタンスの選択] ページで、アップグレードする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定します。  
  
8.  [エディション アップグレード ルール] ページでは、エディションのアップグレード操作が開始される前に、コンピューターの構成が検証されます。  
  
9. [エディションのアップグレードの準備完了] ページには、セットアップ時に指定したインストール オプションのツリー ビューが表示されます。 続行するには、 **[アップグレード]** をクリックします。  
  
10. エディションのアップグレード処理時に、新しい設定内容が反映されるようにサービスを再起動する必要があります。 エディションのアップグレードが終了すると、[完了] ページにエディションのアップグレードについての概要ログ ファイルへのリンクが表示されます。 ウィザードを閉じるには、 **[閉じる]** をクリックします。  
  
11. [完了] ページにインストールの概要ログ ファイルへのリンクと、その他の重要な注意事項が表示されます。  
  
12. コンピューターの再起動を求めるメッセージが表示されたら、再起動してください。 セットアップが完了した時点で、インストール ウィザードによるメッセージを確認することが重要です。 セットアップ ログ ファイルの詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。  
  
13. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]からアップグレードした場合は、アップグレード済みの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスを使用する前に、追加の手順を実行する必要があります。  
  
    -   Windows SCM で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを有効にします。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントを準備します。  
  
 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]からアップグレードした場合は、上記の手順に加えて次の手順の実行が必要になる場合があります。  
  
-   [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] で準備されたユーザーは、アップグレード後も準備された状態のままです。 具体的には、BUILTIN\Users グループが準備されたままになります。 必要に応じて、これらのアカウントの無効化、削除、または再設定を実行します。 詳細については、「 [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
-   tempdb システム データベースおよび model システム データベースのサイズと復旧モードはアップグレード後も変更されません。 必要に応じて、これらの設定を再構成します。 詳細については、「[システム データベースのバックアップと復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)」を参照してください。  
  
-   テンプレート データベースはアップグレード後もコンピューター上に残ります。  
  
## <a name="see-also"></a>参照  
 [SQL Server のアップグレード](../../database-engine/install-windows/upgrade-sql-server.md)   
 [旧バージョンとの互換性_削除](https://msdn.microsoft.com/library/15d9117e-e2fa-4985-99ea-66a117c1e9fd)  
  
  
