---
title: ジョブの表示または変更 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- jobs [SQL Server Agent], viewing
- modifying jobs
- viewing jobs
- SQL Server Agent jobs, viewing
- SQL Server Agent jobs, modifying
- displaying jobs
ms.assetid: 57f649b8-190c-4304-abd7-7ca5297deab7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 87e5644329742712e112fd3df97f601838f7faea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245522"
---
# <a name="view-or-modify-jobs"></a>ジョブの表示または変更
  作成したジョブはどのジョブでも表示できます。 ジョブの実行後は、履歴を表示することもできます。 ジョブの履歴を表示すると、ジョブを実行した時間、ジョブ全体のステータス、およびジョブを構成するジョブ ステップごとのステータスを確認できます。 これまでにジョブが失敗したことがあるかどうか、最後にジョブが正常に実行されたのはいつか、各ジョブの実行でジョブにより作成された出力はどのようなものかを確認できます。 **sysadmin** 固定サーバー ロールのメンバーは、ジョブの所有者がだれであるかにかかわらず、すべてのジョブを表示または変更できます。  
  
> [!NOTE]  
>  一度も実行されていないジョブには、ジョブ履歴はありません。 ジョブ履歴ログ全体のサイズとジョブごとのサイズは制限できます。  
  
 また、新たな要件に合わせて、ジョブは変更できます。 次の項目を変更できます。  
  
-   応答オプション  
  
-   Schedules  
  
-   ジョブ ステップ  
  
-   所有権  
  
-   ジョブ カテゴリ  
  
-   ターゲット サーバー (マルチサーバー ジョブの場合のみ)  
  
 マルチサーバー ジョブに対する変更を確実に有効にするには、ターゲット サーバーが更新されたジョブをダウンロードできるように、変更をダウンロード一覧に適用する必要があります。 ターゲット サーバーが最新のジョブ定義を保持するようにするには、マルチサーバー ジョブの更新後に、次のような INSERT 命令を通知します。  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
 詳細については、次を参照してください。 [sp_purge_jobhistory &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql)します。  
  
 **sysadmin** 固定サーバー ロールのメンバーは、あらゆるジョブに対して、ジョブの定義や履歴を表示したり、ジョブを変更したりできます。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**[説明]**|**トピック**|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント ジョブを表示する方法について説明します。|[View a Job](view-a-job.md)|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントのジョブ履歴ログを表示する方法について説明します。|[View the Job History](view-the-job-history.md)|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントのジョブ履歴ログの内容を削除する方法について説明します。|[Clear the Job History Log](clear-the-job-history-log.md)|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントのジョブ履歴ログのサイズ制限を設定する方法について説明します。|[Resize the Job History Log](resize-the-job-history-log.md)|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のエージェント ジョブのプロパティを変更する方法について説明します。|[Modify a Job](modify-a-job.md)|  
  
## <a name="see-also"></a>参照  
 [dbo.sysjobhistory &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-tables/dbo-sysjobhistory-transact-sql)  
  
  
