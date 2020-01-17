---
title: sys.dm_os_cluster_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_cluster_properties_TSQL
- sys.dm_os_cluster_properties
- dm_os_cluster_properties_TSQL
- dm_os_cluster_properties
dev_langs:
- TSQL
helpviewer_keywords:
- dm_os_cluster_properties
- sys.dm_os_cluster_properties
ms.assetid: 6d82e770-fba7-49e0-9a0c-3b34b393e4a7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3fd3c53f5603567e0f6c2b6ee4f1712f742c1137
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900228"
---
# <a name="sysdmosclusterproperties-transact-sql"></a>sys.dm_os_cluster_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  このトピックに記載されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クラスター リソース プロパティの現在の設定内容で 1 つの行を返します。 このビューが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスタンドアロン インスタンスで実行されている場合、データは返されません。  
  
 これらのプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスのエラー検出、障害応答時間、および正常性状態の監視のログ記録に影響を与える値を設定するために使用されます。  
  

|列名|プロパティ|説明|  
|-----------------|--------------|-----------------|  
|VerboseLogging|BIGINT|SQL Server フェールオーバー クラスターのログ記録レベルです。 詳細ログをオンにすると、トラブルシューティングを目的とした詳細情報をエラー ログに追加できます。 次のいずれかの値です。<br /><br /> 0: ログ記録はオフです (既定)<br /><br /> 1: エラーのみ。<br /><br /> 2: エラーおよび警告<br /><br /> 詳細については、次を参照してください。 [ALTER SERVER CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)します。|  
|SqlDumperDumpFlags|BIGINT|SQLDumper ダンプ フラグは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって生成されるダンプ ファイルの種類を決定します。 既定の設定は 0 です。|  
|SqlDumperDumpPath|nvarchar (260)|SQLDumper ユーティリティがダンプ ファイルを生成する場所です。|  
|SqlDumperDumpTimeOut|BIGINT|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でエラーが発生した場合の、SQLDumper ユーティリティによるダンプの生成のタイムアウト値 (ミリ秒単位) です。 既定値は 0 です。|  
|FailureConditionLevel|BIGINT|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターのエラーまたは再起動の条件を設定します。 既定値は、3 です。 詳細については、またはプロパティの設定を変更するを参照してください。 [FailureConditionLevel プロパティ設定の構成](../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md)します。|  
|HealthCheckTimeout|BIGINT|SQL Server データベース エンジンのリソース DLL が、サーバーの状態情報を待機する時間のタイムアウト値です。この待機時間を経過すると、SQL Server のインスタンスが応答不能と見なされます。 このタイムアウト値は、ミリ秒単位で指定します。 既定値は 60000 です。 詳細については、またはこのプロパティの設定を変更するを参照してください。 [HealthCheckTimeout プロパティ設定の構成](../../sql-server/failover-clusters/windows/configure-healthchecktimeout-property-settings.md)します。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、sys.dm_os_cluster_properties を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター リソースのプロパティ設定を返します。  
  
```  
SELECT VerboseLogging, SqlDumperDumpFlags, SqlDumperDumpPath, SqlDumperDumpTimeOut, FailureConditionLevel, HealthCheckTimeout  
FROM sys.dm_os_cluster_properties;  
```  
  
 次に結果セットの例を示します。  
  
|VerboseLogging|SqlDumperDumpFlags|SqlDumperDumpPath|SqlDumperDumpTimeOut|FailureConditionLevel|HealthCheckTimeout|  
|--------------------|------------------------|-----------------------|--------------------------|---------------------------|------------------------|  
|0|0|NULL|0|3|60000|  
  
  
