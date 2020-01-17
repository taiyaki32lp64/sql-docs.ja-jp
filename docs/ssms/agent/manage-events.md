---
title: イベントの管理 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- event-triggered jobs [SQL Server]
- forwarding events [SQL Server]
- alerts [SQL Server], forwarded events
- alerts [SQL Server], management servers
- SQL Server Agent alerts, management servers
ms.assetid: 8f4ee7f5-80df-49fd-b2b8-d020e04b6e1b
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a777dc834e835f7f06bc301158e4967d9c8117e1
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68258173"
---
# <a name="manage-events"></a>イベントの管理
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスには、特定のエラー重大度レベル以上のあらゆるイベント メッセージを転送できます。 この処理を *イベントの転送*と呼びます。 転送先サーバーは、マスター サーバーにもなる専用のサーバーです。 イベントの転送を使用して、サーバーのグループに対する警告を集中管理できます。その結果、使用頻度の高いサーバーの負荷を減少させることができます。  
  
1 台のサーバーが別のサーバー グループのイベントを受信する場合、イベントを受信するサーバーは *警告管理サーバー*と呼ばれます。 マルチサーバー環境では、マスター サーバーを警告管理サーバーとして指定します。  
  
## <a name="advantages-of-using-an-alerts-management-server"></a>警告管理サーバーを使用する利点  
警告管理サーバーのセットアップには、次の利点があります。  
  
-   **集中化**。 1 台のサーバーで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンスのイベントを集中管理したり統合表示したりできます。  
  
-   **スケーラビリティ**。 多くの物理サーバーを 1 台の論理サーバーとして管理できます。 必要に応じて、この物理サーバー グループに対してサーバーを追加または削除できます。  
  
-   **効率性**。 警告とオペレーターは一度だけ定義すればよいので、構成にかかる時間を節約できます。  
  
## <a name="disadvantages-of-using-an-alerts-management-server"></a>警告管理サーバーを使用する欠点  
警告管理サーバーのセットアップには、次のような欠点があります。  
  
-   **トラフィックの増加**。 警告管理サーバーにイベントを転送すると、ネットワーク トラフィックが増加することがあります。 ネットワーク トラフィックの増加を緩和するには、指定した重大度レベルを超えるイベントだけを転送するように制限します。  
  
-   **単一地点での障害**。 警告管理サーバーがオフラインになると、管理されたサーバーのグループのイベントに対して警告が発行されません。  
  
-   **サーバーの負荷**。 転送されるイベントの警告処理により、警告管理サーバーの処理負荷が増加します。  
  
## <a name="guidelines-for-using-an-alerts-management-server"></a>警告管理サーバーの使用に関するガイドライン  
警告管理サーバーを構成する場合、次のガイドラインに従います。  
  
-   転送されたイベントを受信するには、警告管理サーバーが SQL Server の既定のインスタンスである必要があります。  
  
-   警告管理サーバーで、重要度または使用頻度の高いアプリケーションを実行しないようにします。  
  
-   多くのサーバーで同じ警告管理サーバーが共有されるように構成する場合、それに伴うネットワーク トラフィックについて慎重に検討します。 トラフィックが集中してしまった場合は、特定の警告管理サーバーを使用するサーバーの台数を減らします。  
  
    [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 内で登録されたサーバーは、警告転送サーバーとして選択できるサーバーの一覧に含まれます。  
  
-   警告管理サーバーに警告を転送するのではなく、サーバー固有の応答を必要とする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカル インスタンスで警告を定義します。  
  
    警告管理サーバーは、警告を転送してくるすべてのサーバーを 1 台の論理サーバーと見なします。 たとえば、警告管理サーバーは、サーバー A からの 605 イベントと、サーバー B からの 605 イベントに同じように応答します。  
  
-   警告システムを構成した後は、Microsoft Windows アプリケーション ログで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント イベントの有無を定期的に確認します。  
  
    警告エンジンによって検出されたエラー状況は、"SQL Server エージェント" のソース名でローカル Windows アプリケーション ログに書き込まれます。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが定義に従って電子メールによる通知を送信できない場合は、アプリケーション ログにイベントが記録されます。  
  
ローカルで定義された警告が無効になっていて、その警告の発生原因となるイベントが発生した場合、そのイベントが (警告転送の条件を満たしていれば) 警告管理サーバーに転送されます。 この場合、ローカル サイトのユーザーの必要に応じて、ローカルオーバーライド (つまりローカル サーバーで定義され、警告管理サーバーでも定義される警告) を有効または無効にすることができます。 また、イベントがローカル警告によって処理される場合でも、必ずイベントが転送されるように要求することもできます。  
  
次に、マルチサーバー環境でイベントを管理するための一般的なタスクを示します。  
  
**警告管理サーバーを指定するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/designate-an-events-forwarding-server-sql-server-management-studio.md)  
  
**警告に対する応答を定義するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)  
  
## <a name="running-event-triggered-jobs"></a>イベント トリガーのジョブの実行  
警告に応答して実行されるジョブを定義できます。 たとえば、警告によって検出された問題を修正したり、さらに診断したりするジョブを実行できます。  
  
> [!NOTE]  
> ジョブがイベントを発生させることもありえるので、再帰的な警告ジョブ ループを作成しないように注意してください。  
  
## <a name="see-also"></a>参照  
[sp_add_notification (Transact-SQL)](https://msdn.microsoft.com/44bee7d9-7517-4071-99be-8b36f979c7cc)  
  
