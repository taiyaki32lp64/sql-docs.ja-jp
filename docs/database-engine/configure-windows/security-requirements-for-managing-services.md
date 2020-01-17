---
title: サービスの管理に関するセキュリティ要件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent service, security
- services [SQL Server], security
- SQL Server services, security
- WMI Providers [SQL Server]
- server configuration [SQL Server]
- security [SQL Server], services
- services [SQL Server], WMI
ms.assetid: 1874a317-ddb2-425d-98d9-b53e1be6fc6a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ede737abf7d158e4d8dee66885ced018f03a375e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68025629"
---
# <a name="security-requirements-for-managing-services"></a>サービスの管理に関するセキュリティ要件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを管理するには、SQL Server 構成マネージャーまたは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用します。 クラスター化されたサーバー上のサービスを管理するには、クラスター アドミニストレーターを使用します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを管理し、サーバー構成オプションを設定するには、 **serveradmin** 固定サーバー ロールまたは **sysadmin** 固定サーバー ロールのメンバーであることが必要です。 Windows の **Administrators** グループのメンバーは、サービスを開始および停止したり、Windows で提供されているサーバー オプションを構成したりできます。  
  
> [!NOTE]  
>  適切に操作するには、サービスに使用するアカウントに、正しいドメイン、ファイル システム、およびレジストリ権限を設定する必要があります。 必要なアクセス許可については、「 [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
## <a name="windows-management-instrumentation"></a>Windows Management Instrumentation (Windows Management Instrumentation)  
 SQL Server 構成マネージャーと [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、一部のサーバー プロパティの表示および変更に Windows Management Instrumentation (WMI) が使用されます。 サービスを管理し、サービスの状態を取得するには、ユーザーは WMI オブジェクトにアクセスする権限を持っている必要があります。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]では、次のサーバー プロパティ ページで WMI が使用されています。  
  
-   サービスの自動開始  
  
-   起動時のパラメーター  
  
-   Security  
  
-   その他のサーバーの設定  
  
## <a name="related-tasks"></a>Related Tasks  
 [SQL Server ツールでサーバーの状態を表示できるようにする WMI の構成](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 [構成管理用の WMI プロバイダーの概念](../../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  
