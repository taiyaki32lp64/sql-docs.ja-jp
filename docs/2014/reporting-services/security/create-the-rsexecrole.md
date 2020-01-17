---
title: RSExecRole を作成する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- RSExecRole
ms.assetid: 7ac17341-df7e-4401-870e-652caa2859c0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3a6bc5ecbd1c59a5dc03f9c28d36d2816e6a8d92
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102028"
---
# <a name="create-the-rsexecrole"></a>RSExecRole を作成する
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] では、`RSExecRole` と呼ばれる定義済みのデータベース ロールを使用して、レポート サーバー データベースに対するレポート サーバーの権限が付与されます。 `RSExecRole`ロールは、レポート サーバー データベースで自動的に作成されます。 原則として、このロールを変更したり、他のユーザーをこのロールに割り当てたりすることはできません。 ただし、レポート サーバー データベースを新規または別の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../../includes/ssde-md.md)]に移動した場合は、master および MSDB システム データベースでロールを再作成する必要があります。  
  
 ここで説明する手順に従って、次の操作を実行します。  
  
-   master システム データベースでの `RSExecRole` の作成と準備  
  
-   MSDB システム データベースでの `RSExecRole` の作成と準備  
  
> [!NOTE]  
>  ここで説明する手順は、レポート サーバー データベースを準備する方法としてスクリプトの実行や WMI コードの作成を考えていないユーザーを対象としています。 大規模な配置を管理していて、データベースを定期的に移動する予定がある場合は、上記の操作を自動的に実行するスクリプトを作成する必要があります。 詳細については、「 [Reporting Service WMI プロバイダーへのアクセス](../tools/access-the-reporting-services-wmi-provider.md)」を参照してください。  
  
## <a name="before-you-start"></a>開始前の準備  
  
-   データベースを移動した後に復元できるように、暗号化キーをバックアップします。 この手順は `RSExecRole` の作成と準備には直接影響しませんが、作業を確認するためにはキーのバックアップが必要です。 詳細については、「 [Back Up and Restore Reporting Services Encryption Keys](../install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)」を参照してください。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスでの `sysadmin` 権限を持つユーザー アカウントでログオンしていることを確認します。  
  
-   使用する予定の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに [!INCLUDE[ssDE](../../../includes/ssde-md.md)] エージェント サービスがインストールされ、実行されていることを確認します。  
  
-   reportservertempdb および reportserver データベースをアタッチします。 実際のロールを作成するためにデータベースをアタッチする必要はありませんが、作業を確認する場合は事前にデータベースをアタッチする必要があります。  
  
 `RSExecRole` を手動で作成する手順は、レポート サーバー インストールの移行というコンテキストで使用されることを目的としています。 レポート サーバー データベースのバックアップや移動などの重要なタスクは、このトピックでは取り上げませんが、データベース エンジンのドキュメントで説明されています。  
  
## <a name="create-rsexecrole-in-master"></a>master での RSExecRole の作成  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] では、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント サービスの拡張ストアド プロシージャを使用して、スケジュールされた操作をサポートします。 次の手順では、プロシージャの実行権限を `RSExecRole` ロールに付与する方法について説明します。  
  
#### <a name="to-create-rsexecrole-in-the-master-system-database-using-management-studio"></a>Management Studio を使用して master システム データベースに RSExecRole を作成するには  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を起動し、レポート サーバー データベースをホストする [!INCLUDE[ssDE](../../../includes/ssde-md.md)] インスタンスに接続します。  
  
2.  **[データベース]** を開きます。  
  
3.  **[システム データベース]** を開きます。  
  
4.  `Master`を開きます。  
  
5.  **[セキュリティ]** を開きます。  
  
6.  **[ロール]** を開きます。  
  
7.  **[データベース ロール]** を右クリックして **[新しいデータベース ロール]** をクリックします。 [全般] ページが表示されます。  
  
8.  **ロール名**、型`RSExecRole`します。  
  
