---
title: 'セキュリティの構成ウィザード: サーバーの選択'
descriptoin: Describes the properties found on the the 'Choose Servers' page of the 'Configure Database Mirroring Security Wizard'.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.choosesrvrs.f1
ms.assetid: 59e23ff3-d7ee-4e32-9629-0b54d3a258f7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cfb2396e97c4cceee534472c07c285aa2a8a371e
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822314"
---
# <a name="configure-database-mirroring-wizard-choose-servers-to-configure"></a>データベース ミラーリング構成ウィザード: 構成するサーバーを選択する 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このページを使用すると、構成するサーバー インスタンスを指定できます。 ウィザードを進めるには、少なくとも 1 つのサーバー インスタンスを選択する必要があります。  
  
 サーバー インスタンスのチェック ボックスをオフにすると、このウィザードでは、そのサーバーを変更できなくなります。 ただし、他のサーバー インスタンスの構成の一部としてこのインスタンスの情報を入力し、保存するように求められます。 たとえば、ミラーリング監視サーバー インスタンスのチェック ボックスをオフにした場合でも、ミラーリング監視サーバーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントを入力するように求められます。これは、プリンシパル サーバー インスタンスおよびミラー サーバー インスタンスに保存するセキュリティ構成の中で、このアカウントのログインを作成する必要があるためです。  
  
 **SQL Server Management Studio を使用してデータベース ミラーリングを構成するには**  
  
-   [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [データベース ミラーリング セキュリティ構成ウィザードの起動 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>オプション  
 **[プリンシパル サーバー インスタンス]**  
 プリンシパル サーバーのセキュリティを構成する場合に選択します。  
  
 **[ミラー サーバー インスタンス]**  
 ミラー サーバーのセキュリティを構成する場合に選択します。  
  
 **[ミラーリング監視サーバー インスタンス]**  
 ミラーリング監視サーバー (存在する場合) のセキュリティを構成する場合に選択します。  
  
## <a name="see-also"></a>参照  
 [データベース プロパティ &#40;[ミラーリング] ページ&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
