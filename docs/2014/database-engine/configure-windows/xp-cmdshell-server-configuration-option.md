---
title: xp_cmdshell サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: c147c9e1-b81d-49c8-b800-3019f4d86a13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9f4ab373c9827adff6e0138a81b5eaa57d1c4414
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62755177"
---
# <a name="xpcmdshell-server-configuration-option"></a>xp_cmdshell サーバー構成オプション
  **xp_cmdshell** オプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] xp_cmdshell **拡張ストアド プロシージャをシステムで実行できるかどうかをシステム管理者が制御できるようにする、** のサーバー構成オプションです。 新しいインストールでは、 **xp_cmdshell** オプションは既定で無効になっており、ポリシー ベースの管理を使用するか、次のコード例のように **sp_configure** システム ストアド プロシージャを実行することで有効にできます。  
  
```  
-- To allow advanced options to be changed.  
EXEC sp_configure 'show advanced options', 1;  
GO  
-- To update the currently configured value for advanced options.  
RECONFIGURE;  
GO  
-- To enable the feature.  
EXEC sp_configure 'xp_cmdshell', 1;  
GO  
-- To update the currently configured value for this feature.  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
