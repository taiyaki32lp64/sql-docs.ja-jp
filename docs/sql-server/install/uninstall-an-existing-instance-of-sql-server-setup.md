---
title: SQL Server の既存のインスタンスのアンインストール (セットアップ) | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- removing instances of SQL Server
- uninstalling instances of SQL Server
- removing SQL Server
- instances of SQL Server, uninstalling
- uninstalling SQL Server
ms.assetid: 3c64b29d-61d7-4b86-961c-0de62261c6a1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 16c406052b563accdc2cd98fd629909cce38e0ce
ms.sourcegitcommit: 1c3f56deaa4c1ffbe5d7f75752ebe10447c3e7af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71251066"
---
# <a name="uninstall-an-existing-instance-of-sql-server-setup"></a>SQL Server の既存のインスタンスのアンインストール (セットアップ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  ここでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のスタンドアロン インスタンスをアンインストールする方法について説明します。 また、この記事の手順を実行してシステムを準備し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再インストールできるようにします。  
  
 > [!NOTE]
 > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターをアンインストールするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップによって提供されるノードの削除機能を使用して、各ノードを個別に削除します。 詳細については、「[SQL Server フェールオーバー クラスターでのノードの追加または削除 &#40;セットアップ&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)」を参照してください。  

## <a name="considerations"></a>考慮事項

- SQL Server をアンインストールするには、サービスとしてログオンする権限を持つローカル管理者である必要があります。 
- コンピューターに "*最低限*" 必要な量の物理メモリがある場合は、ページ ファイルのサイズを物理メモリの量の 2 倍に増やします。 仮想メモリが不足した状況では、SQL Server の削除が不完全になる場合があります。 
- SQL Server の複数のインスタンスがあるシステムでは、SQL Server の最後のインスタンスが削除されたときにのみ、SQL Server ブラウザー サービスがアンインストールされます。 SQL Server Browser サービスは、**コントロール パネル**の **[プログラムと機能]** から手動で削除できます。 
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をアンインストールすると、インストール プロセス中に追加された tempdb データ ファイルが削除されます。 tempdb_mssql_*.ndf という名前パターンのファイルがシステム データベース ディレクトリにある場合、そのファイルは削除されます。 
  

  
## <a name="prepare"></a>準備  
  
1.  **データのバックアップ。** システム データベースを含むすべてのデータベースの[完全バックアップ](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)を作成するか、.mdf ファイルと .ldf ファイルを別の場所に手動でコピーします。 **master** データベースには、ログインやスキーマなど、サーバーのシステム レベルの情報がすべて含まれています。 **msdb** データベースには、SQL Server エージェント ジョブ、バックアップ履歴、メンテナンス プランなどのジョブ情報が含まれています。 システム データベースの詳細については、[システム データベース](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)に関するページを参照してください。 
  
    保存する必要のあるファイルには、次のデータベース ファイルがあります。  

    |             |            |           |            |
    | :---------- | :--------- |:--------- | :--------- |
    | master.mdf  | mastlog.ldf| model.mdf | modellog.ldf| 
    | msdbdata.mdf| msdblog.ldf| Mssqlsystemresource.mdf | Mssqlsustemresource.ldf |
    | Tempdb.mdf | Templog.ldf|  ReportServer[$InstanceName] | ReportServer[$InstanceName]TempDB| 

    > [!NOTE]
    > ReportServer データベースは、SQL Server Reporting Services に含まれています。   

 
1.  **サービス** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **をすべて停止します。** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントをアンインストールする前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスをすべて停止することをお勧めします。 アクティブな接続が存在すると、アンインストールに失敗する場合があるためです。  
  
1.  **適切な権限を持つアカウントの使用。** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントを使用するか、同等の権限を持つアカウントを使用して、サーバーにログオンします。 たとえば、ローカルの Administrators グループのメンバーであるアカウントを使用してサーバーにログオンできます。  
  
## <a name="uninstall"></a>アンインストール 

# <a name="windows-10--2016-tabwindows10"></a>[Windows 10 / 2016 以降](#tab/Windows10)

Windows 10、Windows Server 2016、Windows Server 2019 以降から SQL Server をアンインストールするには、次の手順に従います。 

1. 削除プロセスを開始するには、[スタート] メニューから **[設定]** に移動し、 **[アプリ]** を選択します。 
1. 検索ボックスで「`sql`」を検索します。 
1. **[Microsoft SQL Server (バージョン) (ビット)]** を選択します。 たとえば、`Microsoft SQL Server 2017 (64-bit)` のようになります。
1. **[アンインストール]** を選択します。
 
    ![SQL Server のアンインストール](media/uninstall-an-existing-instance-of-sql-server-setup/uninstall-sql-server-windows-10.png)

1. Microsoft SQL Server インストール ウィザードを起動するには、[SQL Server] ポップアップ ダイアログで **[削除]** を選択します。 

    ![SQL Server の削除](media/uninstall-an-existing-instance-of-sql-server-setup/remove-sql-2017.png)
  
1.  **[インスタンスの選択]** ページのドロップダウン ボックスを使用して、削除する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定するか、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の共有機能と管理ツールだけを削除するオプションを指定します。 続けるには、 **[次へ]** を選択します。  
  
1.  **[機能の選択]** ページで、指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスから削除する機能を指定します。  
  
1.  **[削除の準備完了]** ページで、アンインストールされるコンポーネントおよび機能の一覧を確認します。 **[削除]** をクリックしてアンインストールを開始します。  
 
1. **[アプリと機能]** ウィンドウを更新して、SQL Server インスタンスが正常に削除されたことを確認し、まだ存在している SQL Server コンポーネントを確認します。 このウィンドウからこれらのコンポーネントも削除します。その場合は選択します。 

# <a name="windows-2008---2012-r2tabwindows2012"></a>[Windows 2008 から 2012 R2](#tab/windows2012)

Windows Server 2008、Windows Server 2012、Windows 2012 R2 から SQL Server をアンインストールするには、次の手順に従います。 

1. 削除プロセスを開始するには、**コントロール パネル**に移動し、 **[プログラムと機能]** を選択します。
1. **[Microsoft SQL Server (バージョン) (ビット)]** を右クリックし、 **[アンインストール]** を選択します。 たとえば、`Microsoft SQL Server 2012 (64-bit)` のようになります。  
  
    ![SQL Server のアンインストール](media/uninstall-an-existing-instance-of-sql-server-setup/uninstall-sql-server-windows-2012.png)

1. Microsoft SQL Server インストール ウィザードを起動するには、[SQL Server] ポップアップ ダイアログで **[削除]** を選択します。 

    ![SQL Server の削除](media/uninstall-an-existing-instance-of-sql-server-setup/remove-sql-2012.png)
  
1.  **[インスタンスの選択]** ページのドロップダウン ボックスを使用して、削除する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定するか、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の共有機能と管理ツールだけを削除するオプションを指定します。 続けるには、 **[次へ]** を選択します。  
  
1.  **[機能の選択]** ページで、指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスから削除する機能を指定します。  
  
1.  **[削除の準備完了]** ページで、アンインストールされるコンポーネントおよび機能の一覧を確認します。 **[削除]** をクリックしてアンインストールを開始します。  
 
1. **[プログラムと機能]** ウィンドウを更新して、SQL Server インスタンスが正常に削除されたことを確認し、まだ存在している SQL Server コンポーネントを確認します。 このウィンドウからこれらのコンポーネントも削除します。その場合は選択します。 

---

  
## <a name="in-the-event-of-failure"></a>失敗した場合  

削除プロセスが失敗した場合は、[SQL Server セットアップ ログ ファイル](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)を確認して、根本的な原因を特定します。 

[セットアップ ログ ファイル内の SQL Server セットアップの問題を識別する方法](https://support.microsoft.com/kb/955396/en-us)に関するサポート技術情報の記事が調査に役立ちます。 これは SQL Server 2008 用ですが、説明されている方法は SQL Server のすべてのバージョンに適用できます。 

  
## <a name="see-also"></a>参照  
 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
