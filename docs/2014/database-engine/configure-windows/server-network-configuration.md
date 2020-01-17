---
title: サーバー ネットワークの構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Named Pipes [SQL Server], configuring
- connections [SQL Server], server network configuration
- Database Engine [SQL Server], network configurations
- server network configuration [SQL Server]
- protocols [SQL Server], choosing
- ports [SQL Server], changing
- server configuration [SQL Server]
ms.assetid: 890c09a1-6dad-4931-aceb-901c02ae34c5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3545732db24865e47853b023233a127695ada894
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62809482"
---
# <a name="server-network-configuration"></a>サーバー ネットワークの構成
  サーバー ネットワークの構成作業には、プロトコルの有効化、プロトコルで使用されるポートまたはパイプの変更、暗号化の構成、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスの構成、ネットワーク上での [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]の公開または非表示、サーバー プリンシパル名の登録などがあります。 ほとんどの場合、サーバー ネットワークの構成を変更する必要はありません。 特殊なネットワーク要件がある場合は、サーバー ネットワーク プロトコルのみを再構成します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のネットワーク構成は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して行います。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の場合は、その製品に付属するサーバー ネットワーク ユーティリティを使用します。  
  
## <a name="protocols"></a>プロトコル  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって使用されるプロトコルを有効または無効にし、そのプロトコルで使用できるオプションを構成します。 有効にできるプロトコルの数は 1 つ以上です。 また、クライアントが使用するすべてのプロトコルを有効にする必要があります。 サーバーには、どのプロトコルを使用してもアクセスできます。 使用する必要があるプロトコルの選択については、「[サーバー ネットワーク プロトコルの有効化または無効化](enable-or-disable-a-server-network-protocol.md)を参照してください。  
  
### <a name="changing-a-port"></a>ポートの変更  
 指定したポートでリッスンするように TCP/IP プロトコルを構成できます。 既定では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の既定のインスタンスは TCP ポート 1433 でリッスンします。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] と [!INCLUDE[ssEW](../../includes/ssew-md.md)] の名前付きインスタンスは、動的ポートを使用するように構成されています。 つまり、これらのインスタンスでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの開始時に、使用可能なポートが選択されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスは、クライアントが接続時にポートを識別するのに役立ちます。  
  
 動的ポート向けに構成されている場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって使用されるポートは、起動のたびに変更される可能性があります。 ファイアウォールを通じて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって使用されるポートを開く必要があります。 また、特定のポートを使用するように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を構成して、サーバーへの通信を許可するようにファイアウォールを構成できます。 詳細については、「[特定の TCP ポートで受信待ちするようにサーバーを構成する方法 &#40;SQL Server 構成マネージャー&#41;](configure-a-server-to-listen-on-a-specific-tcp-port.md)」を参照してください。  
  
### <a name="changing-a-named-pipe"></a>名前付きパイプの変更  
 指定した名前付きパイプでリッスンするように名前付きパイプ プロトコルを構成できます。 既定では、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] の既定のインスタンスはパイプ \\\\.\pipe\sql\query で、名前付きインスタンスの場合はパイプ \\\\.\pipe\MSSQL$ *\<instancename>* \sql\query でそれぞれリッスンします。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] がリッスンできる名前付きパイプは 1 つのみですが、必要に応じてパイプの名前を変更できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスは、クライアントが接続時にパイプを識別するのに役立ちます。 詳細については、「[代替パイプをリッスンするサーバーの構成  &#40;SQL Server 構成マネージャー&#41;](configure-a-server-to-listen-on-an-alternate-pipe.md)」を参照してください。  
  
## <a name="force-encryption"></a>[強制的に暗号化]  
 クライアント アプリケーションとの通信時に暗号化を要求するように[!INCLUDE[ssDE](../../includes/ssde-md.md)]を構成できます。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
## <a name="extended-protection-for-authentication"></a>認証の拡張保護 (Extended Protection for Authentication)  
 チャネル バインドとサービス バインドを使用した認証の拡張保護のサポートは、拡張保護をサポートしているオペレーティング システムで使用できます。 詳細については、「 [拡張保護を使用したデータベース エンジンへの接続](connect-to-the-database-engine-using-extended-protection.md)」を参照してください。  
  
## <a name="authenticating-by-using-kerberos"></a>Kerberos を使用した認証  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は Kerberos 認証をサポートしています。 Kerberos 認証の詳細については、「 [Kerberos 接続用のサービス プリンシパル名の登録](register-a-service-principal-name-for-kerberos-connections.md) 」および「 [Microsoft® Kerberos Configuration Manager for SQL Server®](https://www.microsoft.com/download/details.aspx?id=39046)」を参照してください。  
  
### <a name="registering-a-server-principal-name-spn"></a>サービス プリンシパル名 (SPN) の登録  
 Kerberos 認証サービスでは、SPN を使用してサービスが認証されます。 詳細については、「 [Kerberos 接続用のサービス プリンシパル名の登録](register-a-service-principal-name-for-kerberos-connections.md)」を参照してください。  
  
 SPN を使用すると、NTLM で接続する場合のクライアント認証のセキュリティを強化することもできます。 詳細については、「 [拡張保護を使用したデータベース エンジンへの接続](connect-to-the-database-engine-using-extended-protection.md)」を参照してください。  
  
## <a name="sql-server-browser-service"></a>SQL Server Browser Service  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスはサーバーで実行され、クライアント コンピューターが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを見つけるのに役立ちます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスを構成する必要はありませんが、いくつかの接続シナリオで実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスの詳細については、「[SQL Server Browser サービス &#40;データベース エンジンと SSAS&#41;](sql-server-browser-service-database-engine-and-ssas.md)」を参照してください。  
  
## <a name="hiding-sql-server"></a>SQL Server の非表示  
 実行中、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser は、インストールされている各インスタンスの名前、バージョン、接続情報などに関するクエリに応答します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の **HideInstance** フラグは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser がこのサーバー インスタンスの情報に関するクエリに応答しないことを示します。 クライアント アプリケーションは接続できますが、接続情報が必要です。 詳細については、「 [SQL Server データベース エンジンのインスタンスの非表示](../sql-server-database-engine-overview.md)」を参照してください。  
  
## <a name="related-content"></a>関連コンテンツ  
 [クライアント ネットワーク構成](client-network-configuration.md)  
  
 [データベース エンジン サービスの管理](manage-the-database-engine-services.md)  
  
  