9. **[所有者]** に「 **DBO**」と入力します。  
  
10. **[セキュリティ保護可能なリソース]** をクリックします。  
  
11. **[検索]** をクリックします。 **[オブジェクトの追加]** ダイアログ ボックスが表示されます。 既定では、 **[特定のオブジェクト]** オプションが選択されています。  
  
12. **[OK]** をクリックします。 **[オブジェクトの選択]** ダイアログ ボックスが表示されます。  
  
13. **[オブジェクトの種類]** をクリックします。  
  
14. **[拡張ストアド プロシージャ]** をクリックします。  
  
15. **[OK]** をクリックします。  
  
16. **[参照]** をクリックします。  
  
17. 拡張ストアド プロシージャの一覧を下にスクロールし、以下を選択します。  
  
    1.  xp_sqlagent_enum_jobs  
  
    2.  xp_sqlagent_is_starting  
  
    3.  xp_sqlagent_notify  
  
18. **[OK]** をクリックし、もう一度 **[OK]** をクリックします。  
  
19. **[実行]** 行の **[許可]** 列で、チェック ボックスをオンにし、 **[OK]** をクリックします。  
  
20. 残りの各ストアド プロシージャに同じ操作を繰り返します。 `RSExecRole` には、3 つのストアド プロシージャすべてに対する実行権限を付与する必要があります。  
  
 ![データベース ロールのプロパティ ページ](../media/rsexecroledbproperties.gif "データベース ロールのプロパティ ページ")  
  
## <a name="create-rsexecrole-in-msdb"></a>MSDB での RSExecRole の作成  
 Reporting Services は、スケジュールされた操作をサポートするために、SQL Server エージェント サービスのストアド プロシージャを使用し、システム テーブルからジョブ情報を取得します。 次の手順では、プロシージャに対する実行権限およびテーブルでの選択権限を RSExecRole に付与する方法を説明します。  
  
#### <a name="to-create-rsexecrole-in-the-msdb-system-database"></a>MSDB システム データベースで RSExecRole を作成するには  
  
1.  MSDB のストアド プロシージャとテーブルに対する権限を付与する場合は、同様の手順を繰り返します。 手順を簡素化するために、ストアド プロシージャとテーブルを別々に準備します。  
  
2.  `MSDB`を開きます。  
  
3.  **[セキュリティ]** を開きます。  
  
4.  **[ロール]** を開きます。  
  
5.  **[データベース ロール]** を右クリックして **[新しいデータベース ロール]** をクリックします。 [全般] ページが表示されます。  
  
6.  ロール名 に入力`RSExecRole`します。  
  
7.  [所有者] に「 **DBO**」と入力します。  
  
8.  **[セキュリティ保護可能なリソース]** をクリックします。  
  
9. **[追加]** をクリックします。 **[オブジェクトの追加]** ダイアログ ボックスが表示されます。 **[オブジェクトの指定]** オプションが既定で選択されます。  
  
10. **[OK]** をクリックします。  
  
11. **[オブジェクトの種類]** をクリックします。  
  
12. **[ストアド プロシージャ]** をクリックします。  
  
13. **[OK]** をクリックします。  
  
14. **[参照]** をクリックします。  
  
15. 項目の一覧を下にスクロールし、以下を選択します。  
  
    1.  sp_add_category  
  
    2.  sp_add_job  
  
    3.  sp_add_jobschedule  
  
    4.  sp_add_jobserver  
  
    5.  sp_add_jobstep  
  
    6.  sp_delete_job  
  
    7.  sp_help_category  
  
    8.  sp_help_job  
  
    9. sp_help_jobschedule  
  
    10. sp_verify_job_identifiers  
  
16. **[OK]** をクリックし、もう一度 **[OK]** をクリックします。  
  
17. 最初のストアド プロシージャ sp_add_category を選択します。  
  
18. **[実行]** 行の **[許可]** 列で、チェック ボックスをオンにし、 **[OK]** をクリックします。  
  
