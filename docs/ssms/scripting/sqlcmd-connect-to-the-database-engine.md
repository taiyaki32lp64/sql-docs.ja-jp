---
title: sqlcmd によるデータベース エンジンへの接続 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd utility, Database Engine connections
- Named Pipes [SQL Server], sqlcmd utility
- TCP/IP [SQL Server], client protocols
- network protocols [SQL Server], sqlcmd utility
- protocols [SQL Server], sqlcmd utility
- VIA
- client protocols [SQL Server]
ms.assetid: 74b0fb71-7f8e-4171-9431-d07528532524
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 21e218bab023ef59f3f9785f85f982546f626006
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267682"
---
# <a name="sqlcmd---connect-to-the-database-engine"></a>sqlcmd - データベース エンジンへの接続
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] TCP/IP ネットワーク プロトコル (既定) および名前付きパイプ プロトコルを使用したクライアント通信をサポートしています。 クライアントが、同じコンピューター上で [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続している場合は、共有メモリ プロトコルも使用できます。 プロトコルの選択には、3 つの一般的な方法があります。 **sqlcmd** ユーティリティで使用されるプロトコルは、次の順序で決定されます。  
  
-   **sqlcmd** では、下に示す接続文字列の一部として指定されているプロトコルが使用されます。  
  
-   接続文字列でプロトコルが指定されていない場合、 **sqlcmd** では、接続先の別名の一部として定義されているプロトコルが使用されます。 別名を作成して特定のネットワーク プロトコルを使用するように **sqlcmd** を構成するには、「[クライアントが使用するサーバーの別名の作成または削除 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)」を参照してください。  
  
-   他の方法でプロトコルが指定されていない場合、 **sqlcmd** では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーで指定されているプロトコル順序によって使用するネットワーク プロトコルが決定されます。  
  
 次の例では、ポート 1433 の [!INCLUDE[ssDE](../../includes/ssde-md.md)] の既定のインスタンスと、ポート 1691 でリッスンしていると想定される [!INCLUDE[ssDE](../../includes/ssde-md.md)] の名前付きインスタンスに接続するさまざまな方法を示しています。 一部の例では、ループバック アダプターの IP アドレス (127.0.0.1) を使用しています。 使用しているコンピューターのネットワーク インターフェイス カードの IP アドレスを使用してテストしてください。  
  
 インスタンス名を指定して、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] に接続します。  
  
```  
sqlcmd -S ComputerA  
sqlcmd -S ComputerA\instanceB  
```  
  
 IP アドレスを指定して、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] に接続します。  
  
```  
sqlcmd -S 127.0.0.1  
sqlcmd -S 127.0.0.1\instanceB  
```  
  
 TCP/IP ポート番号を指定して、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] に接続します。  
  
```  
sqlcmd -S ComputerA,1433  
sqlcmd -S ComputerA,1691  
sqlcmd -S 127.0.0.1,1433  
sqlcmd -S 127.0.0.1,1691  
```  
  
### <a name="to-connect-using-tcpip"></a>TCP/IP を使用して接続するには  
  
-   次に示す一般構文を使用して接続します。  
  
    ```  
    sqlcmd -S tcp:<computer name>,<port number>  
    ```  
  
-   既定のインスタンスに接続します。  
  
    ```  
    sqlcmd -S tcp:ComputerA,1433  
    sqlcmd -S tcp:127.0.0.1,1433  
    ```  
  
-   名前付きインスタンスに接続します。  
  
    ```  
    sqlcmd -S tcp:ComputerA,1691  
    sqlcmd -S tcp:127.0.0.1,1691  
    ```  
  
### <a name="to-connect-using-named-pipes"></a>名前付きパイプを使用して接続するには  
  
-   次に示す一般構文のいずれかを使用して接続します。  
  
    ```  
    sqlcmd -S np:\\<computer name>\<pipe name>  
    ```  
  
-   既定のインスタンスに接続します。  
  
    ```  
    sqlcmd -S np:\\ComputerA\pipe\sql\query  
    sqlcmd -S np:\\127.0.0.1\pipe\sql\query  
    ```  
  
-   名前付きインスタンスに接続します。  
  
    ```  
    sqlcmd -S np:\\ComputerA\pipe\MSSQL$<instancename>\sql\query  
    sqlcmd -S np:\\127.0.0.1\pipe\MSSQL$<instancename>\sql\query  
    ```  
  
### <a name="to-connect-using-shared-memory-a-local-procedure-call-from-a-client-on-the-server"></a>サーバー上のクライアントから共有メモリ (ローカル プロシージャ コール) を使用して接続するには  
  
-   次に示す一般構文のいずれかを使用して接続します。  
  
    ```  
    sqlcmd -S lpc:<computer name>  
    ```  
  
-   既定のインスタンスに接続します。  
  
    ```  
    sqlcmd -S lpc:ComputerA  
    ```  
  
-   名前付きインスタンスに接続します。  
  
    ```  
    sqlcmd -S lpc:ComputerA\<instancename>  
    ```  
  
  
