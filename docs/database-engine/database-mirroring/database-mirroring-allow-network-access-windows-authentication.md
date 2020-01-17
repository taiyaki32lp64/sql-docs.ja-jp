---
title: データベース ミラーリング - ネットワーク アクセスの許可 - Windows 認証 | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Windows authentication [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 28c8fec5-5feb-4c84-8d72-f2bd1ae3b40d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8dbae060ee2fa2714bc7fd624a1f3aafc80959ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951981"
---
# <a name="database-mirroring---allow-network-access---windows-authentication"></a>データベース ミラーリング - ネットワーク アクセスの許可 - Windows 認証
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  次のような条件下で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 2 つのインスタンスのデータベース ミラーリング エンドポイントに接続するために Windows 認証を使用するときは、ログイン アカウントを手動で構成する必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが (同じドメインまたは信頼関係のあるドメインの) 異なるドメイン アカウントでサービスとして実行される場合、各リモート サーバー インスタンス上の **master** に各アカウントのログインを作成する必要があります。また、そのログインには、エンドポイントに対する CONNECT 権限を与える必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスがネットワーク サービス アカウントとして実行される場合、各リモート サーバー インスタンス上の **master** に各ホスト コンピューター アカウント (*DomainName***\\***ComputerName$* ) のログインを作成する必要があります。また、そのログインには、エンドポイントに対する CONNECT アクセス許可を与える必要があります。 これは、ネットワーク サービス アカウントで実行されているサーバー インスタンスではホスト コンピューターのドメイン アカウントを使用して認証を行うためです。  
  
> [!NOTE]  
>  各サーバー インスタンスのエンドポイントが存在することを確認してください。 詳細については、「[Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)」を参照してください。  
  
### <a name="to-configure-logins-for-windows-authentication"></a>Windows 認証のログインを構成するには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各インスタンスのユーザー アカウントについて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の別のインスタンスでログインを作成します。 [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) ステートメントと FROM WINDOWS 句を使用します。  
  
     詳細については、「 [ログインの作成](../../relational-databases/security/authentication-access/create-a-login.md)」を参照してください。  
  
2.  ログイン ユーザーがエンドポイントにアクセスできるように、 [GRANT](../../t-sql/statements/grant-transact-sql.md) ステートメントを使用して、エンドポイントへの接続権限をそのログインに許可します。 エンドポイントへの接続権限の許可は、管理者には不要なので注意してください。  
  
     詳細については、「 [プリンシパルに対する権限の許可](../../relational-databases/security/authentication-access/grant-a-permission-to-a-principal.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] の例では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] というドメインに所属するユーザー アカウント `Otheruser` の `Adomain`ログインを作成します。 このユーザーには、 `Mirroring_Endpoint`という既存のデータベース ミラーリング エンドポイントへの接続権限を許可します。  
  
```  
USE master;  
GO  
CREATE LOGIN [Adomain\Otheruser] FROM WINDOWS;  
GO  
GRANT CONNECT on ENDPOINT::Mirroring_Endpoint TO [Adomain\Otheruser];  
GO  
```  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [データベース ミラーリングと AlwaysOn 可用性グループのトランスポート セキュリティ &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
