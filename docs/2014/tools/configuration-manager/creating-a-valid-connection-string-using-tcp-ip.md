---
title: TCP/IP を使用した有効な接続文字列の作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connection strings [Database Engine]
- ports [SQL Server], connecting to
- TCP/IP [SQL Server], connection strings
- connection strings [Database Engine], TCP/IP
- aliases [SQL Server], TCP/IP
ms.assetid: ee5dbc2c-1fc6-42bd-bdf5-efa792557934
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6449b073adb406d15f41cfe02d477a05ad8b0b31
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63065510"
---
# <a name="creating-a-valid-connection-string-using-tcp-ip"></a>TCP/IP を使用した有効な接続文字列の作成
  TCP/IP を使用した有効な接続文字列を作成するには、次の操作を行ってください。  
  
-   **[別名]** を指定します。  
  
-   **[サーバー]** ボックスに、 **PING** ユーティリティを使用して接続できるサーバー名か、 **PING** ユーティリティを使用して接続できる IP アドレスを入力します。 名前付きインスタンスの場合は、インスタンス名を追加します。  
  
-   **[プロトコル]** に **[TCP/IP]** を指定します。  
  
-   **[ポート番号]** にポート番号を入力します。ポート番号は省略できます。 省略した場合の既定値は 1433 です。この既定値は、サーバー上にある [!INCLUDE[ssDE](../../includes/ssde-md.md)] の既定インスタンスのポート番号です。 ポート 1433 でリッスンしていない名前付きインスタンスまたは既定のインスタンスに接続する場合は、ポート番号を指定するか、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスを開始する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスの構成の詳細については、「 [SQL Server Browser サービス](../../../2014/tools/configuration-manager/sql-server-browser-service.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client コンポーネントは接続の時点で、指定された別名のサーバー、プロトコル、ポート番号の値をレジストリから読み取り、 `tcp:<servername>[\<instancename>],<port>` または `tcp:<IPAddress>[\<instancename>],<port>`の形式で接続文字列を作成します。  
  
> [!NOTE]  
>  既定では、ポート 1433 が [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ファイアウォールによって閉じられます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はポート 1433 経由で通信するため、TCP/IP を使用する着信クライアントをリッスンするように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を構成している場合は、このポートを再度開く必要があります。 ファイアウォールの構成方法の詳細については、次を参照してください。"する方法。ファイアウォールを構成する SQL Server アクセス用"で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックまたはファイアウォールのマニュアルを確認します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client では、インターネット プロトコル バージョン 4 (IPv4) とインターネット プロトコル バージョン 6 (IPv6) の両方が完全にサポートされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーは、IPv4 と IPv6 のどちらの形式の IP アドレスも受け入れます。 IPv6 の詳細については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「IPv6 を使用した接続」を参照してください。  
  
## <a name="connecting-to-the-local-server"></a>ローカル サーバーへの接続  
 クライアントと同じコンピューター上で実行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続する場合は、サーバー名として `(local)` を使用することもできます。 このような指定はあいまいさを残すのでお勧めできませんが、対象のコンピューター上でクライアントを実行していることがわかっている場合には便利な機能です。 たとえば、営業スタッフは、ノート型コンピューター上で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行し、プロジェクト データもそのノート型コンピューターに保存しておきます。このように、ネットワークに接続しないモバイル ユーザー用のアプリケーションの場合、 `(local)` に接続するクライアントは、常にそのノート型コンピューターで実行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続することになります。 `localhost` の代わりに**またはピリオド (** . `(local)`) を使用することもできます。  
  
## <a name="verifying-your-connection-protocol"></a>接続プロトコルの確認  
 次のクエリからは、現在の接続で使用しているプロトコルが返されます。  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>使用例  
 サーバー名による接続:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <servername>  
  
```  
  
 名前付きのインスタンスに対するサーバー名による接続:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <servername>\<instancename>  
  
```  
  
 指定したポートに対するサーバー名による接続:  
  
```  
Alias Name         <serveralias>  
Port No            <port>  
Protocol           TCP/IP  
Server             <servername>  
  
```  
  
 IP アドレスによる接続:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <IPAddress>  
  
```  
  
 名前付きのインスタンスに対する IP アドレスによる接続:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <IPAddress>\<instancename>  
  
```  
  
 指定したポートに対する IP アドレスによる接続:  
  
```  
Alias Name         <serveralias>  
Port No            <port number>  
Protocol           TCP/IP  
Server             <IPAddress>  
  
```  
  
 ローカル コンピューターに対する `(local)`による接続:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             (local)  
  
```  
  
 ローカル コンピューターに対する `localhost`による接続:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             localhost  
  
```  
  
 ローカル コンピューター上の名前付きのインスタンスに対する `localhost`による接続:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             localhost\<instancename>  
  
```  
  
 ローカル コンピューターに対するピリオドによる接続:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             .  
  
```  
  
 ローカル コンピューター上の名前付きのインスタンスに対するピリオドによる接続:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             .\<instancename>  
  
```  
  
> [!NOTE]  
>  としてネットワーク プロトコルを指定することについて、 **sqlcmd**パラメーターを参照してください"する方法。接続に sqlcmd.exe を使用して、データベース エンジン"で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
## <a name="see-also"></a>参照  
 [共有メモリ プロトコルを使用した有効な接続文字列の作成](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)   
 [名前付きパイプを使用した有効な接続文字列の作成](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md)   
 [ネットワーク プロトコルの選択](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
