---
title: データベース ミラーリングの設定 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
ms.assetid: da45efed-55eb-4c71-be34-ac2589dfce8d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c6b7fcdc3f50b941feac4958daa6dad49fde9eac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754452"
---
# <a name="setting-up-database-mirroring-sql-server"></a>データベース ミラーリングの設定 (SQL Server)
  ここでは、データベース ミラーリングを設定するための前提条件、推奨事項、および手順について説明します。 データベース ミラーリングの概要については、「 [データベース ミラーリング &#40;SQL Server&#41;](database-mirroring-sql-server.md)」を参照してください。  
  
> [!IMPORTANT]  
>  構成はパフォーマンスに影響する場合があるので、データベース ミラーリングの構成はピーク タイム以外の時間に行うことをお勧めします。  
  
 
  
##  <a name="PrepareInstances"></a> ミラー サーバーをホストするサーバー インスタンスの準備  
 各データベース ミラーリング セッションで、以下を実行します。  
  
1.  プリンシパル サーバー、ミラー サーバー、およびミラーリング監視サーバー (存在する場合) は、別々のホスト システムにある別々のサーバー インスタンスによってホストされる必要があります。 サーバー インスタンスは、それぞれがデータベース ミラーリング エンドポイントを必要とします。 データベース ミラーリング エンドポイントを作成する必要がある場合は、他のサーバー インスタンスもそのエンドポイントにアクセス可能であることを確認します。  
  
     サーバー インスタンスによりデータベースのミラーリングに使用される認証の形式は、データベース ミラーリング エンドポイントのプロパティで指定します。 データベース ミラーリングのトランスポートには、Windows 認証と証明書ベースの認証の 2 種類のセキュリティを使用できます。 詳細については、次を参照してください。[データベース ミラーリングと AlwaysOn 可用性グループのトランスポート セキュリティ&#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)します。  
  
     ネットワーク アクセスの要件は、次に示すように、認証の形式に固有です。  
  
    -   **Windows 認証を使用する場合**  
  
         サーバー インスタンスが別のドメイン ユーザー アカウントで実行されている場合、それぞれに他方のインスタンスの **master** データベースのログインが必要になります。 ログインが存在しない場合は、作成する必要があります。 詳細については、「 [Windows 認証を使用してデータベース ミラーリング エンドポイントへのネットワーク アクセスを許可する &#40;SQL Server&#41;](../database-mirroring-allow-network-access-windows-authentication.md)」を参照してください。  
  
    -   **証明書を使用する場合**  
  
         あるサーバー インスタンスのデータベース ミラーリングで証明書による認証を有効にするには、システム管理者は、各サーバー インスタンスが発信接続と着信接続の両方で証明書を使用するように構成する必要があります。 この場合、発信接続を最初に構成する必要があります。 詳細については、「[データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)」を参照してください。  
  
2.  すべてのデータベース ユーザーのログインが、ミラー サーバーに存在するようにします。 詳細については、次を参照してください。[データベース ミラーリングまたは AlwaysOn 可用性グループには、ログイン アカウントを設定&#40;SQL Server&#41;](set-up-login-accounts-database-mirroring-always-on-availability.md)します。  
  
3.  ミラー データベースをホストするサーバー インスタンスで、ミラー化されたデータベースで必要な残りの環境を設定します。 詳細については、「 [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)」を参照してください。  
  
##  <a name="EstablishUsingWinAuthentication"></a> 概要: データベース ミラーリング セッションの確立  
 ミラーリング セッションを確立するための基本手順を次に示します。  
  
1.  次のバックアップを復元することで、ミラー データベースを作成します。すべての復元操作で RESTORE WITH NORECOVERY を使用します。  
  
    1.  プリンシパル データベースのバックアップ作成時に、プリンシパル データベースで完全復元モデルが既に使用されていたことを確認した後、プリンシパル データベースの完全バックアップを復元します。 ミラー データベースとプリンシパル データベースの名前は同じである必要があります。  
  
    2.  完全バックアップの復元後に、データベースの差分バックアップを作成している場合は、最新の差分バックアップを復元します。  
  
    3.  データベースの完全バックアップまたは差分バックアップの作成後に行われたログ バックアップをすべて復元します。  
  
     詳細については、「 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)」を参照してください。  
  
    > [!IMPORTANT]  
    >  プリンシパル データベースのバックアップを作成してから、可能な限り早い時点に残りの設定手順を完了します。 パートナー上でミラーリングを開始するには、元のデータベースの現在のログ バックアップを作成し、ミラー データベースになるデータベースに復元しておく必要があります。  
  
2.  データベース ミラーリングは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] またはデータベース ミラーリング ウィザードを使用して設定できます。 詳細については、以下のいずれかを参照してください。  
  
    -   [Windows 認証を使用してデータベース ミラーリング セッションを確立する方法 &#40;Transact-SQL&#41;](database-mirroring-establish-session-windows-authentication.md)  
  
    -   [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
3.  既定ではセッションでのトランザクションの安全性が "完全" に設定され (SAFETY が FULL に設定された状態)、同期セッションが自動フェールオーバーを伴わない高い安全性モードで開始されます。 セッションは、次のように自動フェールオーバーを伴う高い安全性モードか、非同期の高パフォーマンス モードで実行するように再構成できます。  
  
    -   **自動フェールオーバーを伴う高い安全性モード**  
  
         自動フェールオーバーをサポートするために高い安全性モードでセッションを実行する場合は、ミラーリング監視サーバー インスタンスを追加します。  
  
         **ミラーリング監視サーバーを追加するには**  
  
        -   [Windows 認証を使用してデータベースのミラーリング監視を追加する &#40;Transact-SQL&#41;](add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
        -   [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
        > [!NOTE]  
        >  データベース所有者は、いつでもデータベースのミラーリング監視サーバーを無効にできます。 ミラーリング監視サーバーを無効にすると、ミラーリングの監視が行われない状態になり、自動フェールオーバーは行われません。  
  
    -   **高パフォーマンス モード**  
  
         自動フェールオーバーを行わず、高可用性よりパフォーマンスを重視する場合は、トランザクションの安全性を無効にします。 詳細については、「[データベース ミラーリング セッションでのトランザクションの安全性の変更 &#40;Transact-SQL&#41;](change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)」を参照してください。  
  
        > [!NOTE]  
        >  高パフォーマンス モードでは、WITNESS を OFF に設定する必要があります。 詳細については、「[クォーラム: データベースの可用性にミラーリング監視サーバーが与える影響 (データベース ミラーリング)](quorum-how-a-witness-affects-database-availability-database-mirroring.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] での Microsoft Windows 認証を使用したデータベース ミラーリングの設定例については、「[Windows 認証を使用したデータベース ミラーリングの設定の例 &#40;Transact-SQL&#41;](example-setting-up-database-mirroring-using-windows-authentication-transact-sql.md)」を参照してください。  
>   
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] での証明書ベースのセキュリティを使用したデータベース ミラーリングの設定例については、「[証明書を使用したデータベース ミラーリングの設定の例 &#40;Transact-SQL&#41;](example-setting-up-database-mirroring-using-certificates-transact-sql.md)」を参照してください。  
  
 
  
##  <a name="InThisSection"></a> トピックの内容  
 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)  
 中断されたセッションを再開する前に、ミラー データベースを作成したりミラー データベースを準備するための手順についてまとめています。 また、操作方法に関するトピックへのリンクも示します。  
  
 [サーバー ネットワーク アドレスの指定 &#40;データベース ミラーリング&#41;](specify-a-server-network-address-database-mirroring.md)  
 サーバー ネットワーク アドレスの構文、そのアドレスによってサーバー インスタンスのデータベース ミラーリング エンドポイントがどのように識別されるか、およびシステムの完全修飾ドメイン名を検索する方法について説明します。  
  
 [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
 データベース ミラーリング セキュリティ構成ウィザードを使用してデータベース ミラーリングを開始する方法について説明します。  
  
 [Windows 認証を使用してデータベース ミラーリング セッションを確立する方法 &#40;Transact-SQL&#41;](database-mirroring-establish-session-windows-authentication.md)  
 データベース ミラーリングを設定するための [!INCLUDE[tsql](../../includes/tsql-md.md)] の手順について説明します。  
  
 [例:Windows 認証を使用したデータベース ミラーリングの設定 &#40;Transact-SQL&#41;](example-setting-up-database-mirroring-using-windows-authentication-transact-sql.md)  
 Windows 認証を使用してミラーリング監視サーバーを利用するデータベース ミラーリング セッションを作成する場合に必要なすべての段階の例を示します。  
  
 [例:証明書を使用したデータベース ミラーリングの設定 &#40;Transact-SQL&#41;](example-setting-up-database-mirroring-using-certificates-transact-sql.md)  
 証明書ベースの認証を使用してミラーリング監視サーバーを利用するデータベース ミラーリング セッションを作成する場合に必要なすべての段階の例を示します。  
  
 [ログイン アカウントのデータベース ミラーリングまたは AlwaysOn 可用性グループ セットアップ&#40;SQL Server&#41;](set-up-login-accounts-database-mirroring-always-on-availability.md)  
 ローカル サーバー インスタンスと異なるアカウントを使用しているリモート サーバー インスタンスのログインの作成について説明します。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **SQL Server Management Studio**  
  
-   [データベース ミラーリング セキュリティ構成ウィザードの起動 &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
-   [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
 **Transact-SQL**  
  
-   [Windows 認証を使用してデータベース ミラーリング エンドポイントへのネットワーク アクセスを許可する &#40;SQL Server&#41;](../database-mirroring-allow-network-access-windows-authentication.md)  
  
-   [データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md)  
  
-   [データベース ミラーリング エンドポイントで着信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Windows 認証を使用してデータベース ミラーリング セッションを確立する方法 &#40;Transact-SQL&#41;](database-mirroring-establish-session-windows-authentication.md)  
  
-   [Windows 認証を使用してデータベースのミラーリング監視を追加する &#40;Transact-SQL&#41;](add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
-   [TRUSTWORTHY プロパティを使用するようにミラー データベースを設定する方法 &#40;Transact-SQL&#41;](set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)  
  
 **Transact-SQL/SQL Server Management Studio**  
  
-   [サーバー インスタンスのアップグレード時に、ミラー化されたデータベースのダウンタイムを最小化する方法](upgrading-mirrored-instances.md)  
  
-   [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [データベース ミラーリング構成のトラブルシューティング &#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)  
  
 
  
## <a name="see-also"></a>参照  
 [データベース ミラーリング &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [データベース ミラーリング: 相互運用性と共存 &#40;SQL Server&#41;](database-mirroring-interoperability-and-coexistence-sql-server.md)   
 [データベース ミラーリングと AlwaysOn 可用性グループのトランスポート セキュリティ&#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)   
 [サーバー ネットワーク アドレスの指定 &#40;データベース ミラーリング&#41;](specify-a-server-network-address-database-mirroring.md)  
  
  
