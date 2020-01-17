---
title: アプリケーションのセキュリティ |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 940879b4-aa0f-41ce-a369-6cfc0e78e01d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 81c57e5ab7ca88267693690992106b5f39e2af82
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028511"
---
# <a name="application-security"></a>アプリケーションのセキュリティ
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] を使用するときは、アプリケーションのセキュリティを確保するための対策を講じることが重要です。 以下のセクションでは、アプリケーションをセキュリティ保護するために実行できる手順に関する情報を提供します。  
  
## <a name="using-java-policy-permissions"></a>Java のポリシー アクセス許可の使用  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] を使用するときは、JDBC ドライバーに必要な Java のポリシー アクセス許可を指定することが重要です。 Java ランタイム環境 (JRE) には、スレッドがリソースにアクセスできるかどうかを判断するために実行時に使用できる拡張セキュリティ モデルがあります。 セキュリティ ポリシー ファイルでこのアクセスを制御することができます。 ポリシー ファイル自体は開発者およびコンテナーのシステム管理者が管理しますが、このトピックで挙げるアクセス許可は JDBC ドライバーの機能に影響します。  
  
 ポリシー ファイルの一般的なアクセス許可は、次のようになっています。  
  
```  
// Example policy file entry.  
grant [signedBy <signer>,] [codeBase <code source>] {  
   permission  <class>  [<name> [, <action list>]];  
};  
```  
  
 特権の付与を最小限に留めるために、次のコードベースは JDBC ドライバーのコードベースに限定してください。  
  
```  
grant codeBase "file:/install_dir/lib/-" {  
  
// Grant access to data source.  
permission java.util.PropertyPermission "java.naming.*", "read,write";  
  
// Specify which hosts can be connected to.  
permission java.net.socketPermission "host:port", "connect";  
  
// Logger permission to take advantage of logging.  
permission java.util.logging.LoggingPermission;  
  
// Grant listen/connect/accept permissions to the driver if   
// connecting to a named instance as the client driver.   
// This connects to a udp service and listens for a response.  
permission java.net.SocketPermission "*", "listen, connect, accept";   
};   
```  
  
> [!NOTE]  
>  コード "file:/install_dir/lib/-" は、JDBC ドライバーのインストール ディレクトリを指します。  
  
## <a name="protecting-server-communication"></a>サーバーとの通信の保護  
 JDBC ドライバーを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースと通信する場合、インターネット プロトコル セキュリティ (IPSec) または SSL (Secure Sockets Layer) を使用して、通信チャネルをセキュリティで保護できます。また、IPSec と SSL の両方を使用することも可能です。  
  
 SSL のサポートは、IPSec 以外の追加の保護レベルを提供するために使用できます。 SSL の使用方法の詳細については、「 [ssl 暗号化の使用](../../connect/jdbc/using-ssl-encryption.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [JDBC ドライバー アプリケーションのセキュリティ保護](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
