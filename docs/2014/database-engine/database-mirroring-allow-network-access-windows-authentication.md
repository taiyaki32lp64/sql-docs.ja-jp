---
title: データベースミラーリングエンドポイントへのネットワークアクセス
description: SQL Server のデータベースミラーリングエンドポイントへの windows 認証のネットワークアクセスを許可する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Windows authentication [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 28c8fec5-5feb-4c84-8d72-f2bd1ae3b40d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e40a1eead54fe9d00eaf099410260023229796d0
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228565"
---
# <a name="allow-network-access-to-a-database-mirroring-endpoint-using-windows-authentication-sql-server"></a>Windows 認証を使用してデータベース ミラーリング エンドポイントへのネットワーク アクセスを許可する (SQL Server)
  次のような条件下で、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の 2 つのインスタンスのデータベース ミラーリング エンドポイントに接続するために Windows 認証を使用するときは、ログイン アカウントを手動で構成する必要があります。  
  
-   
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスが (同じドメインまたは信頼関係のあるドメインの) 異なるドメイン アカウントでサービスとして実行される場合、各リモート サーバー インスタンス上の **master** に各アカウントのログインを作成する必要があります。また、そのログインには、エンドポイントに対する CONNECT 権限を与える必要があります。  
  
-   
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスがネットワーク サービス アカウントとして実行される場合、各リモート サーバー インスタンス上の *master*** に各ホスト コンピューター アカウント (\\DomainName******ComputerName$**) のログインを作成する必要があります。また、そのログインには、エンドポイントに対する CONNECT アクセス許可を与える必要があります。 これは、ネットワーク サービス アカウントで実行されているサーバー インスタンスではホスト コンピューターのドメイン アカウントを使用して認証を行うためです。  
  
> [!NOTE]  
>  各サーバー インスタンスのエンドポイントが存在することを確認してください。 詳細については、「[Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)」を参照してください。  
  
### <a name="to-configure-logins-for-windows-authentication"></a>Windows 認証のログインを構成するには  
  
1.  
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の各インスタンスのユーザー アカウントについて、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の別のインスタンスでログインを作成します。 
  [CREATE LOGIN](/sql/t-sql/statements/create-login-transact-sql) ステートメントと FROM WINDOWS 句を使用します。  
  
     詳細については、「 [ログインの作成](../relational-databases/security/authentication-access/create-a-login.md)」を参照してください。  
  
2.  ログイン ユーザーがエンドポイントにアクセスできるように、 [GRANT](/sql/t-sql/statements/grant-transact-sql) ステートメントを使用して、エンドポイントへの接続権限をそのログインに許可します。 エンドポイントへの接続権限の許可は、管理者には不要なので注意してください。  
  
     詳細については、「 [プリンシパルに対する権限の許可](../relational-databases/security/authentication-access/grant-a-permission-to-a-principal.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の [!INCLUDE[tsql](../includes/tsql-md.md)] の例では、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] というドメインに所属するユーザー アカウント `Otheruser` の `Adomain`ログインを作成します。 このユーザーには、 `Mirroring_Endpoint`という既存のデータベース ミラーリング エンドポイントへの接続権限を許可します。  
  
```  
USE master;  
GO  
CREATE LOGIN [Adomain\Otheruser] FROM WINDOWS;  
GO  
GRANT CONNECT on ENDPOINT::Mirroring_Endpoint TO [Adomain\Otheruser];  
GO  
```  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ &#40;SQL Server の概要&#41;](availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [データベースミラーリング &#40;SQL Server&#41;](database-mirroring/database-mirroring-sql-server.md)   
 [データベースミラーリングと AlwaysOn 可用性グループ &#40;SQL Server のトランスポートセキュリティ&#41;](database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [データベースミラーリングエンドポイント &#40;SQL Server&#41;](database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
