---
title: レプリケーション セキュリティの推奨事項 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], best practices
- security [SQL Server replication], between domains
- authentication [SQL Server replication]
- Internet [SQL Server replication], security
ms.assetid: 1ab2635d-0992-4c99-b17d-041d02ec9a7c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7db85ce6d63cd6c3eb458434357fa5a2d8127dec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63268672"
---
# <a name="replication-security-best-practices"></a>レプリケーション セキュリティの推奨事項
  レプリケーションでは、単一ドメインのイントラネットから、信頼できないドメイン間およびインターネット経由でデータにアクセスするアプリケーションに及ぶ分散環境でデータを移動します。 これらのさまざまな状況下でレプリケーション接続のセキュリティを確保するためには、推奨事項を理解することが重要です。  
  
 次の情報は、すべての環境のレプリケーションに関連します。  
  
-   レプリケーション トポロジ内のコンピューター間の接続を、仮想プライベート ネットワーク (VPN)、SSL (Secure Sockets Layer)、IPSEC (IP Secrity) などの業界標準の方式を使用して暗号化する。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。 VPN と SSL を使用したインターネット経由のデータのレプリケーションについては、「 [Securing Replication Over the Internet](securing-replication-over-the-internet.md)」を参照してください。  
  
     SSL を使用してレプリケーション トポロジのコンピューター間の接続をセキュリティで保護する場合、各レプリケーション エージェントの **-EncryptionLevel** パラメーターに値 **1** または **2** を指定します (値 **2** が推奨値です)。 値 **1** は、暗号化を使用していますが、SSL サーバー証明書が信頼されている発行者によって署名されていることをエージェントが検証していないことを示します。値 **2** は、証明書が検証されていることを示します。 エージェント パラメーターは、エージェント プロファイルおよびコマンド ラインで指定できます。 詳細については、以下をご覧ください。  
  
    -   [レプリケーション エージェント プロファイルの操作](../agents/replication-agent-profiles.md)  
  
    -   [レプリケーション エージェント コマンド プロンプト パラメーターを表示および変更する &#40;SQL Server Management Studio&#41;](../agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../concepts/replication-agent-executables-concepts.md)  
  
-   異なる Windows アカウントで各レプリケーション エージェントを実行し、すべてのレプリケーション エージェント接続に対して Windows 認証を使用する。 アカウントの指定の詳細については、「[レプリケーションのログインとパスワードの管理](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)」を参照してください。  
  
-   各エージェントに必要な権限のみを許可する。 詳細については、「 [Replication Agent Security Model](replication-agent-security-model.md)」の「エージェントに必要な権限」を参照してください。  
  
-   マージ エージェントとディストリビューション エージェントのすべてのアカウントがパブリケーション アクセス リスト (PAL) に含まれているかどうかを確認する。 詳細については、「[パブリッシャーのセキュリティ保護](secure-the-publisher.md)」を参照してください。  
  
-   最小特権の原則に従って、PAL 内のアカウントに、レプリケーション タスクを実行するために必要な権限のみを許可する。 レプリケーションに必要のない固定サーバー ロールにはログインを追加しないでください。  
  
-   すべてのマージ エージェントおよびディストリビューション エージェントによる読み取りアクセスを許可するようにスナップショット共有を構成する。 パラメーター化されたフィルターを使用するパブリケーションのスナップショットの場合は、適切なマージ エージェント アカウントへのアクセスのみを許可するように各フォルダーを設定してください。  
  
-   スナップショット エージェントによる書き込みアクセスを許可するようにスナップショット共有を構成する。  
  
-   プル サブスクリプションを使用する場合は、スナップショット フォルダーにローカル パスではなく、ネットワーク共有を使用する。  
  
 レプリケーション トポロジに、同じドメイン内に存在しないコンピューター、または相互に信頼関係を持たないドメインに存在するコンピューターが含まれている場合、エージェントが確立する接続には Windows 認証または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用できます (ドメインの詳細については、Windows のマニュアルを参照してください)。 セキュリティの推奨方法としては、Windows 認証の使用をお勧めします。  
  
-   Windows 認証を使用するには  
  
    -   適切なノードで、各エージェントのドメイン アカウントではない、ローカルの Windows アカウントを追加します (各ノードでは同じ名前とパスワードを使用します)。 たとえば、プッシュ サブスクリプションのディストリビューション エージェントをディストリビューターで実行し、ディストリビューターとサブスクライバーに接続しているとします。 この場合、ディストリビューション エージェントの Windows アカウントを、ディストリビューターおよびサブスクライバーに追加する必要があります。  
  
    -   指定されたエージェント (たとえば、サブスクリプションのディストリビューション エージェント) が、各コンピューターで同じアカウントを使用して実行されているかどうかを確認します。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用するには  
  
    -   適切なノードで、各エージェントのローカルの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] アカウントを追加します (各ノードで同じ名前とパスワードを使用します)。 たとえば、プッシュ サブスクリプションのディストリビューション エージェントをディストリビューターで実行し、ディストリビューターとサブスクライバーに接続しているとします。 この場合、ディストリビューション エージェントの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] アカウントを、ディストリビューターおよびサブスクライバーに追加する必要があります。  
  
    -   指定されたエージェント (たとえば、サブスクリプションのディストリビューション エージェント) が、各コンピューターで同じアカウントを使用して接続しているかどうかを確認します。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証が必要な状況では、多くの場合、UNC スナップショット共有へのアクセスは実行できません (たとえば、アクセスがファイアウォールでブロックされます)。 この場合は、ファイル転送プロトコル (FTP) を使用して、スナップショットをサブスクライバーに転送できます。 詳細については、「[FTP によるスナップショットの転送](../transfer-snapshots-through-ftp.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [インターネット経由のレプリケーション](../replication-over-the-internet.md)   
 [サブスクライバーのセキュリティ保護](secure-the-subscriber.md)   
 [ディストリビューターのセキュリティ保護](secure-the-distributor.md)   
 [パブリッシャーのセキュリティ保護](secure-the-publisher.md)   
 [SQL Server レプリケーションのセキュリティ](view-and-modify-replication-security-settings.md)  
  
  
