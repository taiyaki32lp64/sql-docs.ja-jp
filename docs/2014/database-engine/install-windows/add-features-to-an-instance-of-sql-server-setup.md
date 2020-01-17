---
title: SQL Server 2014 (セットアップ) のインスタンスに機能の追加 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- feature adding [SQL Server]
- SQL Server, features
- adding features to SQL Server
ms.assetid: 97931fdc-d943-48dd-81b9-ae8b8d2c6dad
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 147fe717919035c365ef2e3507e46a4323694570
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779373"
---
# <a name="add-features-to-an-instance-of-sql-server-2014-setup"></a>SQL Server 2014 のインスタンスへの機能の追加 (セットアップ)
  ここでは、機能を [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のインスタンスに追加する手順について詳しく説明します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のコンポーネントまたはサービスには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに固有のものがあります。 これらは、インスタンス対応とも呼ばれます。 また、これらをホストしているインスタンスとバージョンが同じで、そのインスタンスにのみ使用されます。 インスタンス対応のコンポーネントがまだインストールされていない場合は、共有コンポーネントと共に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスに追加できます。 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。  
  
 インスタンスに機能を追加する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、コマンド プロンプトから次を参照してください。[コマンド プロンプトから SQL Server 2014 のインストール](install-sql-server-from-the-command-prompt.md)します。  
  
## <a name="prerequisites"></a>前提条件  
 続行する前に、「 [SQL Server のインストール計画](../../sql-server/install/planning-a-sql-server-installation.md)」のトピックを参照してください。  
  
> [!NOTE]  
>  ローカル インストールの場合は、セットアップを管理者として実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をリモート共有からインストールする場合は、そのリモート共有に対する読み取り権限を持つドメイン アカウントを使用する必要があります。  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインスタンスに機能を追加する場合、新しく追加した機能には既存の使用状況レポートの設定が適用されます。 これらの設定を変更するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **[構成ツール]** メニューにある **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][ エラーと使用状況レポート]** ツールを使用します。  
  
## <a name="procedures"></a>手順  
  
#### <a name="to-add-features-to-an-instance-of-includesscurrentincludessscurrent-mdmd"></a>コマンド プロンプトから [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール メディアを挿入します。 ルート フォルダーの setup.exe をダブルクリックします。 ネットワーク共有からインストールするには、ネットワーク共有上のルート フォルダーに移動し、setup.exe をダブルクリックします。 [ [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] セットアップ] ダイアログ ボックスが表示されます。必須コンポーネントをインストールする場合は [!INCLUDE[clickOK](../../includes/clickok-md.md)] **をインストールしない場合は** [キャンセル] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] をクリックします。  
  
