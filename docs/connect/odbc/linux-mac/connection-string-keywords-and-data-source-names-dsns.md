---
title: SQL Server への接続 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source names
- connection string keywords
- DSNs
ms.assetid: f95cdbce-e7c2-4e56-a9f7-8fa3a920a125
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 486d26dd3afeb91cb43181875e22592fb482af5f
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702805"
---
# <a name="connecting-to-sql-server"></a>SQL Server への接続
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

このトピックでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースへの接続を作成する方法について説明します。  
  
## <a name="connection-properties"></a>接続プロパティ  

Linux および Mac でサポートされているすべての接続文字列キーワードと属性については、「 [DSN と接続文字列のキーワードと属性](../../../connect/odbc/dsn-connection-string-attribute.md)」を参照してください。

> [!IMPORTANT]  
> データベース ミラーリングを使用する (フェールオーバー パートナーがある) データベースに接続する場合は、接続文字列にデータベース名を指定しないでください。 代わりに、**use** <_データベース名_> コマンドを送信してデータベースに接続してから、クエリを実行します。  
  
**Driver**キーワードに渡される値には、次のいずれかを指定できます。  
  
-   ドライバーをインストールしたときに使用した名前。

-   ドライバー ライブラリへのパス。ドライバーのインストールに使用されたテンプレート .ini ファイルで指定されています。  

Dsn を作成するには、必要に応じて、現在の**ユーザーだけが`.odbc.ini`アクセスできるユーザー dsn のファイル** (ホームディレクトリの場合は`/etc/odbc.ini` ) を作成し、システム dsn (管理者特権が必要です) を編集します。次のサンプルファイルは、DSN に最低限必要なエントリを示しています。  

```  
[MSSQLTest]  
Driver = ODBC Driver 13 for SQL Server  
Server = [protocol:]server[,port]  
#   
# Note:  
# Port is not a valid keyword in the odbc.ini file  
# for the Microsoft ODBC driver on Linux or macOS
#  
```  

サーバーに接続するために、必要に応じてプロトコルとポートを指定することができます。 たとえば、 **Server = tcp:** _servername_ **, 12345**のようになります。 Linux および macOS ドライバーでサポートされているプロトコルは`tcp`のみであることに注意してください。

静的ポートの名前付きインスタンスに接続するには、<b>Server=</b>*servername*,**port_number** を使用します。 バージョン 17.4 より前では、動的ポートへの接続はサポートされていません。

または、DSN 情報をテンプレート ファイルに追加し、次のコマンドを実行して `~/.odbc.ini` に追加することもできます。
 - **odbcinst -i -s -f** _template_file_  
 
を使用`isql`して接続をテストすることで、ドライバーが動作していることを確認できます。または、次のコマンドを使用することもできます。
 - **bcp master.INFORMATION_SCHEMA.TABLES out OutFile.dat -S <server> -U <name> -P <password>**  

## <a name="using-secure-sockets-layer-ssl"></a>Secure Sockets Layer (SSL) を使用する  
Secure Sockets Layer (SSL) を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]への接続を暗号化できます。 SSL は、ネットワーク上の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のユーザー名とパスワードを保護します。 また、サーバーの ID を検証して、man-in-the-middle (MITM) 攻撃に対して保護することもできます。  

暗号化を有効にすると、セキュリティは向上しますが、パフォーマンスは低下します。

詳細については、「 [SQL Server への接続の暗号化](https://go.microsoft.com/fwlink/?LinkId=220900)」と「[検証を伴わない暗号化の使用](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)」を参照してください。

**Encrypt** と **TrustServerCertificate**の設定に関係なく、サーバー ログインの資格情報 (ユーザー名とパスワード) は常に暗号化されます。 次の表は、 **Encrypt** 設定と **TrustServerCertificate** 設定の効果の一覧です。  

||**TrustServerCertificate = いいえ**|**TrustServerCertificate = はい**|  
|-|-------------------------------------|------------------------------------|  
|**Encrypt=no**|サーバー証明書は確認されません。<br /><br />クライアントとサーバー間で送信されるデータは暗号化されません。|サーバー証明書は確認されません。<br /><br />クライアントとサーバー間で送信されるデータは暗号化されません。|  
|**Encrypt=yes**|サーバー証明書は確認されます。<br /><br />クライアントとサーバー間で送信されるデータは暗号化されます。<br /><br />[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SSL 証明書のサブジェクトの共通名 (CN) またはサブジェクトの別名 (SAN) の名前 (または IP アドレス) は、接続文字列に指定されているサーバー名 (または IP アドレス) と一致する必要があります。|サーバー証明書は確認されません。<br /><br />クライアントとサーバー間で送信されるデータは暗号化されます。|  

既定では、暗号化された接続はサーバーの証明書を必ず検証します。 ただし、自己署名証明書があるサーバーに接続する場合は、信頼された`TrustServerCertificate`証明機関の一覧に対して証明書の確認をバイパスするオプションも追加します。  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
SSL は、OpenSSL ライブラリを使用します。 次の表は、OpenSSL の最低限のサポートされるバージョンと、各プラットフォームの既定の証明書信頼ストアを示します。

|プラットフォーム|最低限の OpenSSL のバージョン|既定の証明書信頼ストアの場所|  
|------------|---------------------------|--------------------------------------------|
|Debian 10|1.1.1|/etc/ssl/certs|
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71|1.0.1|/etc/ssl/certs|
|OS X 10.11、macOS 10.12、10.13、10.14|1.0.2|/usr/local/etc/openssl/certs|
|Red Hat Enterprise Linux 8|1.1.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 15|1.1.0|/etc/ssl/certs|
|SuSE Linux Enterprise 11, 12|1.0.1|/etc/ssl/certs|
|Ubuntu 18.10、19.04|1.1.1|/etc/ssl/certs|
|Ubuntu 18.04|1.1.0|/etc/ssl/certs|
|Ubuntu 16.04、16.10、17.10|1.0.2|/etc/ssl/certs|
|Ubuntu 14.04|1.0.1|/etc/ssl/certs|

`Encrypt` **SQLDriverConnect**を使用して接続する場合は、オプションを使用して接続文字列で暗号化を指定することもできます。

## <a name="adjusting-the-tcp-keep-alive-settings"></a>TCP キープアライブ設定の調整

ODBC ドライバー17.4 以降では、ドライバーがキープアライブパケットを送信し、応答が受信されないときにそのドライバーを転送する頻度を構成できます。
を構成するには、のドライバーのセクション`odbcinst.ini`またはの DSN の`odbc.ini`セクションに、次の設定を追加します。 DSN を使用して接続する場合、ドライバーは DSN のセクションの設定を使用します (存在する場合)。それ以外の場合、または接続文字列のみを使用して接続する場合は、の`odbcinst.ini`ドライバーのセクションの設定が使用されます。 どちらの場所にも設定が存在しない場合、ドライバーは既定値を使用します。

- `KeepAlive=<integer>`キープアライブパケットを送信して、アイドル状態の接続がまだ破損していないことを TCP が確認する頻度を制御します。 既定値は **30** 秒です。

- `KeepAliveInterval=<integer>`応答が受信されるまで、キープアライブの再送信を分離する間隔を決定します。  既定値は **1** 秒です。


## <a name="see-also"></a>参照  
[Linux および macOS に Microsoft ODBC Driver for SQL Server をインストールする](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[プログラミング ガイドライン](../../../connect/odbc/linux-mac/programming-guidelines.md)
