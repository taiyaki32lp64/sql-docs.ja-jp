---
title: Hadoop 接続マネージャー - SQL Server Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoopconn.f1
ms.assetid: 8bb15b97-9827-46bc-aca6-068534ab18c4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4b07af028cd0f2385c447c99192ccc50b65c4925
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096130"
---
# <a name="hadoop-connection-manager"></a>Hadoop 接続マネージャー

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Hadoop 接続マネージャーでは、プロパティに指定された値を使用して SQL Server Integration Services (SSIS) パッケージを Hadoop クラスターに接続できます。  
  
## <a name="configure-the-hadoop-connection-manager"></a>Hadoop 接続マネージャーの構成  
  
1.  **[SSIS 接続マネージャーの追加]** ダイアログ ボックスで **[Hadoop]**  >  **[追加]** の順に選択します。 **[Hadoop Connection Manager Editor]** (Hadoop Connection 接続マネージャー エディター) ダイアログ ボックスが表示されます。  
  
2.  関連する Hadoop クラスター情報を構成するには、左側のウィンドウで **[WebHCat]** または **[WebHDFS]** タブを選択します。
  
3.  Hive または Pig ジョブを Hadoop で起動するために **WebHCat** オプションを有効にする場合は、次の操作を行います。 
  
    1.  **[WebHCat ホスト]** に、WebHCat サービスをホストするサーバーを入力します。  
  
    2.  **[WebHCat Port]** (WebHCat ポート) に、WebHCat サービスのポートを入力します (既定値は 50111 です)。  
  
    3.  WebHCat サービスにアクセスするときに使用する **認証** 方法を選択します。 使用できる値は、 **[基本]** と **[Kerberos]** です。  
  
         ![Hadoop 接続マネージャー エディターと基本認証のスクリーンショット](../../integration-services/connection-manager/media/hadoop-cm-basic.png "Hadoop 接続マネージャー エディターと基本認証")  
  
         ![Hadoop 接続マネージャー エディターと Kerberos 認証のスクリーンショット](../../integration-services/connection-manager/media/hadoop-cm-kerberos.png "Hadoop 接続マネージャー エディターと Kerberos 認証")  
  
    4.  **[WebHCat User]** (WebHCat ユーザー) に、WebHCat へのアクセスが許可されている **ユーザー** を入力します。  
  
    5.  **[Kerberos]** 認証を選択した場合は、ユーザーの **パスワード** と **ドメイン**を入力します。  
  
4.  HDFS との間でデータをコピーするために **WebHDFS** オプションを有効にする場合は、次の操作を行います。 
  
    1.  **[WebHDFS Host]** (WebHDFS ホスト) に、WebHDFS サービスをホストするサーバーを入力します。  
  
    2.  **[WebHDFS Port]** (WebHDFS ポート) に、WebHDFS サービスのポートを入力します (既定値は 50070 です)。  
  
    3.  WebHDFS サービスにアクセスするときに使用する **認証** 方法を選択します。 使用できる値は、 **[基本]** と **[Kerberos]** です。  
  
    4.  **[WebHDFS User]** (WebHDFS ユーザー) に、HDFS へのアクセスが許可されているユーザーを入力します。  
  
    5.  **[Kerberos]** 認証を選択した場合は、ユーザーの **パスワード** と **ドメイン**を入力します。  
  
5.  **[接続テスト]** を選択します (有効にした接続のみがテストされます)。  
  
6.  **[OK]** を選択して、ダイアログ ボックスを閉じます。  

