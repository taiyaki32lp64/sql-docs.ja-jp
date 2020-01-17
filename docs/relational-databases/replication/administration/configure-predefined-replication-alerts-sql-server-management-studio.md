---
title: 定義済みのレプリケーションの警告の構成 (SSMS)
description: SQL Server Management Studio (SSMS) を使用して、定義済みのレプリケーションの警告を構成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
ms.assetid: c0414147-7ffe-4f9a-908c-71c1b5201584
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 9bf49c5892dd22b417df7aeec50f20c0f81b410b
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322069"
---
# <a name="configure-predefined-replication-alerts-sql-server-management-studio"></a>定義済みのレプリケーションの警告の構成 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  レプリケーションには、以下の定義済みの警告が用意されています。これらは、レプリケーション イベントに応答するように構成できます。  
  
-   **レプリケーション: エージェントが成功しました**  
  
-   **レプリケーション: エージェントが失敗しました**  
  
-   **レプリケーション: エージェントを再試行します**  
  
-   **レプリケーション: 有効期限の切れたサブスクリプションを削除しました**  
  
-   **レプリケーション:データ検証で問題が見つかった後、サブスクリプションが再初期化されました**  
  
-   **レプリケーション:サブスクライバーでデータ検証の問題が見つかりました**  
  
-   **レプリケーション:サブスクライバーでデータ検証を正常に終了しました**  
  
-   **レプリケーション: エージェントのカスタム シャットダウン**  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] の **[警告]** フォルダー、またはレプリケーション モニターの **[警告]** タブからこれらの警告を構成できます。 このタブにアクセスする方法の詳細については、「[レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)」を参照してください。  
  
 これらの警告に加え、レプリケーション モニターでは、ステータスおよびパフォーマンスに関連する一連の警告を使用できます。 詳細については、「 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)」を参照してください。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 警告システムを使用して、他のレプリケーション イベントの警告を定義することもできます。 詳細については、「[ユーザー定義イベントの作成](https://msdn.microsoft.com/library/03d71a35-97fa-4bba-aa9a-23ac9c9cf879)」を参照してください。  
  
### <a name="to-configure-a-predefined-replication-alert-in-management-studio"></a>Management Studio で定義済みのレプリケーションの警告を構成するには  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]でディストリビューターに接続して、サーバー ノードを展開します。  
  
2.  **[SQL Server エージェント]** フォルダーを展開して、 **[警告]** フォルダーを展開します。  
  
3.  レプリケーションの警告を右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[\<AlertName> 警告のプロパティ]** ダイアログ ボックスのオプションを設定します。  
  
    -   **[全般]** ページで **[有効化]** をクリックし、警告を適用するデータベースを指定します。  
  
    -   **[応答]** ページで、電子メールを送信するかどうか、または、ジョブを実行するかどうかを指定します。  
  
         警告が、 **[レプリケーション:サブスクライバーでデータ検証の問題が見つかりました]** である場合、レプリケーションがこの警告に提供する応答ジョブを指定することができます。 **[ジョブの実行]** を選択し、参照ボタン ( **...** ) をクリックします。 **[ジョブの検索]** ダイアログ ボックスで、 **[参照]** をクリックします。 **[オブジェクトの参照]** ダイアログ ボックスで、 **[データ検証で問題が見つかったサブスクリプションの再初期化]** をクリックします。 両方の開いているダイアログ ボックスで、 **[OK]** をクリックします。 ジョブを実行するとき、サブスクリプションを再初期化するストアド プロシージャへのリモート プロシージャ コール (RPC) が使用されます。 パブリッシャーがリモート ディストリビューターを使用する場合、パブリッシャーでリモート サーバー ログインを定義して、ディストリビューターからパブリッシャーへの RPC を実行可能にする必要があります。  
  
    -   **[オプション]** ページで、応答のテキストをカスタマイズします。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

### <a name="to-configure-an-alert-for-a-threshold-in-replication-monitor"></a>レプリケーション モニターでしきい値に対する警告を構成するには  
  
1.  **[警告]** タブで、 **[警告の構成]** をクリックします。  
  
2.  **[レプリケーションの警告の構成]** ダイアログ ボックスで警告を選択し、 **[構成]** をクリックします。  
  
3.  **[\<AlertName> 警告のプロパティ]** ダイアログ ボックスのオプションを設定します。  
  
    -   **[全般]** ページで **[有効化]** をクリックし、警告を適用するデータベースを指定します。  
  
    -   **[応答]** ページで、電子メールを送信するかどうか、または、ジョブを実行するかどうかを指定します。  
  
         警告が、 **[レプリケーション:サブスクライバーでデータ検証の問題が見つかりました]** である場合、レプリケーションがこの警告に提供する応答ジョブを指定することができます。 **[ジョブの実行]** を選択し、参照ボタン ( **...** ) をクリックします。 **[ジョブの検索]** ダイアログ ボックスで、 **[参照]** をクリックします。 **[オブジェクトの参照]** ダイアログ ボックスで、 **[データ検証で問題が見つかったサブスクリプションの再初期化]** をクリックします。 両方の開いているダイアログ ボックスで、 **[OK]** をクリックします。 ジョブを実行するとき、サブスクリプションを再初期化するストアド プロシージャへのリモート プロシージャ コール (RPC) が使用されます。 パブリッシャーがリモート ディストリビューターを使用する場合、パブリッシャーでリモート サーバー ログインを定義して、ディストリビューターからパブリッシャーへの RPC を実行可能にする必要があります。  
  
    -   **[オプション]** ページで、応答のテキストをカスタマイズします。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  **[閉じる]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェント イベントに対する警告の使用](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)  
  
  
