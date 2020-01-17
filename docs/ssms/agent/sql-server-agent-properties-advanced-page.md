---
title: SQL Server エージェントのプロパティ ([詳細設定] ページ) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.advanced.f1
ms.assetid: a4d798ee-4c18-40d4-b6af-63d17503738c
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a427b41e5f1269a4f59fd69257f54bdbd61a3050
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265375"
---
# <a name="sql-server-agent-properties-advanced-page"></a>SQL Server エージェントのプロパティ ([詳細設定] ページ)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このページを使用すると、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスの詳細プロパティを表示および変更できます。  
  
## <a name="options"></a>オプション  
**[SQL Server イベントの転送]**  
このカテゴリのオプションを使用して、イベントの転送をアクティブにしたり、構成したりします。  
  
**[イベントを別のサーバーに転送する]**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント イベントを別のサーバーに転送します。  
  
**[サーバー]**  
イベントの転送先のサーバー名を選択します。  
  
**[未処理のイベント]**  
未処理のイベントのみを指定のサーバーに転送します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、警告が返されないイベントのみを転送します。  
  
**[すべてのイベント]**  
すべてのイベントを転送します。 ローカル インスタンスの警告がイベントに応答した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントはイベントの転送と警告の処理の両方を行います。  
  
**[次のレベル以上のイベント発生時]**  
指定された重大度レベル以上のイベントのみを転送します。  
  
**[CPU のアイドル状態]**  
このカテゴリのオプションは、CPU のアイドル スケジュールで実行がスケジュールされたジョブを、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行するための条件を定義します。  
  
**[CPU のアイドル状態を定義する]**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントにより CPU がアイドル状態であると見なされる条件を定義します。  
  
**[CPU の平均使用量が次の値以下になったとき]**  
CPU がアイドル状態であると見なされる CPU の使用量の割合です。  
  
**[かつ、この使用率以下で次の期間を経過]**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが CPU のアイドル スケジュールのジョブを実行する前に、CPU の平均使用量が指定されたレベルを下回っていなければならない時間です。  
  
## <a name="see-also"></a>参照  
[スケジュールの作成とジョブへのアタッチ](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[イベントの管理](../../ssms/agent/manage-events.md)  
  
