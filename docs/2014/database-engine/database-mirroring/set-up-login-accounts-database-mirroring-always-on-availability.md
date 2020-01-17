---
title: 設定すると、ログイン アカウントのデータベース ミラーリングまたは AlwaysOn 可用性グループ (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- logins [SQL Server], database mirroring
ms.assetid: e9f5287b-1325-4cda-88a6-19eaaa52a652
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5fd397349bc3fa3ed7f69e9e1293415ea96fc75d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754311"
---
# <a name="set-up-login-accounts-for-database-mirroring-or-alwayson-availability-groups-sql-server"></a>データベース ミラーリングまたは AlwaysOn 可用性グループのログイン アカウントの設定 (SQL Server)
  2 つのサーバー インスタンスが互いにもう一方の [データベース ミラーリング エンドポイント](the-database-mirroring-endpoint-sql-server.md) であるポイントに接続するには、各インスタンスのログイン アカウントがもう一方のインスタンスにアクセスできる必要があります。 また、各ログイン アカウントには、他方のインスタンスのデータベース ミラーリング エンドポイントへの接続権限も必要です。  
  
 この要件による影響は、サーバー インスタンスを同じドメイン ユーザー アカウントとして実行しているかどうかによって異なります。  
  
-   同じドメイン ユーザー アカウントでサーバー インスタンスを実行した場合は、自動的に両方の **マスター** データベースに正しいユーザー ログインが存在します。 このため、データベース ミラーリングと AlwaysOn 可用性グループのセキュリティ構成が単純化されます。  
  
-   異なるユーザー アカウントとしてサーバー インスタンスを実行している場合は、プリンシパル サーバーまたはプライマリ レプリカをホストするサーバー インスタンスに対するユーザー ログインを、ミラー サーバーをホストするサーバー インスタンスまたはセカンダリ レプリカをホストするすべてのサーバー インスタンスに手動で再現する必要があります。 詳細については、この後の「 [異なるアカウントのログインの作成](#CreateLogin) 」および「 [接続権限の許可](#GrantConnect)」を参照してください。  
  
    > [!IMPORTANT]  
    >  より安全な環境を作成するには、各サーバー インスタンスに対して個別のドメイン アカウントを使用することを検討してください。  
  
##  <a name="CreateLogin"></a> 異なるアカウントのログインの作成  
 2 つのサーバー インスタンスが異なるアカウントで実行される場合、システム管理者は CREATE LOGIN [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用して、リモート インスタンスのスタートアップ サービス アカウント用にログインを作成する必要があります。このログインは、各サーバー インスタンスに作成します。 詳細については、「[CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)」を参照してください。  
  
> [!IMPORTANT]  
>  ドメイン アカウント以外で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行する場合、証明書を使用する必要があります。 詳細については、この後の「 [データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)」を参照してください。  
  
 たとえば、loginA で実行されるサーバー インスタンス sqlA の場合、loginB で実行されるサーバー インスタンス sqlB に接続するには、loginA が sqlB に存在し、かつ loginB が sqlA に存在する必要があります。 また、データベース ミラーリング セッションにミラーリング監視サーバー インスタンス (sqlC) が含まれ、3 つのサーバー インスタンスがそれぞれ異なるドメイン アカウントで実行される場合は、以下のログインを作成する必要があります。  
  
|インスタンス|ログインを作成し接続権限を許可する対象|  
|--------------------|--------------------------------------------------------------|  
|sqlA|sqlB と sqlC|  
|sqlB|sqlA と sqlC|  
|sqlC|sqlA と sqlB|  
  
> [!NOTE]  
>  ドメイン ユーザーではなくコンピューター アカウントを使用することにより、ネットワーク サービス アカウントで接続できます。 コンピューター アカウントを使用する場合は、そのアカウントを他方のサーバー インスタンスにユーザーとして追加する必要があります。  
  
##  <a name="GrantConnect"></a> 接続権限の許可  
 サーバー インスタンスでログインを作成した後、サーバー インスタンスのデータベース ミラーリング エンドポイントに接続するための権限をそのログインに許可する必要があります。 システム管理者は、GRANT [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用して接続権限を許可します。 詳細については、「 [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)と共に使用できるように構成する方法について説明します。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [ログインの作成](../../relational-databases/security/authentication-access/create-a-login.md)  
  
-   [Windows 認証を使用してデータベース ミラーリング エンドポイントへのネットワーク アクセスを許可する &#40;SQL Server&#41;](../database-mirroring-allow-network-access-windows-authentication.md).  
  
-   [データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [データベース ミラーリング構成のトラブルシューティング &#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)   
 [AlwaysOn 可用性グループの構成のトラブルシューティングを行う&#40;SQL Server&#41;](../availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
