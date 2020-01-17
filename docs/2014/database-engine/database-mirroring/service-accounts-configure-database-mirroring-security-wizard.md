---
title: サービス アカウント (データベース ミラーリング セキュリティ構成ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.serviceaccounts.f1
ms.assetid: d58d8f93-7888-4d66-af4d-969ef6a2dbee
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 69877c6a20e37e012925185d0b807e9579066e35
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754394"
---
# <a name="service-accounts-configure-database-mirroring-security-wizard"></a>[サービス アカウント] (データベース ミラーリング セキュリティ構成ウィザード)
  Windows 認証でサーバー インスタンスが別のアカウントを使用している場合に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のサービス アカウントを指定します。 これらのサービス アカウントは、すべて (同じドメインまたは信頼関係のあるドメインの) ドメイン アカウントである必要があります。  
  
 すべてのサーバー インスタンスが同じアカウントを使用している場合、または証明書ベースの認証を使用している場合、フィールドは空のままにします。 **[完了]** をクリックするだけで、現在のウィザードのアカウントに基づいてアカウントが自動的に構成されます。  
  
> [!IMPORTANT]  
>  サーバー インスタンスのデータベース ミラーリング エンドポイントで証明書を使用するように構成されている場合は、サービス アカウント フィールドをすべて空にする必要があります。  
  
 **SQL Server Management Studio を使用してデータベース ミラーリングを構成するには**  
  
-   [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [データベース ミラーリング セキュリティ構成ウィザードの起動 &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>および  
 **プリンシパル**  
 プリンシパル サーバー インスタンスのサービス アカウントを指定します。 ドメイン名を大文字で入力します。  
  
 *DOMAINNAME*\\*username*  
  
 **ミラー**  
 ミラー サーバー インスタンスのサービス アカウントを指定します。 ドメイン名を大文字で入力します。  
  
 *DOMAINNAME*\\*username*  
  
 **ミラーリング監視サーバー**  
 ミラーリング監視サーバー インスタンスのサービス アカウントを指定します。 ドメイン名を大文字で入力します。  
  
 *DOMAINNAME*\\*username*  
  
## <a name="see-also"></a>関連項目  
 [データベース プロパティ &#40;[ミラーリング] ページ&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [データベース ミラーリング モニターの起動 &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [データベース ミラーリング &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [ログイン アカウントのデータベース ミラーリングまたは AlwaysOn 可用性グループ セットアップ&#40;SQL Server&#41;](set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
  
