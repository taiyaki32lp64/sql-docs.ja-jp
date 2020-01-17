---
title: マスター サーバーからの複数のターゲット サーバーの参加の解除 | Microsoft Docs
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
- multiple target server defections
ms.assetid: 61a3713b-403a-4806-bfc4-66db72ca1156
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7dc5ad3034885805272ed1d507e0168d5884c4c8
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267228"
---
# <a name="defect-multiple-target-servers-from-a-master-server"></a>マスター サーバーからの複数のターゲット サーバーの参加の解除
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して、マルチサーバー管理構成から複数のターゲット サーバーの参加を解除する方法について説明します。 この手順はマスター サーバーから実行します。  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-defect-multiple-target-servers-from-a-master-server"></a>マスター サーバーから複数のターゲット サーバーの参加を解除するには  
  
1.  **オブジェクト エクスプローラー**で、マスター サーバーとして構成するサーバーを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[マルチ サーバーの管理]** をポイントして、 **[ターゲット サーバーの管理]** をクリックします。  
  
3.  **[命令を通知]** をクリックし、 **[命令の種類]** ボックスの一覧の **[参加解除]** をクリックします。  
  
4.  **[受信者]** で、次のいずれかの操作を行います。  
  
    -   このマスター サーバーのすべてのターゲット サーバーの参加を解除するには、 **[すべてのターゲット サーバー]** をクリックします。 このオプションは、現在のマルチサーバー管理構成を完全にアンインストールする場合に使用します。  
  
    -   このマスター サーバーから一部のターゲット サーバーだけを参加解除するには、 **[特定のターゲット サーバー]** をクリックし、参加を解除するサーバーの **[選択]** ボックスをクリックします。  
  
## <a name="see-also"></a>参照  
[マルチサーバー環境の作成](../../ssms/agent/create-a-multiserver-environment.md)  
[エンタープライズ全体の管理の自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[マスター サーバーからのターゲット サーバーの参加の解除](../../ssms/agent/defect-a-target-server-from-a-master-server.md)  
  
