---
title: SQL Server エージェント ジョブの実行タスク
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.executesqlserveragentjobtask.f1
helpviewer_keywords:
- Execute SQL Server Agent Job task [Integration Services]
- jobs [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 3aa3bc0e-1a1c-452e-81b8-b4e3422ea053
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 081cfc1b5808ca38fb536197cfa44d60f2203b99
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056561"
---
# <a name="execute-sql-server-agent-job-task"></a>SQL Server エージェント ジョブの実行タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブの実行タスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを実行します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、SQL Server のインスタンスで定義されたジョブを実行する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows サービスです。 ユーザーは、Transact-SQL ステートメントや ActiveX スクリプトの実行、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] やレプリケーションのメンテナンス タスクの実行、およびパッケージの実行を行うジョブを作成できます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を監視し、警告を発するジョブを構成することもできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブは、通常、繰り返し実行するタスクの自動化に使用します。 詳細については、 [「ジョブの実装」](../../ssms/agent/implement-jobs.md)を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブの実行タスクを使用すると、パッケージは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントに関連する管理タスクを実行できます。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブでは、フォルダー内のパッケージの一覧を取得する **sp_enum_dtspackages** などのシステム ストアド プロシージャを実行できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ローカルまたはマルチサーバーの管理ジョブを自動的に実行できるようにするには、エージェントを実行している必要があります。  
  
 このタスクは、 **sp_start_job** システム プロシージャをカプセル化し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブの名前を引数としてこのプロシージャに渡します。 詳細については、[「sp_start_job (Transact-SQL)」](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md) を参照してください。  
  
## <a name="configuring-the-execute-sql-server-agent-job-task"></a>SQL Server エージェント ジョブの実行タスクの構成  
 プロパティは、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから設定できます。 このタスクは、 **デザイナーの** [ツールボックス] **の** [メンテナンス プランのタスク] [!INCLUDE[ssIS](../../includes/ssis-md.md)] に表示されます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[SQL Server エージェント ジョブの実行タスク] (メンテナンス プラン)](../../relational-databases/maintenance-plans/execute-sql-server-agent-job-task-maintenance-plan.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  
