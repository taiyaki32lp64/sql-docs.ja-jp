---
title: 最小構成での SQL Server の起動 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- minimal configuration [SQL Server]
- starting SQL Server, minimal configuration
ms.assetid: 4d733c99-28b3-42d8-b7f6-7b943b548173
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cf7065d064e322e45fb95a38aed514b2acfc714a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62756220"
---
# <a name="start-sql-server-with-minimal-configuration"></a>最小構成での SQL Server の起動
  構成の問題があるためにサーバーを起動できない場合は、最小構成起動オプションを使用して [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを起動できます。 これが起動オプション **-f**です。 最小構成で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを起動すると、サーバーが自動的にシングル ユーザー モードに設定されます。  
  
 最小構成モードで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを起動する場合は、次の点に注意してください。  
  
-   1 人のユーザーのみが接続でき、CHECKPOINT プロセスは実行されません。  
  
-   リモート アクセスと先行読み取りは無効になります。  
  
-   起動ストアド プロシージャは実行されません。  
  
 最小構成でサーバーを起動後、適切なサーバー オプションの値を変更し、サーバーを停止してから再起動してください。  
  
> [!IMPORTANT]  
>  **sqlcmd** ユーティリティと専用管理者接続 (DAC) を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続します。 一般的な接続を使用する場合は、最小構成モードで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続する前に SQL Server エージェント サービスを停止します。 停止しないと、SQL Server エージェント サービスが接続を使用するため、接続がブロックされます。  
  
## <a name="see-also"></a>参照  
 [SQL Server エージェント サービスの開始、停止、または一時停止](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)   
 [データベース管理者用の診断接続](diagnostic-connection-for-database-administrators.md)   
 [sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [データベース エンジン サービスのスタートアップ オプション](database-engine-service-startup-options.md)  
  
  
