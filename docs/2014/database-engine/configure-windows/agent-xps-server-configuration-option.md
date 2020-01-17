---
title: Agent XP サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Agent XPs option
- extended stored procedures [SQL Server], SQL Server Agent
ms.assetid: 2e1c6c64-5ce7-4357-98c7-ac7763a9f9de
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4ed2a24c72765c51e7d05fecaa5ab22c344013b2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62789023"
---
# <a name="agent-xps-server-configuration-option"></a>Agent XP サーバー構成オプション
  **Agent XPs** オプションは、このサーバーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの拡張ストアド プロシージャを有効にする場合に使用します。 このオプションを有効にしないと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のオブジェクト エクスプローラーに [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] エージェントのノードが表示されません。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ツールを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを開始すると、これらの拡張ストアド プロシージャは自動的に有効になります。 詳細については、「 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] のオブジェクト エクスプローラーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント サービスの状態にかかわらず、これらの拡張ストアド プロシージャを有効にしない限り、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのノードのコンテンツは表示されません。  
  
 可能な値は次のとおりです。  
  
-   **0**は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの拡張ストアド プロシージャを使用できないことを示します (既定)。  
  
-   **1**は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの拡張ストアド プロシージャを使用できることを示します。  
  
 この設定は、サーバーを停止して再起動しなくてもすぐに有効になります。  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの拡張ストアド プロシージャを有効にします。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Agent XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>参照  
 [管理タスクの自動化 &#40;SQL Server エージェント&#41;](../../ssms/agent/sql-server-agent.md)   
 [SQL Server エージェント サービスの開始、停止、または一時停止](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  
