---
title: Powershell:可用性グループのデータベース ミラーリング エンドポイント
description: PowerShell を利用し、Always On 可用性グループのデータベース ミラーリング エンドポイントを作成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
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
ms.openlocfilehash: d8cc91d628c365d4f9092ca24a8b4df06f17adf2
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252896"
---
# <a name="create-a-database-mirroring-endpoint-for-an-availability-group-using-powershell"></a>PowerShell を利用し、可用性グループのデータベース ミラーリング エンドポイントを作成する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックでは、PowerShell を使用して、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で使用するデータベース ミラーリング エンドポイントを作成する方法について説明します。  
  

  
##  <a name="Permissions"></a> Permissions  
 CREATE ENDPOINT 権限、または sysadmin 固定サーバー ロールのメンバーシップが必要です。 詳細については、「 [GRANT (エンドポイントの権限の許可) &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)」を参照してください。  

> [!IMPORTANT]  
>  RC4 アルゴリズムは非推奨とされます。 [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)] AES を使用することをお勧めします。  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
 **データベース ミラーリング エンドポイントを作成するには**  
  
1.  ディレクトリ変更コマンド (**cd**) を使用して、データベース ミラーリング エンドポイントを作成するサーバー インスタンスに接続します。  
  
2.  **New-SqlHadrEndpoint** コマンドレットを使用してエンドポイントを作成し、その後 **Set-SqlHadrEndpoint** を使用してエンドポイントを開始します。  
  
###  <a name="PShellExample"></a> 例 (PowerShell)  
 次の PowerShell コマンドでは、SQL Server のインスタンス (*Machine*\\*Instance*) にデータベース ミラーリング エンドポイントを作成します。 このエンドポイントはポート 5022 を使用します。  
  
> [!IMPORTANT]  
>  この例を使用できるのは、現在データベース ミラーリング エンドポイントが存在しないサーバー インスタンスのみです。  
  
```  
# Create the endpoint.  
$endpoint = New-SqlHadrEndpoint MyMirroringEndpoint -Port 5022 -Path SQLSERVER:\SQL\Machine\Instance  
  
# Start the endpoint  
Set-SqlHadrEndpoint -InputObject $endpoint -State "Started"  
  
```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **データベース ミラーリング エンドポイントを構成するには**  
  
-   [Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [データベース ミラーリング エンドポイントで着信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [サーバー ネットワーク アドレスの指定 &#40;データベース ミラーリング&#41;](../../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [可用性レプリカを追加または変更する場合のエンドポイント URL の指定 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **データベース ミラーリング エンドポイントに関する情報を表示するには**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [可用性グループの作成 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)   
 [Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
