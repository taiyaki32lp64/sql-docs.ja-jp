---
title: SQL Server の既存のインスタンスのアンインストール (セットアップ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 484ef7dead58a6e8ae35639cdc6218d5c8223bd9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62990186"
---
# <a name="uninstall-an-existing-instance-of-sql-server-setup"></a>SQL Server の既存のインスタンスのアンインストール (セットアップ)
  ここでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のスタンドアロン インスタンスをアンインストールする方法について説明します。 また、このトピックの手順を実行してシステムを準備し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を再インストールできるようにします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスをアンインストールするには、サービスとしてログオンする権限を持つローカル管理者である必要があります。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターをアンインストールするには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップによって提供されるノードの削除機能を使用して、各ノードを個別に削除します。 詳細については、「[SQL Server フェールオーバー クラスターでのノードの追加または削除 &#40;セットアップ&#41;](../failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をアンインストールする前に、次の重要な情報について検討してください。  
  
-   必要最小限の物理メモリを搭載したコンピューターから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントを削除する場合、ページ ファイルのサイズが十分な大きさであることを確認してください。 ページ ファイルのサイズは、物理メモリの 2 倍である必要があります。 仮想メモリが不足した状況では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の削除が不完全になる場合があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを複数インストールしている場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser は [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の最後のインスタンスがアンインストールされるときに自動的にアンインストールされます。  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のすべてのコンポーネントをアンインストールするには、**コントロール パネル**の **[プログラムと機能]** を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser コンポーネントを手動でアンインストールする必要があります。  
  
### <a name="before-you-uninstall"></a>アンインストールする前に  
  
1.  **データのバックアップ。** これは必須の手順ではありませんが、現在の状態で保存しておく必要のあるデータベースが存在する場合に行います。 また、システム データベースに対して行った変更の保存が必要になることもあります。 どのような状況でも、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をアンインストールする前にデータを必ずバックアップしてください。 あるいは、MSSQL フォルダー以外のフォルダー内にあるすべてのデータとログ ファイルのコピーを保存してください。 MSSQL フォルダーはアンインストール中に削除されます。  
  
     保存する必要のあるファイルには、次のデータベース ファイルがあります。  
  
    -   Master.mdf  
  
    -   Mastlog.ldf  
  
    -   Model.mdf  
  
    -   Modellog.ldf  
  
    -   Msdbdata.mdf  
  
    -   Msdblog.ldf  
  
    -   Mssqlsystemresource.mdf  
  
    -   Mssqlsustemresource.ldf  
  
    -   Tempdb.mdf  
  
    -   Templog.ldf  
  
    -   `ReportServer[$InstanceName]` (これは、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]既定のデータベースです)。  
  
    -   ReportServer[$InstanceName]TempDB (これは [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の既定の一時データベースです)  
  
2.  **ローカル セキュリティ グループの削除。** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をアンインストールする前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントのローカル セキュリティ グループを削除します。  
  
3.  **サービス** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **をすべて停止します。** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントをアンインストールする前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスをすべて停止することをお勧めします。 アクティブな接続が存在すると、アンインストールに失敗する場合があるためです。  
  
4.  **適切な権限を持つアカウントの使用。** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントを使用するか、同等の権限を持つアカウントを使用して、サーバーにログオンします。 たとえば、ローカルの Administrators グループのメンバーであるアカウントを使用してサーバーにログオンできます。  
  
### <a name="to-uninstall-an-instance-of-includessnoversionincludesssnoversion-mdmd"></a>のインスタンスをアンインストールするには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  アンインストール プロセスを開始するには、 **コントロール パネル** で **[プログラムと機能]** をクリックします。  
  
2.  右クリックして **[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]** 選択**アンインストール**します。 次に、 **[削除]** をクリックします。 これにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードが起動します。  
  
     セットアップ サポート ルールが実行され、コンピューターの構成が確認されます。 続行するには、 **[次へ]** をクリックします。  
  
3.  [インスタンスの選択] ページのドロップダウン ボックスを使用して、削除する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定するか、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の共有機能と管理ツールだけを削除するオプションを指定します。 続行するには、 **[次へ]** をクリックします。  
  
4.  [機能の選択] ページで、指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスから削除する機能を指定します。  
  
     削除ルールが実行され、操作を正常に完了できることが確認されます。  
  
5.  **[削除の準備完了]** ページで、アンインストールされるコンポーネントおよび機能の一覧を確認します。 **[削除]** をクリックしてアンインストールを開始します。  
  
6.  最後の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスをアンインストールした直後は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に関連付けられたその他のプログラムがまだ **[プログラムと機能]** のプログラムの一覧に表示されています。 ただし、 **[プログラムと機能]** を閉じ、次に **[プログラムと機能]** を開いたときには、プログラムの一覧は更新され、実際にインストールされているプログラムのみが表示されます。  
  
### <a name="if-the-uninstallation-fails"></a>アンインストールが失敗した場合  
  
1.  アンインストール プロセスが正常に完了しない場合は、アンインストールが失敗した原因となる問題の解決を試みます。 アンインストールの失敗の原因を把握するには、次の記事が役立ちます。  
  
    -   [セットアップ ログ ファイルで SQL Server 2008 のセットアップの問題を特定する方法](https://support.microsoft.com/kb/955396/en-us)  
  
    -   [SQL Server セットアップ ログ ファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
2.  アンインストールが失敗した原因を解決できない場合は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポートに問い合わせてください。 重要なファイルを誤って削除した場合など、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再インストールする前に、オペレーティング システムの再インストールが必要になる場合もあります。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
