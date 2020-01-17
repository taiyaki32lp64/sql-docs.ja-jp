---
title: スケジュールの作成とジョブへのアタッチ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server]
- scheduling jobs [SQL Server]
- jobs [SQL Server], scheduling
- CPU [SQL Server], idle conditions
- automatic job processing
- SQL Server Agent jobs, scheduling
- idle time [SQL Server]
ms.assetid: 079c2984-0052-4a37-a2b8-4ece56e6b6b5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 414ff334139919e08b06291ec910f8531c70cd55
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63136279"
---
# <a name="create-and-attach-schedules-to-jobs"></a>スケジュールの作成とジョブへのアタッチ
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブのスケジュール設定とは、ユーザーの操作なしでジョブの実行が開始される条件を定義することです。 ジョブのスケジュールを設定して自動的に実行するには、ジョブの新しいスケジュールを作成するか、既存のスケジュールをジョブにアタッチします。  
  
 スケジュールを作成するには、次の 2 つの方法があります。  
  
-   ジョブの作成時にスケジュールを作成する。  
  
-   オブジェクト エクスプローラーでスケジュールを作成する。  
  
 スケジュールを作成したら、特定のジョブに対して作成した場合でも、そのスケジュールを複数のジョブにアタッチすることができます。 また、ジョブからスケジュールをデタッチすることもできます。  
  
 スケジュールは、時刻またはイベントに基づいて作成できます。 たとえば、次のタイミングで実行するようにジョブをスケジュールできます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが開始されるたびに、ジョブを実行する。  
  
-   コンピューターの CPU 使用率がアイドルとして定義したレベルになったときに、ジョブを実行する。  
  
-   指定した日時に 1 回だけジョブを実行する。  
  
-   スケジュールに従って定期的にジョブを実行する。  
  
 また、ジョブ スケジュールの代わりとして、ジョブの実行によってイベントに応答する警告を作成することもできます。  
  
> [!NOTE]  
>  一度にジョブの 1 つのインスタンスだけを実行できます。 スケジュールどおりに実行されているときに、手動でジョブを実行しようとすると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントはその要求を拒否します。  
  
 スケジュールされたジョブが実行されないようにするには、次のいずれかの操作を行う必要があります。  
  
-   スケジュールを無効にする。  
  
-   ジョブを無効にする。  
  
-   ジョブからスケジュールをデタッチする。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを停止する。  
  
-   スケジュールを削除する。  
  
 スケジュールが無効になっている場合でも、ジョブは警告に応答したときやユーザーが手動で実行したときに実行されます。 ジョブ スケジュールが無効になっているときは、スケジュールを使用するすべてのジョブのスケジュールが無効になります。  
  
 無効になっているスケジュールは、明示的に有効にする必要があります。 スケジュールを編集しても、スケジュールは自動的に有効になりません。  
  
## <a name="scheduling-start-dates"></a>開始日のスケジュール設定  
 スケジュールの開始日は 19900101 以降にする必要があります。  
  
 スケジュールをジョブにアタッチする場合は、スケジュールでジョブを最初に実行する際に使用する開始日を確認する必要があります。 開始日は、スケジュールをジョブにアタッチする日時によって決まります。 たとえば、隔週月曜日の午前 8 時に実行されるスケジュールを作成するとします。 2008 年 3 月 3 日月曜日の午前 10 時にジョブを作成した場合、 スケジュールの開始日は 2008 年 3 月 17 日月曜日になります。 2008 年 3 月 4 日火曜日に別のジョブを作成した場合、スケジュールの開始日は 2008 年 3 月 10 日月曜日になります。  
  
 スケジュールの開始日は、スケジュールをジョブにアタッチした後でも変更できます。  
  
## <a name="cpu-idle-schedules"></a>CPU アイドル スケジュール  
 CPU リソースを最大限に使用するために、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントに対して CPU アイドル条件を定義できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、CPU アイドル条件の設定に基づいて、ジョブの実行に最適な時期を決定します。 たとえば、CPU アイドル時と処理量の少ない時期に、インデックスを再構築するジョブをスケジュールできます。  
  
 CPU アイドル時に実行するジョブを定義する前に、通常処理時の CPU の負荷を調べてください。 CPU の負荷を調べるには、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] またはパフォーマンス モニターを使用して、サーバー トラフィックを監視し、統計情報を収集します。 収集した情報を参考にして、CPU アイドル時の比率および時間を設定します。  
  
 CPU アイドル条件は、特定の時間にわたり、CPU 使用率が一定の割合を下回っている状態として定義します。 次に、この時間の長さを設定します。 指定された長さの時間にわたって CPU 使用率が指定の率を下回ると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、CPU アイドル時スケジュールが設定されているすべてのジョブを開始します。 使用しての詳細については[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]CPU 使用率を監視するパフォーマンス モニターを参照してくださいまたは[CPU 使用状況の監視](../../relational-databases/performance-monitor/monitor-cpu-usage.md)します。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**[説明]**|**トピック**|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブのスケジュールを作成する方法について説明します。|[Create a Schedule](create-a-schedule.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブのスケジュールを設定する方法について説明します。|[ジョブのスケジュール設定](schedule-a-job.md)|  
|使用しているサーバーの CPU アイドル状態を定義する方法について説明します。|[CPU のアイドル時間と期間の設定 (SQL Server Management Studio)](set-cpu-idle-time-and-duration-sql-server-management-studio.md)|  
  
## <a name="see-also"></a>関連項目  
 [sp_help_jobschedule &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-jobschedule-transact-sql)   
 [では&#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-tables/dbo-sysjobschedules-transact-sql)  
  
  
