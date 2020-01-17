---
title: '[SQL Server エージェントのプロパティ] ダイアログ ボックス ([ジョブ システム] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2c419212205e7bf5b57f82036b8537a321032895
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265250"
---
# <a name="sql-server-agent-properties-job-system-page"></a>[SQL Server エージェントのプロパティ] ダイアログ ボックス ([ジョブ システム] ページ)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このページを使用すると、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスによるジョブの管理方法を表示および変更ができます。  
  
## <a name="options"></a>オプション  
**[シャットダウン タイムアウト間隔 (秒)]**  
シャットダウンの前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがジョブの完了を待つ時間を秒数で指定します。 指定した時間が過ぎてもジョブが実行されている場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって強制的にジョブが停止されます。  
  
**[管理者以外のプロキシ アカウントを使用する]**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントに管理者以外のプロキシ アカウントを設定します。 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] 以降のバージョンでは複数のプロキシがサポートされるため、このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] より前のバージョンの [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]エージェントを管理する場合にのみ適用できます。  
  
**User name**  
管理者以外のプロキシ アカウントのユーザーの名前を入力します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では複数のプロキシがサポートされるため、このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] より前のバージョンの [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]エージェントを管理する場合にのみ適用できます。  
  
**パスワード**  
管理者以外のプロキシ アカウントのユーザーのパスワードを入力します。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンでは複数のプロキシがサポートされるため、このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] より前のバージョンの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]エージェントを管理する場合にのみ適用できます。  
  
**[ドメイン]**  
管理者以外のプロキシ アカウントのユーザーのドメインを入力します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では複数のプロキシがサポートされるため、このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] より前のバージョンの [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]エージェントを管理する場合にのみ適用できます。  
  
## <a name="see-also"></a>参照  
[ジョブの実装](../../ssms/agent/implement-jobs.md)  
  
