---
title: SQL Server フェールオーバー クラスターでのノードの追加または削除 (セットアップ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- adding nodes
- nodes [Faillover Clustering], removing
- nodes [Faillover Clustering], adding
- failover clustering [SQL Server], nodes
- deleting nodes
- cluster maintenance [SQL Server]
- removing nodes
ms.assetid: fe20dca9-a4c1-4d32-813d-42f1782dfdd3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1b6298020c1aa39f2c5c319efa492f6832c301f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63190281"
---
# <a name="add-or-remove-nodes-in-a-sql-server-failover-cluster-setup"></a>SQL Server フェールオーバー クラスターでのノードの追加または削除 (セットアップ)
  次の手順を使用すると、既存の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスでノードを管理できます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターを更新または削除するには、フェールオーバー クラスターのすべてのノードでサービスとしてログインする権限を持つローカル管理者である必要があります。 ローカル インストールの場合は、セットアップを管理者として実行する必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をリモート共有からインストールする場合は、そのリモート共有に対する読み取り権限と実行権限を持つドメイン アカウントを使用する必要があります。  
  
 既存の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターにノードを追加するには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスに追加するノードで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを実行する必要があります。 セットアップは、アクティブなノードでは実行しないでください。  
  
 既存の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターからノードを削除するには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスから削除するノードで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを実行する必要があります。  
  
 ノードを追加または削除するための手順を表示するには、次のいずれかの操作を選択します。  
  
-   [既存の SQL Server フェールオーバー クラスターにノードを追加する](#Add)  
  
-   [既存の SQL Server フェールオーバー クラスターからノードを削除する](#Remove)  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストール場所に使用されているオペレーティング システムのドライブ文字は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターに追加されるすべてのノードで一致している必要があります。  
  
##  <a name="Add"></a> ノードの追加  
  
#### <a name="to-add-a-node-to-an-existing-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>既存の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターにノードを追加するには  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インストール メディアを挿入し、ルート フォルダーの Setup.exe をダブルクリックします。 ネットワーク共有からインストールするには、ネットワーク共有上のルート フォルダーに移動し、Setup.exe をダブルクリックします。  
  
2.  インストール ウィザードによって [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インストール センターが起動されます。 既存のフェールオーバー クラスター インスタンスにノードを追加するには、左側のペインで **[インストール]** をクリックします。 次に、 **[[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターにノードを追加します]** を選択します。  
  
3.  システム構成チェッカーにより、コンピューターで検出処理が実行されます。 続行するには、 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  ローカライズされたオペレーティング システムでのインストールで、インストール メディアに英語とそのオペレーティング システムに対応する言語の両方の言語パックが含まれている場合は、[言語の選択] ページで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの言語を指定できます。 言語間サポートとインストールに関する注意点の詳細については、「 [SQL Server のローカル言語版](../../install/local-language-versions-in-sql-server.md)」を参照してください。  
  
     続行するには、 **[次へ]** をクリックします。  
  
5.  [プロダクト キー] ページで、SQL Server の製品版の PID キーを指定します。 このインストールで入力するプロダクト キーは、アクティブ ノードにインストールされている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エディションのプロダクト キーと同じにする必要があります。  
  
6.  [ライセンス条項] ページで使用許諾契約書を読み、使用許諾条件に同意する場合は対応するチェック ボックスをオンにします。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の機能向上に役立てるため、機能の使用状況オプションを有効にしてレポートを [!INCLUDE[msCoName](../../../includes/msconame-md.md)]に送信することもできます。 続行するには、 **[次へ]** をクリックします。 セットアップを終了するには、 **[キャンセル]** をクリックします。  
  
7.  セットアップを続行する前に、システム構成チェッカーによってコンピューターのシステムの状態が確認されます。 確認が完了したら、 **[次へ]** をクリックして続行します。  
  
8.  [クラスター ノードの構成] ページで、ドロップダウン ボックスを使用して、このセットアップ操作で変更する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスの名前を指定します。  
  
9. [サーバーの構成 - サービス アカウント] ページで、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスのログイン アカウントを指定します。 このページで構成する実際のサービスは、インストール時に選択した機能によって異なります。 フェールオーバー クラスターのインストールでは、アクティブ ノードに指定された設定に基づいて、アカウント名とスタートアップの種類に関する情報がこのページにあらかじめ設定されます。 各アカウントのパスワードを入力する必要があります。 詳細については、「 [サーバーの構成 - サービス アカウント](../../install/server-configuration-service-accounts.md) 」および「 [Windows サービス アカウントと権限の構成](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
     **セキュリティに関する注意** [!INCLUDE[ssNoteStrongPass](../../../includes/ssnotestrongpass-md.md)]  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスのログイン情報を指定したら、 **[次へ]** をクリックします。  
  
10. [レポート] ページで、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] に送信する、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の強化に役立つ情報を指定します。 既定では、エラー レポートのオプションは有効になっています。  
  
11. システム構成チェッカーによって別のルール セットが実行され、コンピューターの構成と指定した [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能が検証されます。  
  
12. [ノード追加の準備完了] ページには、セットアップで指定したインストール オプションのツリー ビューが表示されます。  
  
13. セットアップの進行に合わせてインストールの進行状況を監視できるように、[ノード追加の進行状況] ページに状態が表示されます。  
  
14. インストールが終了すると、[完了] ページにインストールの概要ログ ファイルへのリンクと、その他の重要な注意事項が表示されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストール プロセスを完了するには、 **[閉じる]** をクリックします。  
  
15. コンピューターの再起動を求めるメッセージが表示されたら、再起動してください。 セットアップが完了した時点で、インストール ウィザードによるメッセージを確認することが重要です。 セットアップ ログ ファイルの詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。  
  
##  <a name="Remove"></a> ノードの削除  
  
#### <a name="to-remove-a-node-from-an-existing-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>既存の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターからノードを削除するには  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストール メディアを挿入します。 ルート フォルダーの setup.exe をダブルクリックします。 ネットワーク共有からインストールするには、ネットワーク共有上のルート フォルダーに移動し、Setup.exe をダブルクリックします。  
  
2.  インストール ウィザードによって、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インストール センターが起動されます。 既存のフェールオーバー クラスター インスタンスからノードを削除するには、左側のペインで **[メンテナンス]** をクリックし、 **[[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターからノードを削除します]** をクリックします。  
  
3.  システム構成チェッカーにより、コンピューターで検出処理が実行されます。 続行するには、 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  [セットアップ サポート ファイル] ページで [インストール] をクリックすると、セットアップを続行する前に、システム構成チェッカーによってコンピューターのシステムの状態が確認されます。 確認が完了したら、 **[次へ]** をクリックして続行します。  
  
5.  [クラスター ノードの構成] ページで、ドロップダウン ボックスを使用して、このセットアップ操作で変更する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスの名前を指定します。 削除されるノードが **"このノードの名前"** フィールドに一覧表示されます。  
  
6.  [ノード削除の準備完了] ページには、セットアップで指定したオプションのツリー ビューが表示されます。 続行するには、 **[削除]** をクリックします。  
  
7.  削除の操作中に、[ノード削除の進行状況] ページに状態が表示されます。  
  
8.  [完了] ページにノード削除操作の概要ログ ファイルへのリンクと、その他の重要な注意事項が表示されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のノード削除を完了するには、 **[閉じる]** をクリックします。 セットアップ ログ ファイルの詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
