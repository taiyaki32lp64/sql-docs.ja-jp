---
title: ネットワークを使用する場合とネットワークを使用しない場合の SQL Server の実行 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- verifying Server service has been started
- net start [SQL Server]
- command prompt [SQL Server], connections
- SQL Server services, networks
- status information [SQL Server], Server service
- running SQL Server
- networking [SQL Server], SQL Server with or without
- services [SQL Server], networks
- starting Server service
- SQL Server, running
ms.assetid: 54eac961-5c7a-4481-982d-f93a64b5c2f4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: db02b300e0f327a9186fb9b9af612d8f3f1ec452
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915985"
---
# <a name="run-sql-server-with-or-without-a-network"></a>ネットワークを使用する場合とネットワークを使用しない場合の SQL Server の実行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はネットワーク上で実行できます。また、ネットワークを使用せずに機能させることもできます。  
  
## <a name="running-sql-server-on-a-network"></a>ネットワーク上での SQL Server の実行  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がネットワーク経由で通信するようにするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを実行する必要があります。 既定では、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows により、組み込みの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが自動的に開始されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが開始されているかどうかを調べるには、コマンド プロンプトで次のように入力します。  
  
 **net start**  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に関連付けれらたサービスが開始されている場合は、以下のサービスが **net start** の出力に表示されます。  
  
-   Analysis Services (MSSQLSERVER)  
  
-   SQL Server (MSSQLSERVER)  
  
-   SQL Server Agent (MSSQLSERVER)  
  
## <a name="running-sql-server-without-a-network"></a>ネットワークを使用しない SQL Server の実行  
 ネットワークを使用せずに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行する場合は、組み込みの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを開始する必要はありません。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、SQL Server 構成マネージャー、および **net start** コマンドと **net stop** コマンドは、ネットワークを使用していなくても機能するので、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを起動および停止する手順は、ネットワークを使用している場合もスタンドアロン運用の場合も同じです。  
  
 **sqlcmd** などのローカル クライアントからスタンドアロンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続するときは、ネットワークを使用せずに、ローカル パイプを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに直接接続します。 ローカル パイプとネットワーク パイプの相違は、ネットワークを使用するかしないかです。 他に指定がない限り、ローカル パイプでもネットワーク パイプでも、標準パイプ (\\\\.\pipe\sql\query) を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスとの接続が確立されます。  
  
 サーバー名を指定せずにローカル [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続しているときは、ローカル パイプを使用していることになります。 ローカルの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続し、明示的にサーバー名を指定しているときは、ネットワーク パイプまたは IPX/SPX (Internetwork Packet Exchange/Sequenced Packet Exchange) などの別のネットワーク プロセス間通信 (IPC) メカニズムを使用していることになります (複数のネットワークを使用するように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を構成している場合)。 スタンドアロンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではネットワーク パイプがサポートされないので、クライアントから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続するときに、不要な **/** _Server_name>_ 引数を省略する必要があります。 たとえば、 **osql** から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスタンドアロンのインスタンスに接続するには、次のように入力します。  
  
 **osql /Usa /P** _\<saPassword>_  
  
  