19. 残りの各ストアド プロシージャに同じ操作を繰り返します。 RSExecRole には、10 個のストアド プロシージャすべてに対する実行権限を付与する必要があります。  
  
20. [セキュリティ保護可能なリソース] タブで、もう一度 **[追加]** をクリックします。 **[オブジェクトの追加]** ダイアログ ボックスが表示されます。 **[オブジェクトの指定]** オプションが既定で選択されます。  
  
21. **[OK]** をクリックします。  
  
22. **[オブジェクトの種類]** をクリックします。  
  
23. **[テーブル]** をクリックします。  
  
24. **[OK]** をクリックします。  
  
25. **[参照]** をクリックします。  
  
26. 項目の一覧を下にスクロールし、以下を選択します。  
  
    1.  syscategories  
  
    2.  sysjobs  
  
27. **[OK]** をクリックし、もう一度 **[OK]** をクリックします。  
  
28. 最初のテーブル syscategories を選択します。  
  
29. **[選択]** 行の **[許可]** 列で、チェック ボックスをオンにし、 **[OK]** をクリックします。  
  
30. sysjobs テーブルに同じ操作を繰り返します。 RSExecRole には、両方のテーブルに対する選択権限を付与する必要があります。  
  
## <a name="move-the-report-server-database"></a>レポート サーバー データベースの移動  
 ロールを作成したら、レポート サーバー データベースを新しい SQL Server インスタンスに移動できます。 詳細については、「[別のコンピューターへのレポート サーバー データベースの移動 &#40;SSRS ネイティブ モード&#41;](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)」を参照してください。  
  
 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] を [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]にアップグレードする場合、そのアップグレードはデータベースを移動する前と後のどちらでも実行できます。  
  
 レポート サーバー データベースは、レポート サーバーがそのデータベースに接続するときに、自動的に [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] へとアップグレードされます。 データベースをアップグレードするために特定の手順を実行する必要はありません。  
  
## <a name="restore-encryption-keys-and-verify-your-work"></a>暗号化キーの復元と作業の確認  
 レポート サーバー データベースをアタッチしたら、次の手順を実行して作業を確認します。  
  
#### <a name="to-verify-report-server-operability-after-a-database-move"></a>データベース移動後にレポート サーバーの運用性を確認するには  
  
1.  Reporting Services 構成ツールを起動して、レポート サーバーに接続します。  
  
2.  **[データベース]** をクリックします。  
  
3.  **[データベースの変更]** をクリックします。  
  
4.  **[既存のレポート サーバー データベースを選択する]** をクリックします。  
  
5.  データベース エンジンのサーバー名を入力します。 レポート サーバー データベースを名前付きインスタンスにアタッチした場合は、\<サーバー名>\\<インスタンス名\> の形式でインスタンス名を入力する必要があります。  
  
6.  **[接続テスト]** をクリックします。  
  
7.  **[次へ]** をクリックします。  
  
8.  [データベース] で、レポート サーバー データベースを選択します。  
  
9. **[次へ]** をクリックし、ウィザードを終了します。  
  
10. **[暗号化キー]** をクリックします。  
  
11. **[復元]** をクリックします。  
  
12. レポート サーバー データベースに格納されている資格情報および接続情報の暗号化を解除するために使用される対称キーのバックアップ コピーが含まれている厳密な名前のキー ファイル (.snk) を選択します。  
  
13. パスワードを入力し、 **[OK]** をクリックします。  
  
14. **[レポート マネージャー URL]** をクリックします。  
  
15. レポート マネージャーを開くリンクをクリックします。 レポート サーバー データベースのレポート サーバー アイテムが表示されます。  
  
## <a name="see-also"></a>参照  
 [別のコンピューターへのレポート サーバー データベースの移動 (SSRS ネイティブ モード)](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)   
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [ネイティブ モード レポート サーバー データベースの作成 &#40;SSRS 構成マネージャー&#41;](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Back Up and Restore Reporting Services Encryption Keys](../install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
  
  
