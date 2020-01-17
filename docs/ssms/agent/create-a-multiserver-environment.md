---
title: マルチサーバー環境の作成 | Microsoft Docs
ms.custom: ''
ms.date: 01/30/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, multiserver environments
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- multiserver environments [SQL Server]
ms.assetid: edc2b60d-15da-40a1-8ba3-f1d473366ee6
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 27ef7467b0a5877e75f0391c3afe5ea88003c8c4
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264820"
---
# <a name="create-a-multiserver-environment"></a>マルチサーバー環境の作成
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

マルチサーバー管理では、マスター サーバー (MSX) 1 台と、ターゲット サーバー (TSX) 1 台以上を設定する必要があります。 すべてのターゲット サーバーで処理されるジョブは、まずマスター サーバーで定義されてからターゲット サーバーにダウンロードされます。  
  
既定では、マスター サーバーとターゲット サーバーの間の接続では、完全な SSL (Secure Sockets Layer) 暗号化と証明書の検証が有効になります。 詳しくは、「[ターゲット サーバーでの暗号化オプションの設定](../../ssms/agent/set-encryption-options-on-target-servers.md)」をご覧ください。  
  
ターゲット サーバーが多数ある場合、他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能から多くのパフォーマンス要求を受け取る実稼働サーバー上には、マスター サーバーを定義しないでください。ターゲット サーバーのトラフィックによって実稼働サーバーのパフォーマンスが低下する可能性があります。 また、専用のマスター サーバーにイベントを転送すると、1 つのサーバーに管理を集中することができます。 詳しくは、「 [イベントの管理](../../ssms/agent/manage-events.md)」をご覧ください。  
  
> [!NOTE]  
> マルチサーバー ジョブの処理を使用するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスのアカウントがマスター サーバーの **msdb** データベースの **TargetServersRole** ロールのメンバーでなければなりません。 マスター サーバー ウィザードを使用すると、登録処理の一環としてこのロールがサービス アカウントに自動的に追加されます。  
  
## <a name="considerations-for-multiserver-environments"></a>マルチサーバー環境に関する注意点  
  
マルチサーバー環境を作成するときは、次の点を考慮してください。  
  
-   マスター サーバーとして最新のバージョンを使用します。 現在のバージョンと以前の 2 つのバージョンがサポートされています。

-   各ターゲット サーバーは、1 つのマスター サーバーのみに対してレポートを行います。 ターゲット サーバーを別のマスター サーバーに参加させるには、現在のマスター サーバーからそのターゲット サーバーの参加を解除する必要があります。  
  
-   ターゲット サーバーの名前を変更する場合は、名前を変更する前に参加を解除し、変更を行ってから再登録する必要があります。  
  
-   マルチサーバー構成を取り消す場合は、マスター サーバーからすべてのターゲット サーバーの参加を解除する必要があります。  
  
-   SQL Server Integration Services は、マスター サーバーのバージョンと同じバージョンまたはそれ以降のバージョンのターゲット サーバーのみサポートします。  
  
## <a name="related-tasks"></a>Related Tasks  
次のトピックでは、マルチサーバー環境を作成するための一般的な作業について説明します。  
  
|[説明]|トピック|  
|---------------|---------|  
|マスター サーバーを作成する方法について説明します。|[マスター サーバーの作成](../../ssms/agent/make-a-master-server.md)|  
|ターゲット サーバーを作成する方法について説明します。|[ターゲット サーバーの作成](../../ssms/agent/make-a-target-server.md)|  
|マスター サーバーにターゲット サーバーを参加させる方法について説明します。|[マスター サーバーへのターゲット サーバーの参加](../../ssms/agent/enlist-a-target-server-to-a-master-server.md)|  
|マスター サーバーからターゲット サーバーの参加を解除する方法について説明します。|[マスター サーバーからのターゲット サーバーの参加の解除](../../ssms/agent/defect-a-target-server-from-a-master-server.md)|  
|マスター サーバーから複数のターゲット サーバーの参加を解除する方法について説明します。|[マスター サーバーからの複数のターゲット サーバーの参加の解除](../../ssms/agent/defect-multiple-target-servers-from-a-master-server.md)|  
|ターゲット サーバーの状態を確認する方法について説明します。|[sp_help_targetserver (Transact-SQL)](https://msdn.microsoft.com/f841d3bd-901a-4980-ad0b-1c6eeba3f717)<br /><br />[sp_help_targetservergroup (Transact-SQL)](https://msdn.microsoft.com/ec3a4a68-b591-431c-9518-053ede522d0c)|  
  
## <a name="see-also"></a>参照  
[プロキシを使用するマルチサーバー ジョブのトラブルシューティング](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)  
  
