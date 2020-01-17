---
title: 名前付きパイプを使用して有効な接続文字列を作成する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connection strings [Database Engine], named pipes
- pipes [SQL Server]
- pipes [SQL Server], connecting to
- aliases [SQL Server], named pipes
- Named Pipes [SQL Server], connection strings
ms.assetid: 90930ff2-143b-4651-8ae3-297103600e4f
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 12d5cb30217a0580d4da101d614b4930cfd8184b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63065550"
---
# <a name="creating-a-valid-connection-string-using-named-pipes"></a>名前付きパイプを使用した有効な接続文字列の作成
  ユーザーが変更しない限りときの既定のインスタンス[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は使用して、名前付きパイプ プロトコルでリッスン、`\\.\pipe\sql\query`パイプ名として。 ここで、ピリオドはコンピューターがローカル コンピューターであることを示し、`pipe` は接続が名前付きパイプであることを示します。`sql\query` はパイプの名前を示します。 既定のパイプに接続するには、別名でもパイプ名に `\\<computer_name>\pipe\sql\query` を指定する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が別のパイプで受信を待機する構成になっている場合は、パイプ名としてそのパイプを使用する必要があります。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がパイプとして `\\.\pipe\unit\app` を使用している場合、別名ではパイプ名として `\\<computer_name>\pipe\unit\app` を使用しなければなりません。  
  
 有効なパイプ名を作成するには、次の操作を行う必要があります。  
  
-   **[別名]** を指定します。  
  
-   選択**名前付きパイプ**として、**プロトコル**します。  
  
-   入力、**名前をパイプ**します。 または、かまいません**パイプ名**空白と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager は、指定した後、適切なパイプ名は完了、**プロトコル**と**サーバー**  
  
-   指定、 **Server**します。 名前付きのインスタンスの場合は、サーバー名とインスタンス名を指定できます。  
  
 接続の時点で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client コンポーネントと読み取り、サーバー、プロトコル、パイプ名値を指定された別名のレジストリから形式でパイプ名を作成します。`np:\\<computer_name>\pipe\<pipename>`または`np:\\<IPAddress>\pipe\<pipename>`します。名前付きインスタンスの場合は、既定のパイプ名は`\\<computer_name>\pipe\MSSQL$<instance_name>\sql\query`します。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ファイアウォールが既定ではポート 445 を閉じます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通信ポート 445、する必要がありますが再びオープン ポート場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]名前付きパイプを使用して、受信クライアント接続をリッスンするように構成します。 ファイアウォールの構成方法の詳細については、次を参照してください。"する方法。ファイアウォールを構成する SQL Server アクセス用"で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックまたはファイアウォールのマニュアルを確認します。  
  
## <a name="connecting-to-the-local-server"></a>ローカル サーバーへの接続  
 クライアントと同じコンピューター上で実行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続する場合は、サーバー名として `(local)` を使用することもできます。 `(local)` の使用はあいまいさを残すのでお勧めできませんが、対象のコンピューター上でクライアントを実行していることがわかっている場合には便利な機能です。 たとえば、営業スタッフは、ノート型コンピューター上で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行し、プロジェクト データもそのノート型コンピューターに保存しておきます。このように、ネットワークに接続しないモバイル ユーザー用のアプリケーションの場合、(local) に接続するクライアントは、常にそのノート型コンピューターで実行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続することになります。 `localhost` の代わりに、`(local)` またはピリオド (.) を使用することもできます。  
  
## <a name="verifying-your-connection-protocol"></a>接続プロトコルの確認  
 以下のクエリは、現在の接続に使用しているプロトコルを返します。  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>使用例  
 既定のパイプに対するサーバー名による接続:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <blank>  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 既定のパイプに対する IP アドレスによる接続:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <leave blank>  
Protocol           Named Pipes  
Server             <IPAddress>  
  
```  
  
 既定以外のパイプに対するサーバー名による接続:  
  
```  
Alias Name         <serveralias>  
Pipe Name          \\<servername>\pipe\unit\app  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 名前付きのインスタンスに対するサーバー名による接続:  
  
```  
Alias Name         <serveralias>  
Pipe Name          \\<servername>\pipe\MSSQL$<instancename>\SQL\query  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 ローカル コンピューターに対する `localhost`による接続:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <blank>  
Protocol           Named Pipes  
Server             localhost  
  
```  
  
 ローカル コンピューターに対するピリオドによる接続:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <left blank>  
Protocol           Named Pipes  
Server             .  
  
```  
  
> [!NOTE]  
>  としてネットワーク プロトコルを指定する、 **sqlcmd**パラメーターを参照してください"する方法。接続に sqlcmd.exe を使用して、データベース エンジン"で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
## <a name="see-also"></a>関連項目  
 [共有メモリ プロトコルを使用した有効な接続文字列の作成](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)   
 [TCP/IP を使用した有効な接続文字列の作成](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [ネットワーク プロトコルの選択](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
