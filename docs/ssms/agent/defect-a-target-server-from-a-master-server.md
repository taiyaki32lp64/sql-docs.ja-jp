---
title: マスター サーバーからのターゲット サーバーの参加の解除 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
ms.assetid: a6da262b-7b38-4ce4-bfd6-6a557c6e8a84
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 114dbc73c42404d66de34eb0273d47abd561f337
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553037"
---
# <a name="defect-a-target-server-from-a-master-server"></a>マスター サーバーからのターゲット サーバーの参加の解除
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)]、または SQL Server 管理オブジェクト (SMO) を使用して、マスター サーバーからターゲット サーバーの参加を解除する方法について説明します。 この手順はターゲット サーバーから実行します。  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Security"></a>セキュリティ  
  
#### <a name="Permissions"></a>アクセス許可  
このストアド プロシージャを実行するには、 **sysadmin** 固定サーバー ロールのメンバーであることが必要です。  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>マスター サーバーからターゲット サーバーの参加を解除するには  
  
1.  **オブジェクト エクスプローラー**で、ターゲット サーバーとして構成するサーバーを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[マルチ サーバーの管理]** をポイントして、 **[参加解除]** をクリックします。  
  
3.  **[はい]** をクリックして、マスター サーバーからこのターゲット サーバーの参加を解除することを確認します。  
  
## <a name="TsqlProcedure"></a>Transact-SQL の使用  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>マスター サーバーからターゲット サーバーの参加を解除するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde_md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
```  
sp_msx_defect ;  
```  
  
詳細については、「 [sp_msx_defect (Transact-SQL)](https://msdn.microsoft.com/0dfd963a-3bc5-4b58-94f7-aec976da2883)」を参照してください。  
  
## <a name="PowerShellProcedure"></a>SQL Server 管理オブジェクト (SMO) の使用  
**MsxDefect メソッド**を使用します。  
  
## <a name="see-also"></a>参照  
[マルチサーバー環境の作成](../../ssms/agent/create-a-multiserver-environment.md)  
[エンタープライズ全体の管理の自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[マスター サーバーからの複数のターゲット サーバーの参加の解除](../../ssms/agent/defect-multiple-target-servers-from-a-master-server.md)  
  
