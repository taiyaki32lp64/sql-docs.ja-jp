---
title: サブスクライバーのセキュリティ保護 | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], security
- Subscribers [SQL Server replication], security
- security [SQL Server replication], Subscribers
ms.assetid: c8f0d62a-8b5d-4a21-9aec-223da52bb708
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7c8f75360bb3eb4b304c2a56a150218e8f8c8eff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62960833"
---
# <a name="secure-the-subscriber"></a>サブスクライバーのセキュリティ保護
  マージ エージェントとディストリビューション エージェントはサブスクライバーに接続します。 これらの接続は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインまたは Windows ログインのコンテキスト下で行われます。 最低限必要な権限のみを与え、かつ、すべてのパスワードの格納を保護するという原則に従って、これらの各エージェントに対し適切なログインを提供することが重要です。 各エージェントに必要な権限の詳細については、「 [Replication Agent Security Model](replication-agent-security-model.md)」を参照してください。  
  
## <a name="distribution-agent"></a>ディストリビューション エージェント  
 サブスクリプションごとに 1 つのディストリビューション エージェント (パブリケーションの新規作成ウィザードで既定で作成される独立したエージェント)、またはパブリケーション データベースとサブスクリプション データベースのペアごとに 1 つのディストリビューション エージェント (共有エージェント) があります。 T  
  
 プッシュ サブスクリプションの接続情報を指定する場合は、「[プッシュ サブスクリプションの作成](../create-a-push-subscription.md)」を参照してください。  
  
 プル サブスクリプションの接続情報を指定する場合は、「[プル サブスクリプションの作成](../create-a-pull-subscription.md)」を参照してください。  
  
## <a name="merge-agent"></a>[マージ エージェント]  
 マージ サブスクリプションごとにマージ エージェントがあり、パブリッシャーとサブスクライバーの両方に接続し、更新します。  
  
 プッシュ サブスクリプションの接続情報を指定する場合は、「[プッシュ サブスクリプションの作成](../create-a-push-subscription.md)」を参照してください。  
  
 プル サブスクリプションの接続情報を指定する場合は、「[プル サブスクリプションの作成](../create-a-pull-subscription.md)」を参照してください。  
  
## <a name="immediate-updating-subscriptions"></a>即時更新サブスクリプション  
 即時更新サブスクリプションを構成する場合は、パブリッシャーに接続する際のアカウントをサブスクライバーで指定します。 接続はサブスクライバーで起動されるトリガーによって使用され、サブスクライバーに変更を反映します。 接続の種類として、3 つのオプションがあります。  
  
-   レプリケーションが作成するリンク サーバー。構成時に指定した資格情報を使用して接続が行われます。  
  
-   レプリケーションによって作成されるリンク サーバー。サブスクライバーで変更を行うユーザーの資格情報を使用して接続を行います。  
  
-   定義済みのリンク サーバーまたはリモート サーバー。  
  
> [!IMPORTANT]  
>  接続情報を指定する場合は、ストアド プロシージャ [sp_link_publication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) を使用します。 サブスクリプションの新規作成ウィザードの **[更新可能なサブスクリプション用のログイン]** を使用して、 **sp_link_publication**を呼び出すこともできます。 特定の条件下で、サブスクライバーが [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Service Pack 1 (SP1) 以降を実行し、パブリッシャーがそれよりも前のバージョンを実行している場合、このストアド プロシージャは失敗する可能性があります。 このシナリオでストアド プロシージャが失敗する場合は、パブリッシャーを [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] SP1 以降にアップグレードしてください。  
  
 詳細については、「[トランザクション パブリケーションの更新可能なサブスクリプションの作成](../publish/create-an-updatable-subscription-to-a-transactional-publication.md)」および「[レプリケーションのセキュリティ設定の表示および変更](view-and-modify-replication-security-settings.md)」を参照してください。  
  
> [!IMPORTANT]  
>  接続用に指定するアカウントには、レプリケーションによってパブリケーション データベース内に作成されるビューのデータの挿入、更新、および削除だけを実行できる権限を与える必要があります。それ以外の権限は与えないでください。 各サブスクライバーで構成したアカウントに、**syncobj_** _\<HexadecimalNumber>_ の形式で名前が指定されたパブリケーション データベース内のビューに対する権限を与えます。  
  
## <a name="queued-updating-subscriptions"></a>キュー更新サブスクリプション  
 キュー更新サブスクリプションを構成する際には、セキュリティに関して、以下の 2 点に注意してください。  
  
-   各ディストリビューターには、キュー リーダー エージェントが 1 つしかありません。 ディストリビューターごとに、キュー更新サブスクリプションを有効にしたパブリケーションを 1 つだけ構成することをお勧めします。  
  
-   キュー リーダー エージェントは、ディストリビューター、パブリッシャー、および各サブスクライバーに接続します。  
  
    -   エージェントの実行とディストリビューターへの接続で使用するアカウントは、エージェントを作成する際に指定します (パブリケーションの新規作成ウィザードを使用する場合は、更新サブスクリプションを有効にしたパブリケーションを作成する際にエージェントが作成されます)。  
  
    -   エージェントがパブリッシャーに接続する際に使用するアカウントは、パブリッシャーのディストリビューションを構成する際に指定します。 エージェントの実行で使用する Windows アカウントか [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] アカウントを指定してください。  
  
    -   エージェントがサブスクライバーに接続する際に使用するアカウントは、サブスクリプションを作成する際に指定します。  
  
    > [!IMPORTANT]  
    >  サブスクライバーへの接続には [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用し、各サブスクライバーへの接続にはそれぞれ異なるアカウントを指定してください。 プル サブスクリプションを使用する場合は、レプリケーションによって、常に Windows 認証を使用するように接続が設定されます (プル サブスクリプションでは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証が必要なサブスクライバーのメタデータにレプリケーションからアクセスすることはできません)。 その場合、サブスクリプションを構成した後に、接続で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用するように変更してください。  
  
     詳細については、トランザクション パブリケーションに対して更新可能なサブスクリプションを作成する方法 (SQL Server Management Studio) および「[レプリケーションのセキュリティ設定の表示および変更](view-and-modify-replication-security-settings.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [SQL Server レプリケーションのセキュリティ](view-and-modify-replication-security-settings.md)  
  
  
