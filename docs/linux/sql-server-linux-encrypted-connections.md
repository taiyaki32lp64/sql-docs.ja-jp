---
title: SQL Server on Linux への接続の暗号化
description: この記事では、SQL Server on Linux への接続の暗号化について説明します。
ms.date: 01/30/2018
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
helpviewer_keywords:
- Linux, encrypted connections
ms.openlocfilehash: 975a312988a7df4bdb4fb2858d7b0fcbe95cea33
ms.sourcegitcommit: 6413b7495313830ad1ae5aefe0c09e8e7a284b07
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016857"
---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>SQL Server on Linux への接続の暗号化

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux では、トランスポート層セキュリティ (TLS) を使用して、クライアント アプリケーションと [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンス間のネットワークで送信されるデータを暗号化できます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、Windows と Linux の両方で同じ TLS プロトコルがサポートされています。TLS 1.2、1.1、および 1.0。 ただし、TLS を構成する手順は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] が実行されているオペレーティング システムに固有です。  

## <a name="requirements-for-certificates"></a>証明書の要件 
作業を開始する前に、証明書が次の要件に従っていることを確認する必要があります。
- 現在のシステム時刻が証明書の [有効期間の開始] プロパティから証明書の [有効期間の終了] プロパティまでの範囲にあること。
- 証明書がサーバー認証に使用されていること。 つまり、証明書の [拡張キー使用法] プロパティで [ サーバー認証 ] (1.3.6.1.5.5.7.3.1) が指定されている必要があります。
- 証明書が AT_KEYEXCHANGE の KeySpec オプションを使用して作成されていること。 通常、証明書の [キー使用法] プロパティ (KEY_USAGE) には、キーの暗号化 (CERT_KEY_ENCIPHERMENT_KEY_USAGE) も含まれます。
- 証明書の [サブジェクト] プロパティで、共通名 (CN) がサーバー コンピューターのホスト名または完全修飾ドメイン名 (FQDN) と同一であると示されていること。 注:ワイルドカード証明書がサポートされています。

## <a name="configuring-the-openssl-libraries-for-use-optional"></a>使用する OpenSSL ライブラリの構成 (省略可能)
暗号化でどの `libcrypto.so` ライブラリと `libssl.so` ライブラリを使用するかを参照するシンボリック リンクを `/opt/mssql/lib/` ディレクトリに作成できます。 これは、システムで提供されている OpenSSL の既定以外の特定のバージョンを使用するように SQL Server に指示する場合に便利です。 これらのシンボリック リンクが存在しない場合、SQL Server では、システム上の既定の構成済みの OpenSSL ライブラリが読み込まれます。

これらのシンボリック リンクには `libcrypto.so` と `libssl.so` いう名前を付け、`/opt/mssql/lib/` ディレクトリに配置する必要があります。

## <a name="overview"></a>概要
クライアント アプリケーションから [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] への接続を暗号化するために TLS が使用されます。 正しく構成されると、TLS によって、クライアントとサーバー間の通信に対して、プライバシーとデータ整合性の両方が提供されます。  TLS 接続は、クライアント側で開始することもサーバー側で開始することもできます。 

## <a name="client-initiated-encryption"></a>クライアントによって開始される暗号化 
- **証明書を生成する** (/CN とお使いの SQL Server ホストの完全修飾ドメイン名が一致する必要があります)

> [!NOTE]
> この例では、自己署名証明書を使用しますが、運用環境のシナリオでは使用すべきではありません。 CA 証明書を使用する必要があります。 

        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **SQL Server を構成する**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0 

- **クライアント コンピューター (Windows、Linux、または macOS) に証明書を登録する**

    -   CA の署名入り証明書を使用する場合は、ユーザー証明書ではなく、証明機関 (CA) 証明書をクライアント コンピューターにコピーする必要があります。 
    -   自己署名証明書を使用している場合は、各ディストリビューションの次のフォルダーに .pem ファイルをコピーし、それらを有効にするコマンドを実行します。 
        - **Ubuntu**:証明書を ```/usr/share/ca-certificates/``` にコピーします。拡張子を .crt に変更します。dpkg-reconfigure ca-certificates を使用して、CA 証明書として有効にします。 
        - **RHEL**:証明書を ```/etc/pki/ca-trust/source/anchors/``` にコピーします。```update-ca-trust``` を使用して、システム CA 証明書として有効にします。
        - **SUSE**:証明書を ```/usr/share/pki/trust/anchors/``` にコピーします。```update-ca-certificates``` を使用して、システム CA 証明書として有効にします。
        - **Windows**:[現在のユーザー] -> [信頼されたルート証明機関] -> [証明書] で、.pem ファイルを証明書としてインポートします。
        - **macOS**: 
           - 証明書を ```/usr/local/etc/openssl/certs``` にコピーします。
           - 次のコマンドを実行して、ハッシュ値を取得します。```/usr/local/Cellar/openssl/1.0.2l/openssl x509 -hash -in mssql.pem -noout```
           - 証明書の名前を値に変更します。 例: ```mv mssql.pem dc2dd900.0```」を参照してください。 ```/usr/local/etc/openssl/certs``` に dc2dd900.0 が含まれていることを確認します。
    
-   **接続文字列の例** 

    - **[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]**   
  ![SSMS 接続ダイアログ](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "SSMS 接続ダイアログ")  
  
    - **SQLCMD** 

            sqlcmd  -S <sqlhostname> -N -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=True; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=Yes; TrustServerCertificate=no;" 
    - **JDBC** 
    
            "encrypt=true; trustServerCertificate=false;" 

## <a name="server-initiated-encryption"></a>サーバーによって開始される暗号化 

- **証明書を生成する** (/CN とお使いの SQL Server ホストの完全修飾ドメイン名が一致する必要があります)
        
        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **SQL Server を構成する**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 1 
        
-   **接続文字列の例** 

    - **SQLCMD**

            sqlcmd  -S <sqlhostname> -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=False; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=no; TrustServerCertificate=no;"  
    - **JDBC** 
    
            "encrypt=false; trustServerCertificate=false;" 
            
> [!NOTE]
> クライアントで CA に接続して証明書の信頼性を検証できない場合は、**TrustServerCertificate** を True に設定します。

## <a name="common-connection-errors"></a>一般的な接続エラー  

|エラー メッセージ |Fix |
|--- |--- |
|この証明書チェーンは、信頼されていない機関によって発行されました。  |このエラーは、TLS ハンドシェイク中に SQL Server によって提示された証明書の署名をクライアントで検証できない場合に発生します。 クライアントで [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 証明書が直接信頼されているか、SQL Server 証明書に署名した CA が信頼されていることを確認します。 |
|対象のプリンシパル名が間違っています。  |SQL Server の証明書の [共通名] フィールドと、クライアントの接続文字列に指定されているサーバー名が一致していることを確認します。 |  
|既存の接続はリモート ホストに強制的に切断されました。 |このエラーは、SQL Server によって要求されている TLS プロトコルのバージョンがクライアントでサポートされていない場合に発生する可能性があります。 たとえば、TLS 1.2 を要求するように [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] が構成されている場合は、クライアントでも TLS 1.2 プロトコルがサポートされていることを確認します。 |
| | |   
