---
title: "ディストリビューターのセキュリティ保護 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [SQL Server replication], Distributors
- Distributors [SQL Server replication], security
ms.assetid: 76d78229-0ff2-4aa4-9b4e-ad97534c5296
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0455938e9a9b0c017da7f8546821a9f318a85d6b
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="secure-the-distributor"></a>ディストリビューターのセキュリティ保護
  レプリケーション エージェントのうち、ログ リーダー エージェント、スナップショット エージェント、キュー リーダー エージェント、ディストリビューション エージェント、およびマージ エージェントは、ディストリビューターに接続します。 最低限必要な権限のみを与え、かつすべてのパスワードの格納を保護するという原則に従って、これらの各エージェントに対し適切なログインを指定することは重要です。  
  
-   ログインとパスワードの管理の詳細については、「[レプリケーションのログインとパスワードの管理](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)」を参照してください。  
  
-   各エージェントで必要な権限の詳細については、「 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)」を参照してください。  
  
 ログインとパスワードの適切な管理に加えて、リモート サーバー リンク **repl_distributor** 、および **distributor_admin** アカウントのロールを理解することが重要です。  
  
## <a name="securing-the-connection-from-the-publisher-to-the-distributor"></a>パブリッシャーからディストリビューターへの接続の保護  
 管理用のストアド プロシージャをパブリッシャーで実行し、ディストリビューターで情報を更新するために必要な通信をサポートするため、レプリケーションでは、リモート サーバー **repl_distributor**が自動的に構成されます。 リモート サーバー エントリ **repl_distributor** は、ディストリビューション データベースがパブリッシャー インスタンス (ローカル ディストリビューター) 内に含まれるか、リモートの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス (リモート ディストリビューター) に存在するかにかかわらず、ディストリビューション データベースへの接続に使用されます。  
  
 ディストリビューション データベースがローカル インスタンスに含まれる場合は、ランダムなパスワードが生成され自動的に構成されます。 ディストリビューション データベースがリモート インスタンスにある場合は、パブリッシャーとディストリビューターのセットアップ時に管理者が共有パスワードを構成します。このパスワードは、 **repl_distributor** リンク上を流れるトラフィックの認証に使用されます。  
  
 ディストリビューターは、実行時にリモート サーバー エントリ **repl_distributor** を使用して、呼び出し元のサーバーがディストリビューターでパブリッシャーとして構成されていることを検証します。次に、パブリッシャーから渡されたパスワードを検証して、ストアド プロシージャがレプリケーション ストアド プロシージャであることを検証します。  
  
 セットアップ時にリモート サーバー エントリ **repl_distributor** に対して構成されたパスワードは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン **distributor_admin**と関連付けられます。このログインは、ディストリビューター上で固定サーバー ロール **sysadmin** に追加されます。 **distributor_admin** ログインは、ディストリビューターに接続するときに、レプリケーション ストアド プロシージャによって使用されます。  
  
> [!NOTE]  
>  **distributor_admin** のパスワードを手動で変更しないでください。 パスワードの変更は、必ず **sp_changedistributor_password** ストアド プロシージャか、 **の** [ディストリビューターのプロパティ] **または** [レプリケーション パスワードの更新] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]ダイアログ ボックスで行ってください。これにより、パスワードの変更がローカル パブリケーションに自動的に適用されます。  
  
## <a name="snapshot-folder-security"></a>スナップショット フォルダーのセキュリティ  
 スナップショット共有には、マージ エージェント (マージ レプリケーションの場合) またはディストリビューション エージェント (スナップショット レプリケーションまたはトランザクション レプリケーションの場合) の実行に使用するアカウントに読み取りアクセスが許可され、スナップショット エージェントの実行に使用するアカウントに書き込みアクセスが許可されていることを確認してください。 スナップショット フォルダーの詳細については、「[スナップショット フォルダーのセキュリティ保護](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レプリケーションのセキュリティ設定の表示および変更](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [セキュリティと保護 &#40;レプリケーション&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  