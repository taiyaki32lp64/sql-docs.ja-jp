---
title: 接続のトラブルシューティング |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bfba0b49-2e1f-411d-a625-d25fad9ea12d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d6a64589b44de50328aa3384a51e29e0c2cc9a6e
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027619"
---
# <a name="troubleshooting-connectivity"></a>接続のトラブルシューティング
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースと通信を行うため、TCP/IP がインストールされて動作している必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用すると、インストールされているネットワーク ライブラリのプロトコルを確認できます。  
  
 データベース接続は、さまざまな原因により失敗する場合があります。 次のようなものがあります。  
  
-   TCP/IP が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で有効になっていません、または指定されたサーバーやポート番号が間違っています。 指定されたサーバーとポート上の TCP/IP で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が待機していることを確認します。 このようなエラーは、次のような例外で報告されることがあります。"ログインに失敗しました。 ホストに TCP/IP 接続できませんでした。" これは、次のいずれかの原因を示します。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はインストールされていますが、TCP/IP が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用のネットワーク プロトコルとして、[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ネットワーク ユーティリティ、または [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、インストールされていません。  
  
    -   TCP/IP は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロトコルとしてインストールされていますが、JDBC 接続 URL で指定されたポートでリッスンしていません。 既定のポートは 1433 ですが、製品のインストール時に任意のポートで待機するように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を構成することができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がポート 1433 でリッスンしていることを確認します。 または、ポートが変更されている場合は、JDBC 接続 URL で指定するポートを、変更されたポートと一致させます。 JDBC 接続 Url の詳細については、「[接続 url の構築](../../connect/jdbc/building-the-connection-url.md)」を参照してください。  
  
    -   JDBC 接続 URL で指定されたコンピューターのアドレスが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールおよび起動されたサーバーを参照していません。  
  
    -   クライアントと、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているサーバーとの間で、TCP/IP のネットワークが動作していません。 telnet を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への TCP/IP 接続を確認できます。 たとえば、コマンド プロンプトに「`telnet 192.168.0.0 1433`」と入力します。192.168.0.0 は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているコンピューターのアドレス、1433 はリッスンしているポートを示します。 "Telnet が接続できません" というメッセージを受け取る場合、TCP/IP はそのポートで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続をリッスンしていません。 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ネットワーク ユーティリティ、または [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がポート 1433 で TCP/IP を使用するように構成されていることを確認します。  
  
    -   サーバーで使用されるポートがファイアウォールで開かれていない。 これには、サーバーが使用するポート、またはオプションで、サーバーの名前付きインスタンスに関連付けられたポートが含まれます。  
  
-   指定されたデータベース名が間違っている。 実際に存在する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースにログオンしていることを確認します。  
  
-   ユーザー名またはパスワードが間違っている。 値が正しいことを確認します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合、JDBC ドライバーでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が既定ではない [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証でインストールされている必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスをインストールまたは構成するときに、このオプションが選択されていることを確認します。  
  
## <a name="see-also"></a>参照  
 [JDBC ドライバーに関する問題の診断](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)   
 [JDBC ドライバーによる SQL Server への接続](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
