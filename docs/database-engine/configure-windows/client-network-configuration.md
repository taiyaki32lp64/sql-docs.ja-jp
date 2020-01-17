---
title: クライアント ネットワーク構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- client configuration [SQL Server], connections
- Database Engine [SQL Server], network configurations
- connections [SQL Server], client configuration
- client connections [SQL Server], about client network connections
- client computers [SQL Server]
- client connections [SQL Server]
- network connections [SQL Server], client configuration
ms.assetid: c382eacd-0a0c-40a4-958f-9b774eb2d734
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4fcbb9e6ee0f68433034cd2c3a29f565e05359e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012964"
---
# <a name="client-network-configuration"></a>クライアント ネットワーク構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  クライアント ソフトウェアを使用すると、クライアント コンピューターからネットワーク上の [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続できます。 "クライアント" は、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]など、サーバーが提供するサービスを使用するフロント エンドのアプリケーションです。 こうしたアプリケーションを実行するコンピューターは、 *クライアント コンピューター*と呼ばれます。  
  
 最も単純な構成では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスと同じコンピューター上に常駐できます。 ただし、通常は、クライアントはネットワーク経由で 1 つ以上のリモート サーバーに接続します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のクライアント/サーバー アーキテクチャにより、同じネットワーク上の複数のクライアントとサーバーのシームレスな管理が実現されます。 既定のクライアント構成は、ほとんどの状況に使用できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントには、以下のようなさまざまな種類のアプリケーションがあります。  
  
-   OLE DB コンシューマー  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続するアプリケーションです。 OLE DB プロバイダーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータを OLE DB 行セットとして使用するクライアント アプリケーションと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とを仲介します。 たとえば、 **sqlcmd** コマンド プロンプト ユーティリティや [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]は、OLE DB アプリケーションです。  
  
-   ODBC アプリケーション  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の以前のバージョンと共にインストールされるクライアント ユーティリティも、この種類のアプリケーションに該当します。たとえば、 **osql** コマンド プロンプト ユーティリティや、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへの接続に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC ドライバーを使用するその他のアプリケーションなどです。  
  
-   DB-Library クライアント  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **isql** コマンド プロンプト ユーティリティや DB-Library に書き込まれるクライアントなどです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の DB-Library を使用したクライアント アプリケーションに対するサポートは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 限定の機能です。  
  
> [!NOTE]  
>  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] では、DB-Library および Embedded SQL API を使用した既存アプリケーションからの接続が引き続きサポートされますが、これらの API を使用するアプリケーションでのプログラミング作業に必要なファイルやドキュメントは含まれません。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] の今後のバージョンでは、DB-Library アプリケーションや Embedded SQL アプリケーションからの接続はサポートされなくなります。 新しいアプリケーションの開発には DB-Library や Embedded SQL を使用しないでください。 DB-Library や Embedded SQL への依存関係は、既存アプリケーションを変更するときに削除してください。 これらの API の代わりに、SQLClient 名前空間または OLE DB や ODBC などの API を使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、これらのアプリケーションの実行に必要な DB-Library DLL は含まれていません。 DB-Library アプリケーションまたは Embedded SQL アプリケーションを実行するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version 6.5、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0、または [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]から DB-Library DLL を入手する必要があります。  
  
 どの種類のアプリケーションを使用する場合も、クライアントの主な管理作業として、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のサーバー コンポーネントへの接続を構成する必要があります。 クライアントの管理は、ユーザー サイトの要件に応じて、簡単な作業から複雑な作業までさまざまです。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client の DLL には、ネットワーク ライブラリが含まれており、セットアップ プログラムによってインストールされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を新規インストールする場合は、セットアップ中にネットワーク プロトコルは有効になりません。 アップグレード インストールの場合は、以前有効になっていたプロトコルが有効になります。 基になるネットワーク プロトコルは、Windows セットアップの一環としてインストールするか、コントロール パネルの [ネットワーク] を使用してインストールします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントの管理には、以下のツールを使用します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャー  
  
     クライアント ネットワーク コンポーネント、サーバー ネットワーク コンポーネントのいずれの管理にも、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用します。これは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ネットワーク ユーティリティ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアント ネットワーク ユーティリティ、および以前のバージョンで提供されていたサービス マネージャーで構成されています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーは、MMC ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソール) スナップインです。 また、Windows のコンピューターの管理スナップインにも、ノードの 1 つとして表示されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用すると、各ネットワーク ライブラリの有効と無効の切り替えや、構成、優先順位の設定を行うことができます。  
  
-   セットアップ  
  
     クライアント コンピューターにネットワーク コンポーネントをインストールするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを実行します。 セットアップをコマンド プロンプトから実行している場合は、セットアップ中に各ネットワーク ライブラリの有効と無効を個別に設定できます。  
  
-   ODBC データ ソース アドミニストレーター  
  
     ODBC データ ソース アドミニストレーターでは、Microsoft Windows オペレーティング システムを実行するコンピューター上で、ODBC データ ソースを作成および変更できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [クライアント プロトコルの構成](../../database-engine/configure-windows/configure-client-protocols.md)  
  
 [クライアントが使用するサーバーの別名の作成または削除 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)  
  
 [SQL Server へのログイン](../../database-engine/configure-windows/logging-in-to-sql-server.md)  
  
 [ODBC データ ソース アドミニストレーターの起動](../../database-engine/configure-windows/open-the-odbc-data-source-administrator.md)  
  
 [ODBC SQL Server のドライバーのバージョンを確認する方法 &#40;Windows&#41;](../../database-engine/configure-windows/check-the-odbc-sql-server-driver-version-windows.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 [サーバー ネットワークの構成](../../database-engine/configure-windows/server-network-configuration.md)  
  
 [データベース エンジン サービスの管理](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  
