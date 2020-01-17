---
title: パフォーマンス オブジェクトの使用 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 73e36b4d0ee10d42ec7774e20693d217ee274344
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68260910"
---
# <a name="use-performance-objects"></a>パフォーマンス オブジェクトの使用
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントには、サービスの動作を監視するためのパフォーマンス オブジェクトとパフォーマンス カウンターが含まれています。 パフォーマンス オブジェクトを使用すると、パフォーマンス モニターや Windows ツールを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスのバックグラウンド動作を特定できるようになります。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスで現在実行されているアクティブなジョブの数を特定して、ブロックされたジョブを特定できます。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスのパフォーマンス オブジェクトとパフォーマンス カウンターは、コンピューターにインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスごとに存在します。 パフォーマンス オブジェクトの名前は、各オブジェクトが表す [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに従って付けられます。  
  
次の表は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスのパフォーマンス オブジェクトの命名形式を示しています。  
  
|インスタンスの種類|オブジェクト名です。|  
|-----------------|---------------|  
|既定|**SQLAgent:** _オブジェクト_:_カウンター_|  
|名前付き|**SQLAgent$**<br /> **&#42;instance_name&#42; :** _オブジェクト_:_カウンター_|  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの次のパフォーマンス オブジェクトが含まれています。  
  
|オブジェクト名です。|[説明]|  
|---------------|---------------|  
|[SQLAgent:Jobs](../../relational-databases/performance-monitor/sql-server-agent-jobs-object.md)|開始されたジョブ、成功率、および現在の状態に関するパフォーマンス情報|  
|[SQLAgent:JobSteps](../../relational-databases/performance-monitor/sql-server-agent-jobsteps-object.md)|ジョブ ステップに関する状態情報|  
|[SQLAgent:Alerts](../../relational-databases/performance-monitor/sql-server-agent-alerts-object.md)|警告と通知の数に関する情報|  
|[SQLAgent:Statistics](../../relational-databases/performance-monitor/sql-server-agent-statistics-object.md)|パフォーマンスに関する一般的な情報|  
  
## <a name="see-also"></a>参照  
[パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
[方法:システム モニターの起動 (Windows)](https://msdn.microsoft.com/5e51bb79-5737-470b-9c47-fac330c001c5)  
  
