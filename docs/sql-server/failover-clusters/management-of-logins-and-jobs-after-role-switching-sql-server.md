---
title: 役割の交代後のログインとジョブの管理 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- role switching [SQL Server]
ms.assetid: fc2fc949-746f-40c7-b5d4-3fd51ccfbd7b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2887cfe969afd8739b15646efb8ee4700c8affff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063851"
---
# <a name="management-of-logins-and-jobs-after-role-switching-sql-server"></a>役割の交代後のログインとジョブの管理 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの高可用性ソリューションまたは災害復旧ソリューションを展開する場合、 **master** 内のデータベースまたは **msdb** データベースに格納されている関連情報を再現することが重要です。 通常、関連情報には、プライマリ/プリンシパル データベースのジョブおよびデータベースへの接続に必要なユーザーまたはプロセスのログインが含まれます。 セカンダリ/ミラー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の任意のインスタンスでこの情報を複製する必要があります。 可能であれば、役割の交代後に、プログラムで新しいプライマリ/プリンシパル データベースに情報を再現することが最善の方法です。  
  
## <a name="logins"></a>Login  
 データベースのコピーをホストするすべてのサーバー インスタンスで、プリンシパル データベースにアクセスする権限を持つログインを再現する必要があります。 プライマリ/プリンシパルの役割が交代すると、新しいプリンシパル/プライマリ サーバー インスタンスにログインが存在するユーザーのみが新しいプリンシパル/プライマリ データベースにアクセスできます。 ログインが新しいプライマリ/プリンシパル サーバー インスタンスで定義されていないユーザーは孤立して、データベースにアクセスできません。  
  
 ユーザーが孤立している場合は、新しいプライマリ/プリンシパル サーバー インスタンスでログインを作成し、 [sp_change_users_login](../../relational-databases/system-stored-procedures/sp-change-users-login-transact-sql.md)を実行します。 詳細については、「 [孤立ユーザーのトラブルシューティング &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)を実行します。  
  
###  <a name="SSauthentication"></a> SQL Server 認証またはローカル Windows ログインを使用するアプリケーションのログイン  
 アプリケーションで SQL Server 認証またはローカル Windows ログインを使用している場合、SID が一致しないと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のリモート インスタンスでアプリケーションのログインを解決できないことがあります。 SID が一致しないと、ログインはリモート サーバー インスタンスの孤立ユーザーになります。 この問題は、アプリケーションがフェールオーバー後にミラー化されたデータベースまたはログ配布データベース、またはバックアップから初期化されたレプリケーション サブスクライバー データベースに接続すると発生する可能性があります。  
  
 この問題を防ぐために、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のリモート インスタンスによってホストされているデータベースを使用するようにアプリケーションをセットアップする場合、予防策を講じることをお勧めします。 予報策として、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカル インスタンスから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のリモート インスタンスにログインとパスワードを転送する必要があります。 この問題を回避する方法の詳細については、サポート技術情報の記事 918992「[SQL Server のインスタンス間でログインおよびパスワードを転送する方法](https://support.microsoft.com/kb/918992/)」を参照してください。  
  
> [!NOTE]  
>  この問題は、さまざまなコンピューターの Windows ローカル アカウントに影響します。 ただし、各コンピューターの SID は同じであるため、この問題はドメイン アカウントでは発生しません。  
  
 詳細については、「 [Orphaned Users with Database Mirroring and Log Shipping](https://blogs.msdn.com/b/sqlserverfaq/archive/2009/04/13/orphaned-users-with-database-mirroring-and-log-shipping.aspx) 」(データベース ミラーリングとログ配布での孤立ユーザー) (データベース エンジンのブログ) を参照してください。  
  
## <a name="jobs"></a>ジョブ  
 バックアップ ジョブなどのジョブでは、特別な考慮が必要になります。 通常は、役割の交代後、データベース所有者またはシステム管理者が、新しいプライマリ/プリンシパル データベース用にジョブを再作成する必要があります。  
  
 元のプライマリ/プリンシパル サーバー インスタンスが使用できる場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のそのインスタンスで元のジョブを削除する必要があります。 現在のミラー データベースのジョブは RESTORING 状態であるため失敗し、使用できなくなります。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンスを、別のドライブ文字などを使用して別に構成できます。 パートナーごとのジョブは、このような違いを考慮する必要があります。  
  
## <a name="see-also"></a>参照  
 [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [孤立ユーザーのトラブルシューティング &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)  
  
  
