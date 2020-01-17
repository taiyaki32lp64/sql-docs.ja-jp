---
title: プライマリ ログ配布サーバーとセカンダリ ログ配布サーバー間でのロールの変更 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], role changes
- secondary data files [SQL Server], roles changed between
- primary databases [SQL Server]
- initial role changes [SQL Server]
- log shipping [SQL Server], failover
- failover [SQL Server], log shipping
ms.assetid: 2d7cc40a-47e8-4419-9b2b-7c69f700e806
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 08467118608db6b222bea2a41351eac951449a16
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774566"
---
# <a name="change-roles-between-primary-and-secondary-log-shipping-servers-sql-server"></a>プライマリ ログ配布サーバーとセカンダリ ログ配布サーバー間でのロールの変更 (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログ配布構成をセカンダリ サーバーにフェールオーバーした後、プリイマリ データベースとして機能するようにセカンダリ データベースを構成できます。 その後、プライマリ データベースとセカンダリ データベースを必要に応じて切り替えることができます。  
  
## <a name="performing-the-initial-role-change"></a>初期ロール切り替えの実行  
 初めてセカンダリ データベースにフェールオーバーし、これを新しいプライマリ データベースとして使用する場合は、次の一連の手順を実行する必要があります。 この初期手順を実行した後、プライマリ データベースとセカンダリ データベース間でロールを簡単に切り替えることができるようになります。  
  
1.  プライマリ データベースからセカンダリ データベースに手動でフェールオーバーします。 NORECOVERY 句を使用して、プライマリ サーバー上のアクティブなトランザクション ログを必ずバックアップしてください。 詳細については、「 [ログ配布のセカンダリへのフェールオーバー &#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)」を参照してください。  
  
2.  元のプライマリ サーバー上のログ配布バックアップ ジョブと、元のセカンダリ サーバー上のコピーおよび復元ジョブを無効にします。  
  
3.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、セカンダリ データベース (新しいプライマリにするデータベース) でログ配布を構成します。 詳細については、「 [ログ配布の構成 &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)で導入されました。 手順は次のとおりです。  
  
    1.  元のプライマリ サーバーについて作成したときと同じ共有を使用してバックアップを作成します。  
  
    2.  セカンダリ データベースを追加するときは、 **[セカンダリ データベースの設定]** ダイアログ ボックスの **[セカンダリ データベース]** ボックスに元のプライマリ データベースの名前を入力します。  
  
    3.  **[セカンダリ データベースの設定]** ダイアログ ボックスで、 **[いいえ、セカンダリ データベースは初期化されています]** を選択します。  
  
4.  ログ配布モニターが以前のログ配布構成で有効になっていた場合は、新しいログ配布構成を監視するようにログ配布モニターを再構成します。  *database_name* をデータベースの名前に置き換えて、次のコマンドを実行します。  
  
    1.  **新しいプライマリ サーバーで、**  
  
         次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行します。  
  
        ```  
        -- Statement to execute on the new primary server  
        USE msdb  
        GO  
        EXEC master.dbo.sp_change_log_shipping_secondary_database @secondary_database = N'database_name', @threshold_alert_enabled = 0;  
        GO  
        ```  
  
    2.  **新しいセカンダリ サーバーで、**  
  
         次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行します。  
  
        ```  
        -- Statement to execute on the new secondary server  
        USE msdb  
        GO  
        EXEC master.dbo.sp_change_log_shipping_primary_database @database=N'database_name', @threshold_alert_enabled = 0;  
        GO  
        ```  
  
## <a name="swapping-roles"></a>ロールの切り替え  
 上記の初期ロール切り替えの手順が完了したら、このセクションの手順に従って、プライマリ データベースとセカンダリ データベース間のロールを切り替えることができます。 ロールを切り替えるには、次の一般的な手順を実行します。  
  
1.  セカンダリ データベースをオンラインにし、NORECOVERY 句を使用してプライマリ サーバー上のトランザクション ログをバックアップします。  
  
2.  元のプライマリ サーバー上のログ配布バックアップ ジョブと、元のセカンダリ サーバー上のコピーおよび復元ジョブを無効にします。  
  
3.  セカンダリ サーバー (新しいプライマリ サーバー) 上のログ配布バックアップ ジョブを有効にし、プライマリ サーバー (新しいセカンダリ サーバー) 上のコピーおよび復元ジョブを有効にします。  
  
> [!IMPORTANT]  
>  セカンダリ データベースをプライマリ データベースに変更するときは、ユーザーおよびアプリケーションに一貫した使用環境を提供するために、新しいプライマリ サーバー インスタンスで、ログインやジョブなどのデータベースのメタデータの一部またはすべてを作成し直す必要がある場合があります。 詳細については、「 [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [ログ配布のセカンダリへのフェールオーバー &#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [役割の交代後のログインとジョブの管理 &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
## <a name="see-also"></a>関連項目  
 [ログ配布テーブルとストアド プロシージャ](log-shipping-tables-and-stored-procedures.md)  
  
  