## <a name="connect-with-kerberos-authentication"></a>Kerberos 認証を使用した接続
Hadoop 接続マネージャーで Kerberos 認証を使用できるようにオンプレミス環境を設定する方法は 2 つあります。 状況に合う方法を選択することができます。
-   オプション 1:[SSIS コンピューターを Kerberos 領域に参加させる](#kerberos-join-realm)
-   オプション 2:[Windows ドメインと Kerberos 領域の間の相互信頼関係を有効にする](#kerberos-mutual-trust)

### <a name="kerberos-join-realm"></a>オプション 1: SSIS コンピューターを Kerberos 領域に参加させる

#### <a name="requirements"></a>要件:

-   ゲートウェイ コンピューターは Kerberos 領域に参加する必要があり、Windows ドメインに参加することはできません。

#### <a name="how-to-configure"></a>構成方法:

SSIS コンピューター:

1.  **Ksetup** ユーティリティを実行して、Kerberos Key Distribution Center (KDC) サーバーと領域を構成します。

    コンピューターはワークグループのメンバーとして構成する必要があります。これは、Kerberos 領域が Windows ドメインとは異なるためです。 次の例のように Kerberos 領域を設定し、KDC サーバーを追加します。 `REALM.COM` は、必要に応じて実際の領域に置き換えます。

    ```    
    C:> Ksetup /setdomain REALM.COM`
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    ```

    これらのコマンドを実行した後に、コンピューターを再起動します。

2.  **Ksetup** コマンドを実行して構成を確認します。 出力は次の例のようになります。

    ```
    C:> Ksetup
    default realm = REALM.COM (external)
    REALM.com:
        kdc = <your_kdc_server_address>
    ```

### <a name="kerberos-mutual-trust"></a>オプション 2: Windows ドメインと Kerberos 領域の間の相互信頼関係を有効にする

#### <a name="requirements"></a>要件:
-   ゲートウェイ コンピューターは Windows ドメインに参加する必要があります。
-   ドメイン コントローラーの設定を更新するアクセス許可が必要です。

#### <a name="how-to-configure"></a>構成方法:

> [!NOTE]
> 次のチュートリアルの `REALM.COM` と `AD.COM` を、必要に応じて実際の領域とドメイン コントローラーに置き換えます。

KDC サーバー:

1.  **krb5.conf** ファイルの KDC 構成を編集します。 次の構成テンプレートを参照して、KDC が Windows ドメインを信頼することを許可します。 既定で、この構成は **/etc/krb5.conf** にあります。

    ```
    [logging]
    default = FILE:/var/log/krb5libs.log
    kdc = FILE:/var/log/krb5kdc.log
    admin_server = FILE:/var/log/kadmind.log

    [libdefaults]
    default_realm = REALM.COM
    dns_lookup_realm = false
    dns_lookup_kdc = false
    ticket_lifetime = 24h
    renew_lifetime = 7d
    forwardable = true

    [realms]
    REALM.COM = {
        kdc = node.REALM.COM
        admin_server = node.REALM.COM
        }
    AD.COM = {
        kdc = windc.ad.com
        admin_server = windc.ad.com
        }

    [domain_realm]
    .REALM.COM = REALM.COM
    REALM.COM = REALM.COM
    .ad.com = AD.COM
    ad.com = AD.COM

    [capaths]
    AD.COM = {
        REALM.COM = .
        }
    ```

    構成が完了したら、KDC サービスを再起動します。

2.  KDC サーバーで **krbtgt/REALM.COM\@AD.COM** という名前のプリンシパルを準備します。 次のコマンドを実行します。

    `Kadmin> addprinc krbtgt/REALM.COM@AD.COM`

3.  **hadoop.security.auth_to_local** HDFS サービス構成ファイルに `RULE:[1:$1@$0](.*@AD.COM)s/@.*//` を追加します。

ドメイン コントローラー:

1.  次の **Ksetup** コマンドを実行して、領域のエントリを追加します。

    ```
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
    ```

2.  Windows ドメインから Kerberos 領域への信頼関係を確立します。 次の例で、`[password]` はプリンシパル **krbtgt/REALM.COM\@AD.COM** のパスワードです。

    `C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /password:[password]`

3.  Kerberos で使用する暗号化アルゴリズムを選択します。

    1. **[サーバー マネージャー]**  >  **[グループ ポリシーの管理]**  >  **[ドメイン]** の順に選択します。 次に、 **[グループ ポリシー オブジェクト]**  >  **[Default or Active Domain Policy]\(既定またはアクティブなドメイン ポリシー\)**  >  **[編集]** の順に選択します。

    2. **グループ ポリシー管理エディター**のポップアップ ウィンドウで、 **[コンピューターの構成]**  >  **[ポリシー]**  >  **[Windows の設定]** の順に選択します。 次に、 **[セキュリティ設定]**  >  **[ローカル ポリシー]**  >  **[セキュリティ オプション]** の順に選択します。 **[ネットワーク セキュリティ: Kerberos で許可する暗号化の種類を構成する]** を構成します。

    3. KDC への接続に使用する暗号化アルゴリズムを選択します。 通常は任意のオプションを選択できます。

        ![Kerberos の暗号化の種類のスクリーンショット](media/hadoop-connection-manager/config-encryption-types-for-kerberos.png)

    4. **Ksetup** コマンドを使用して、特定の領域に使用する暗号化アルゴリズムを指定します。

        `C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96`

4.  Windows ドメインで Kerberos プリンシパルを使用するには、ドメイン アカウントと Kerberos プリンシパル間のマッピングを作成します。

    1. **[管理ツール]**  >  **[Active Directory ユーザーとコンピューター]** の順に選択します。

    2. **[表示]**  >  **[高度な機能]** の順に選択して、高度な機能を構成します。

    3. マッピングを作成するアカウントを見つけ、右クリックして **[名前のマッピング]** を表示し、 **[Kerberos 名]** タブを選択します。

    4. 領域からプリンシパルを追加します。

        ![[セキュリティ ID マッピング] ダイアログ ボックスのスクリーンショット](media/hadoop-connection-manager/map-security-identity.png)

ゲートウェイ コンピューター:

次の **Ksetup** コマンドを実行して、領域のエントリを追加します。

    ```
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
    ```

## <a name="see-also"></a>参照  
 [Hadoop Hive Task](../../integration-services/control-flow/hadoop-hive-task.md)   
 [Hadoop Pig Task](../../integration-services/control-flow/hadoop-pig-task.md)   
 [Hadoop ファイル システム タスク](../../integration-services/control-flow/hadoop-file-system-task.md)  
  
  
