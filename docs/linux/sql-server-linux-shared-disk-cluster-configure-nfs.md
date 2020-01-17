---
title: NFS ストレージ FCI の構成 - SQL Server on Linux
description: SQL Server 用の NFS ストレージを使用してフェールオーバー クラスター インスタンス (FCI) を構成する方法について説明します。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 35f6dc79756c192419dbe3a8962d5dcdfeea8aef
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558337"
---
# <a name="configure-failover-cluster-instance---nfs---sql-server-on-linux"></a>フェールオーバー クラスター インスタンスを構成する - NFS - SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Linux 上のフェールオーバー クラスター インスタンス (FCI) 用の NFS ストレージを構成する方法について説明します。 

NFS (ネットワーク ファイル システム) は、Linux 環境ではディスクを共有するための一般的な方法ですが、Windows ではそうではありません。 iSCSI と同様に、NFS は、SQL Server のストレージ要件を満たす限り、サーバーまたはある種のアプライアンスやストレージ ユニットに構成できます。

## <a name="important-nfs-server-information"></a>NFS サーバーに関する重要な情報

NFS をホストするソース (Linux サーバーまたはその他のもの) は、バージョン4.2 以降を使用しているか、それに準拠している必要があります。 それより前のバージョンは、SQL Server on Linux では動作しません。

NFS サーバーで共有されるようにフォルダーを構成するときは、それらが次のガイドラインの一般的なオプションに従っていることを確認してください。
- フォルダーを読み書きできるように `rw`
- フォルダーへの書き込みが保証されるように `sync`
- オプションとして `no_root_squash` を使用しないでください。セキュリティ上のリスクと見なされます
- フォルダーにフル権限 (777) が適用されていることを確認します

アクセスに対してセキュリティ標準が適用されていることを確認します。 フォルダーを構成するときは、FCI に参加しているサーバーだけが NFS フォルダーを参照するようにします。 Linux ベースの NFS ソリューション上で変更された /etc/exports の例を次に示します。フォルダーは FCIN1 および FCIN2 に制限されています。

![05-nfsacl][1]

## <a name="instructions"></a>Instructions

1. FCI の構成に参加するいずれかのサーバーを選択します。 どれを選んでも問題ありません。 

2. サーバーで NFS サーバー上のマウントを参照できることを確認します。

    ```bash
    sudo showmount -e <IPAddressOfNFSServer>
    ```

    \<IPAddressOfNFSServer> は、使用する NFS サーバーの IP アドレスです。

3. システム データベース、または既定のデータの場所に格納されているものについては、以下の手順に従います。 それ以外の場合は、手順 4 に進みます。
 
   * 作業中のサーバーで SQL Server が停止していることを確認します。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
   * 完全にスーパーユーザーに切り替えます。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    sudo -i
    ```

   * mssql ユーザーに切り替えます。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    su mssql
    ```

   * SQL Server のデータ ファイルとログ ファイルを格納するための一時ディレクトリを作成します。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir> はフォルダーの名前です。 次の例では、/var/opt/mssql/tmp という名前のフォルダーを作成します。

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   * SQL Server のデータ ファイルとログ ファイルを一時ディレクトリにコピーします。 成功した場合は、確認応答を何も受け取りません。
    
    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir> は、前の手順で指定したフォルダーの名前です。

   * ファイルがディレクトリ内にあることを確認します。

    ```bash
    ls TempDir
    ```

    \<TempDir> は、手順 d で作成したフォルダーの名前です。

   * 既存の SQL Server データ ディレクトリからファイルを削除します。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    rm - f /var/opt/mssql/data/*
    ```

   * ファイルが削除されていることを確認します。 

    ```bash
    ls /var/opt/mssql/data
    ```
    
   * 「exit」と入力して、ルート ユーザーに切り替えます。

   * SQL Server データ フォルダーに NFS 共有をマウントします。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer> は、使用する NFS サーバーの IP アドレスです 

    \<FolderOnNFSServer> は、NFS 共有の名前です。 次の例の構文は、手順 2 の NFS の情報と一致します。

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

   * スイッチなしでマウントを発行して、マウントが成功したことを確認します。

    ```bash
    mount
    ```

    ![10-mountnoswitches][2]

   * mssql ユーザーに切り替えます。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    su mssql
    ```

   * 一時ディレクトリ /var/opt/mssql/data からファイルをコピーします。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssqldata
    ```

   * ファイルがあることを確認します。

    ```bash
    ls /var/opt/mssql/data
    ```

   * 「exit」と入力して mssql を終了します 
    
   * 「exit」と入力してルートを終了します

   * SQL Server を起動します。 すべてが正しくコピーされ、セキュリティが正しく適用されている場合、SQL Server は起動済みと表示されます。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
    
   * データベースを作成して、セキュリティが適切に設定されていることをテストします。 次の例では、Transact-SQL を使用して行っています。SSMS で行うこともできます。
 
    ![CreateTestdatabase][3]

   * SQL Server を停止し、シャットダウンされていることを確認します。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   * 他の NFS マウントを作成していない場合は、共有のマウントを解除します。 作成している場合は、マウントを解除しないでください。

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer> は、使用する NFS サーバーの IP アドレスです

    \<FolderOnNFSServer> は、NFS 共有の名前です

    \<FolderMountedIn> は、前の手順で作成したフォルダーです。 

4. ユーザー データベースやバックアップなどのシステム データベース以外のものについては、次の手順に従います。 既定の場所のみを使用する場合は、手順 5 に進みます。

   * スーパーユーザーになるように切り替えます。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    sudo -i
    ```

   * SQL Server によって使用されるフォルダーを作成します。 

    ```bash
    mkdir <FolderName>
    ```

    \<FolderName> はフォルダーの名前です。 正しい場所にない場合は、フォルダーの完全なパスを指定する必要があります。 次の例では、/var/opt/mssql/userdata という名前のフォルダーを作成します。

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   * 前の手順で作成したフォルダーに NFS 共有をマウントします。 成功した場合は、確認応答を何も受け取りません。

    ```bash
    Mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn> -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer> は、使用する NFS サーバーの IP アドレスです

    \<FolderOnNFSServer> は、NFS 共有の名前です

    \<FolderToMountIn> は、前の手順で作成したフォルダーです。 次に例を示します。 

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci2 /var/opt/mssql/userdata -o nfsvers=4.2,timeo=14,intr
    ```

   * スイッチなしでマウントを発行して、マウントが成功したことを確認します。
  
   * スーパーユーザーではなくなるよう、「Exit」と入力します。

   * テストするには、そのフォルダーにデータベースを作成します。 次の例では、sqlcmd を使用してデータベースを作成し、コンテキストをそれに切り替え、ファイルが OS レベルで存在することを確認した後、一時的な場所を削除します。 SSMS を使用できます。

    ![15-createtestdatabase][4]
 
   * 共有のマウントを解除します 

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer> は、使用する NFS サーバーの IP アドレスです
    
    \<FolderOnNFSServer> は、NFS 共有の名前です

    \<FolderMountedIn> は、前の手順で作成したフォルダーです。 次に例を示します。 
 
5. その他のノードでこれらの手順を繰り返します。


## <a name="next-steps"></a>次のステップ

[フェールオーバー クラスター インスタンスの構成 - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/05-nfsacl.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/10-mountnoswitches.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/20-createtestdatabase.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/15-createtestdatabase.png
