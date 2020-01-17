---
title: AlwaysOn 可用性グループ (SQL Server PowerShell) のデータベースミラーリングエンドポイントを作成します。Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], endpoint
ms.assetid: 6197bbe7-67d4-446d-ba5f-cabfa5df77f1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5fb67c488da5f01ac572ec78a369790fc9014513
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782989"
---
# <a name="create-a-database-mirroring-endpoint-for-alwayson-availability-groups-sql-server-powershell"></a>AlwaysOn 可用性グループのデータベース ミラーリング エンドポイントの作成 (SQLServer PowerShell)
  このトピックでは、PowerShell を使用して、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で使用するデータベース ミラーリング エンドポイントを作成する方法について説明します。  
  
 **このトピックの内容**  
  
-   **Before you begin:**  [Security](#Security)  
  
-   **データベース ミラーリング エンドポイントを作成するために使用するもの:**  [PowerShell](#PowerShellProcedure)  
  
## <a name="before-you-begin"></a>作業を開始する準備  
  
###  <a name="Security"></a> セキュリティ  
  
> [!IMPORTANT]  
>  RC4 アルゴリズムは非推奨とされます。 [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)] AES を使用することをお勧めします。  
  
####  <a name="Permissions"></a> アクセス許可  
 CREATE ENDPOINT 権限、または sysadmin 固定サーバー ロールのメンバーシップが必要です。 詳細については、「 [GRANT (エンドポイントの権限の許可) &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql)」を参照してください。  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
 **データベース ミラーリング エンドポイントを作成するには**  
  
1.  ディレクトリ変更コマンド (`cd`) を使用して、データベース ミラーリング エンドポイントを作成するサーバー インスタンスに接続します。  
  
2.  `New-SqlHadrEndpoint` コマンドレットを使用してエンドポイントを作成し、その後 `Set-SqlHadrEndpoint` を使用してエンドポイントを開始します。  
  
###  <a name="PShellExample"></a> 例 (PowerShell)  
 次の PowerShell コマンドでは、SQL Server のインスタンス (*Machine*\\*Instance*) にデータベース ミラーリング エンドポイントを作成します。 このエンドポイントはポート 5022 を使用します。  
  
> [!IMPORTANT]  
>  この例を使用できるのは、現在データベース ミラーリング エンドポイントが存在しないサーバー インスタンスのみです。  
  
```powershell
# Create the endpoint.  
$endpoint = New-SqlHadrEndpoint MyMirroringEndpoint -Port 5022 -Path SQLSERVER:\SQL\Machine\Instance  
  
# Start the endpoint  
Set-SqlHadrEndpoint -InputObject $endpoint -State "Started"
```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **データベース ミラーリング エンドポイントを構成するには**  
  
-   [Windows 認証でのデータベース ミラーリング エンドポイントを作成する &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [データベース ミラーリング エンドポイントで着信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [サーバー ネットワーク アドレスの指定 &#40;データベース ミラーリング&#41;](../../database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [可用性レプリカを追加または変更する場合のエンドポイント URL の指定 &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **データベース ミラーリング エンドポイントに関する情報を表示するには**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
## <a name="see-also"></a>参照  
 [可用性グループの作成 &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)   
 [AlwaysOn 可用性グループ&#40;SQL Server の概要&#41;](overview-of-always-on-availability-groups-sql-server.md)  