2.  インストール ウィザードによって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール センターが起動されます。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の既存のインスタンスに新しい機能を追加するには、左側のナビゲーション領域の **[インストール]** をクリックし、[**新規[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スタンドアロン インストールを実行するか、既存のインストールに機能を追加します]** をクリックします。  
  
3.  システム構成チェッカーにより、コンピューターで検出処理が実行されます。 詳細を表示するには、 **[詳細の表示]** をクリックします。 続行するには、 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  [製品の更新プログラム] ページに、使用できる最新の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 製品の更新プログラムが表示されます。 更新プログラムを含めない場合は、 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [製品の更新プログラムを含める]** チェック ボックスをオフにします。 製品の更新プログラムが検出されない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップではこのページは表示されず、 **[セットアップ ファイルのインストール]** ページに自動的に移動します。  
  
5.  [セットアップ ファイルのインストール] ページのセットアップには、セットアップ ファイルのダウンロード、抽出、およびインストールの進行状況が表示されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップの更新プログラムが検出され、含まれるように指定されている場合は、その更新プログラムもインストールされます。 セットアップ サポート ファイルをインストールするには、 **[インストール]** をクリックします。  
  
6.  セットアップを続行する前に、システム構成チェッカーによってコンピューターのシステムの状態が確認されます。  
  
7.  [インストールの種類] ページで、 **[既存の [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インスタンスに機能を追加する]** オプションを選択し、更新するインスタンスを選択します。  
  
8.  [機能の選択] ページで、インストールするコンポーネントを選択します。 機能名を選択すると、右側のウィンドウに各コンポーネント グループの説明が表示されます。 チェック ボックスはいくつでもオンにできます。 詳細については、次を参照してください。[エディションと SQL Server 2014 のコンポーネントの](../../sql-server/editions-and-components-of-sql-server-2016.md)します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の特定のインスタンスに各コンポーネントをインストールできるのは、一度だけです。 複数のコンポーネントをインストールするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の追加のインスタンスをインストールする必要があります。  
  
     選択した機能の必須コンポーネントが、右側のペインに表示されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、この手順の後半で説明するインストール手順の間に、まだインストールされていない必須コンポーネントをインストールします。  
  
     セットアップを続行する前に、システム構成チェッカーによってコンピューターのシステムの状態が確認されます。 **[次へ]** をクリックして次に進みます。  
  
9. [必要なディスク領域] ページでは、指定した機能に必要なディスク領域が計算され、セットアップを実行中のコンピューター上の空き領域と比較されます。  
  
10. このトピックの残りの部分のワーク フローは、インストールするように指定した機能によって異なります。 選択した機能によっては、表示されないページもあります。  
  
11. [サーバーの構成 - サービス アカウント] ページで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスのログイン アカウントを指定します。 このページで構成する実際のサービスは、インストール時に選択した機能によって異なります。  
  
     すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスに同じログイン アカウントを割り当てることも、各サービス アカウントを個々に構成することもできます。 サービスを自動的に開始するか、手動で開始するか、または無効にするかを指定することもできます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 各サービスに最小の権限を与えるためにはサービス アカウントを個別に構成することをお勧めします。サービス アカウントを個別に構成すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスには、サービスでのタスクの実行に必要な最小権限が付与されます。 詳細については、「 [サーバー構成 - サービス アカウント](../../sql-server/install/server-configuration-service-accounts.md) 」および「 [Windows サービス アカウントと権限の構成](../configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のこのインスタンスに含まれるすべてのサービス アカウントに同じログイン アカウントを指定する場合は、ページの下部にあるフィールドに資格情報を指定します。  
  
     **セキュリティに関する注意** : [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスのログイン情報を指定したら、 **[次へ]** をクリックします。  
  
12. **[サーバーの構成 - 照合順序]** タブを使用して、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] および [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]に既定以外の照合順序を指定します。 詳細については、「 [サーバー構成 - 照会順序](../../sql-server/install/server-configuration-collation.md)」を参照してください。  
  
13. [!INCLUDE[ssDE](../../includes/ssde-md.md)] [の構成 - アカウントの準備] ページを使用して、次の項目を指定します。  
  
    -   [セキュリティ モード] - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス用に Windows 認証または混合モード認証を選択します。 混合モード認証を選択した場合は、組み込みの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者アカウントの強力なパスワードを入力する必要があります。  
  
         デバイスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]との接続を正常に確立した後のセキュリティ メカニズムは Windows 認証モード、混合モードのどちらの場合も同じです。 詳細については、次を参照してください。[データベース エンジンの構成 - アカウントのプロビジョニング](../../sql-server/install/database-engine-configuration-account-provisioning.md)します。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [管理者] - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの 1 人以上のシステム管理者を指定する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを実行しているアカウントを追加するには、 **[現在のユーザーの追加]** をクリックします。 システム管理者の一覧に対してアカウントを追加または削除するには、 **[追加]** または **[削除]** をクリックし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスについて管理者特権を持っているユーザー、グループ、またはコンピューターの一覧を編集します。 詳細については、次を参照してください。[データベース エンジンの構成 - アカウントのプロビジョニング](../../sql-server/install/database-engine-configuration-account-provisioning.md)します。  
  
     一覧の編集が完了したら、 **[OK]** をクリックします。 構成ダイアログ ボックスの管理者の一覧を確認します。 一覧が完成したら、 **[次へ]** をクリックします。  
  
14. [!INCLUDE[ssDE](../../includes/ssde-md.md)] [の構成 - データ ディレクトリ] ページを使用して、既定以外のインストール ディレクトリを指定します。 既定のディレクトリにインストールする場合は、 **[次へ]** をクリックします。  
  
    > [!IMPORTANT]  
    >  既定以外のインストール ディレクトリを指定する場合は、インストール フォルダーがこの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の他のインスタンスのディレクトリと共有できません。  
  
     詳細については、「 [データベース エンジンの構成 - データ ディレクトリ](../../sql-server/install/database-engine-configuration-data-directories.md)」を参照してください。  
  
15. [!INCLUDE[ssDE](../../includes/ssde-md.md)][の構成 - FILESTREAM] ページを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対する FILESTREAM を有効にします。 FILESTREAM の詳細については、「 [データベース エンジンの構成 - Filestream](../../sql-server/install/database-engine-configuration-filestream.md)」を参照してください。 続行するには、[次へ] をクリックします。  
  
16. [[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の構成 - アカウントの準備] ページを使用して、サーバー モードと [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の管理者権限を持つユーザーまたはアカウントを指定します。 サーバー モードによって、サーバーで使用されるメモリとストレージ サブシステムが決まります。 サーバー モードによって、実行されるソリューションの種類も異なります。 サーバーで多次元キューブ データベースを実行する場合は、既定の [多次元データおよびデータ マイニング] サーバー モード オプションを選択します。 管理者権限に関しては、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のシステム管理者を少なくとも 1 人指定する必要があります。 SQL Server セットアップを実行しているアカウントを追加するには、 **[現在のユーザーの追加]** をクリックします。 システム管理者の一覧に対してアカウントを追加または削除するには、 **[追加]** または **[削除]** をクリックし、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]の管理者権限を持つユーザー、グループ、またはコンピューターの一覧を編集します。 サーバー モードと管理者権限の詳細については、「 [Analysis Services の構成 - アカウントの準備](../../sql-server/install/analysis-services-configuration-account-provisioning.md)」を参照してください。  
  
     一覧の編集が完了したら、 **[OK]** をクリックします。 構成ダイアログ ボックスの管理者の一覧を確認します。 一覧が完成したら、 **[次へ]** をクリックします。  
  
17. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] [の構成 - データ ディレクトリ] ページを使用して、既定以外のインストール ディレクトリを指定します。 既定のディレクトリにインストールする場合は、 **[次へ]** をクリックします。  
  
    > [!IMPORTANT]  
    >  既定以外のインストール ディレクトリを指定する場合は、インストール フォルダーがこの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の他のインスタンスのディレクトリと共有できません。  
  
     詳細については、「 [Analysis Service の構成 - データ ディレクトリ](../../sql-server/install/analysis-services-configuration-data-directories.md)」を参照してください。  
  
18. 作成する [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インストールの種類を指定するには、[[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の構成] ページを使用します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成モードの詳細については、「[Reporting Services 構成オプション &#40;SSRS&#41;](../../sql-server/install/reporting-services-configuration-options-ssrs.md)」を参照してください。  
  
19. [分散再生コントローラーの構成] ページを使用して、分散再生コントローラー サービスに対する管理権限を付与するユーザーを指定します。 管理権限を持つユーザーには、分散再生コントローラー サービスへの無制限のアクセス許可が与えられます。  
  
     分散再生コントローラー サービスに対するアクセス許可を付与するユーザーを追加するには、 **[現在のユーザーの追加]** をクリックします。 分散再生コントローラー サービスのアクセス許可を追加するには、 **[追加]** をクリックします。 Distributed Replay Controller サービスからアクセス許可を削除するには、 **[削除]** をクリックします。  
  
     続行するには、 **[次へ]** をクリックします。  
  
20. [分散再生クライアントの構成] ページを使用して、分散再生クライアント サービスに対する管理権限を付与するユーザーを指定します。 管理権限を持つユーザーには、分散再生クライアント サービスへの無制限のアクセス許可が与えられます。  
  
     **[コントローラー名]** は、省略可能なパラメーターで、既定値は \<*blank*> です。 分散再生クライアント サービスと通信するクライアント コンピューターであるコントローラーの名前を入力します。 次のことを考慮してください。  
  
    -   コントローラーを既にセットアップしてある場合は、各クライアントを構成するときにコントローラーの名前を入力します。  
  
    -   コントローラーをまだセットアップしていない場合は、コントローラー名を空白にしておくことができます。 ただし、コントローラー名を **クライアント構成** ファイルに手動で入力する必要があります。  
  
     分散再生クライアント サービス用の **[作業ディレクトリ]** を指定します。 既定の作業ディレクトリは、\<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\ です。  
  
     分散再生クライアント サービス用の **[結果ディレクトリ]** を指定します。 既定の結果ディレクトリは、\<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\ です。  
  
     続行するには、 **[次へ]** をクリックします。  
  
21. [エラー レポート] ページで、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] に送信する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の改善に役立つ情報を指定します。 既定では、エラー レポートのオプションは有効になっています。  
  
22. システム構成チェッカーによって別のルール セットが実行され、コンピューターの構成と指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能が検証されます。  
  
23. [インストールの準備完了] ページには、セットアップで指定したインストール オプションのツリー ビューが表示されます。 このページで、セットアップは製品の更新プログラム機能が有効/無効であるか、および最終バージョンの更新プログラムであるかどうかを示します。 [インストール] をクリックすると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップは、選択した機能の必須コンポーネントを最初にインストールした後に、機能をインストールします。  
  
24. インストール中は、セットアップの進行に合わせてインストールの進行状況を監視できるように、[インストールの進行状況] ページに状態が表示されます。  
  
25. インストールが終了すると、[完了] ページにインストールの概要ログ ファイルへのリンクと、その他の重要な注意事項が表示されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール プロセスを完了するには、 **[閉じる]** をクリックします。  
  
26. コンピューターの再起動を求めるメッセージが表示されたら、再起動してください。 セットアップが完了した時点で、インストール ウィザードによるメッセージを確認することが重要です。 セットアップ ログ ファイルの詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](view-and-read-sql-server-setup-log-files.md)」を参照してください。  
  
## <a name="next-steps"></a>次の手順  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストールを構成します。  
  
-   システムのセキュリティを向上するため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、主要なサービスと機能を個別にインストールし、アクティブ化できるようになっています。 詳細については、「 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server セットアップ ログ ファイルの表示と読み取り](view-and-read-sql-server-setup-log-files.md)   
 [SQL Server のインストールの検証](validate-a-sql-server-installation.md)   
 [SQL Server 2014 のインストールを削除します。](repair-a-failed-sql-server-installation.md)   
 [アップグレードする SQL Server 2014 のインストール ウィザードを使用して&#40;セットアップ&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [コマンド プロンプトからの SQL Server 2014 のインストール](install-sql-server-from-the-command-prompt.md)  
  
  
