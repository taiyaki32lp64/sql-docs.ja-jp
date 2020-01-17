---
title: SMB ストレージ FCI の構成 - SQL Server on Linux
description: SQL Server on Linux 用の SMB ストレージを使用してフェールオーバー クラスター インスタンス (FCI) を構成する方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 498518fbc119629d2e7da7717b1f6e41c68984ce
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558582"
---
# <a name="configure-failover-cluster-instance---smb---sql-server-on-linux"></a>フェールオーバー クラスター インスタンスの構成 - SMB - SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Linux 上のフェールオーバー クラスター インスタンス (FCI) の SMB ストレージを構成する方法について説明します。 
 
Windows 以外の環境では、通常、SMB は Common Internet File System (CIFS) 共有と呼ばれ、Samba を介して実装されます。 Windows の環境では、SMB 共有へのアクセスは、\\SERVERNAME\SHARENAME のように行われます。 Linux ベースの SQL Server インストールの場合、SMB 共有はフォルダーとしてマウントする必要があります。

## <a name="important-source-and-server-information"></a>ソースとサーバーに関する重要な情報

SMB を正常に使用するためのヒントと注意事項を次に示します。
- SMB 共有は、Windows、Linux、または、SMB 3.0 以降を使用している場合はアプライアンスからでも実行できます。 Samba と SMB 3.0 の詳細については、「[SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0)」を参照して、Samba の実装が SMB 3.0 に準拠しているかどうかを確認してください。
- SMB 共有は高可用性である必要があります。
- SMB 共有にセキュリティが適切に設定されている必要があります。 /etc/samba/smb.conf の例を次に示します。ここで、SQLData1 は共有の名前です。

![05-smbsource][1]

## <a name="instructions"></a>Instructions

1. FCI の構成に参加するいずれかのサーバーを選択します。 どれを選んでも問題ありません。
   
1. mssql ユーザーに関する情報を取得します。
   
   ```bash
    sudo id mssql
   ```
   
   uid、gid、およびグループに注目してください。 
   
1. `sudo smbclient -L //NameOrIP/ShareName -U User` を実行します。
   
   \<NameOrIP> は、SMB 共有をホストしているサーバーの DNS 名または IP アドレスです。
   
   \<ShareName> は SMB 共有の名前です。 
   
1. システム データベース、または既定のデータの場所に格納されているものについては、次の手順に従います。 それ以外の場合は手順 5 に進みます。 
   
   1. 作業中のサーバーで SQL Server が停止していることを確認します。
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 完全にスーパーユーザーに切り替えます。 成功した場合は、確認応答を何も受け取りません。
      
      ```bash
      sudo -i
      ```
      
   1. mssql ユーザーに切り替えます。 成功した場合は、確認応答を何も受け取りません。
      
      ```bash
      su mssql
      ```
      
   1. SQL Server のデータ ファイルとログ ファイルを格納するための一時ディレクトリを作成します。 成功した場合は、確認応答を何も受け取りません。
      
      ```bash
      mkdir <TempDir>
      ```
      
      \<TempDir> はフォルダーの名前です。 次の例では、/var/opt/mssql/tmp という名前のフォルダーを作成します。
      
      ```bash
      mkdir /var/opt/mssql/tmp
      ```
      
   1. SQL Server のデータ ファイルとログ ファイルを一時ディレクトリにコピーします。 成功した場合は、確認応答を何も受け取りません。
      
      ```bash
      cp /var/opt/mssql/data/* <TempDir>
      ```
      
      \<TempDir> は、前の手順で指定したフォルダーの名前です。
      
   1. ファイルがディレクトリ内にあることを確認します。
      
      ```bash
      ls <TempDir>
      ```
      
      \<TempDir> は、手順 d で作成したフォルダーの名前です。
      
   1. 既存の SQL Server データ ディレクトリからファイルを削除します。 成功した場合は、確認応答を何も受け取りません。
      
      ```bash
      rm - f /var/opt/mssql/data/*
      ```
      
   1. ファイルが削除されていることを確認します。 
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. 「exit」と入力して、ルート ユーザーに切り替えます。
      
   1. SQL Server データフォルダーに SMB 共有をマウントします。 成功した場合は、確認応答を何も受け取りません。 この例は、Windows Server ベースの SMB 3.0 共有に接続するための構文を示しています。
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> /var/opt/mssql/data -o vers=3.0,username=<UserName>,password=<Password>,domain=<domain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName> は、SMB 共有を使用するサーバーの名前です
      
      \<ShareName> は共有の名前です
      
      \<UserName> は、共有にアクセスするユーザーの名前です
      
      \<Password> はユーザーのパスワードです
      
      \<domain> は Active Directory の名前です
      
      \<mssqlUID> は mssql ユーザーの UID です 
      
      \<mssqlGID> は mssql ユーザーの GID です
      
   1. スイッチなしでマウントを発行して、マウントが成功したことを確認します。
      
      ```bash
      mount
      ```
      
   1. mssql ユーザーに切り替えます。 成功した場合は、確認応答を何も受け取りません。
      
      ```bash
      su mssql
      ```
      
   1. 一時ディレクトリ /var/opt/mssql/data からファイルをコピーします。 成功した場合は、確認応答を何も受け取りません。
      
      ```bash
      cp /var/opt/mssql/tmp/* /var/opt/mssql/data
      ```
      
   1. ファイルがあることを確認します。
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. 「exit」と入力して mssql を終了します 
      
   1. 「exit」と入力してルートを終了します
   
   1. SQL Server を起動します。 すべてが正しくコピーされ、セキュリティが正しく適用されている場合、SQL Server は起動済みと表示されます。
      
      ```bash
      sudo systemctl start mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. さらにテストするには、データベースを作成して、アクセス許可が適切であることを確認します。 次の例では、Transact-SQL を使用します。SSMS を使用できます。
      
      ![10_testcreatedb][2] 
      
   1. SQL Server を停止し、シャットダウンされていることを確認します。 他のディスクを追加またはテストする場合は、それらが追加されテストされるまで SQL Server をシャットダウンしないでください。
      
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 完了した場合にのみ、共有のマウントを解除します。 それ以外の場合は、ディスクの追加後またはテスト完了後にマウントを解除します。
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName> は、SMB ホストの IP アドレスまたは名前です
      
      \<ShareName> は共有の名前です
      
      \<FolderMountedIn> は、SMB がマウントされているフォルダーの名前です
      
5. ユーザー データベースやバックアップなどのシステム データベース以外のものについては、次の手順に従います。 既定の場所のみを使用する場合は、手順 14 に進みます。
   
   1. スーパーユーザーになるように切り替えます。 成功した場合は、確認応答を何も受け取りません。
      
      ```bash
      sudo -i
      ```
      
   1. SQL Server によって使用されるフォルダーを作成します。 
      
      ```bash
      mkdir <FolderName>
      ```
      
      \<FolderName> はフォルダーの名前です。 正しい場所にない場合は、フォルダーの完全なパスを指定する必要があります。 次の例では、/var/opt/mssql/userdata という名前のフォルダーを作成します。
      
      ```bash
      mkdir /var/opt/mssql/userdata
      ```
      
   1. SQL Server データフォルダーに SMB 共有をマウントします。 成功した場合は、確認応答を何も受け取りません。 次の例は、Samba ベースの SMB 3.0 共有に接続するための構文を示しています。
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> <FolderName> -o vers=3.0,username=<UserName>,password=<Password>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName> は、SMB 共有を使用するサーバーの名前です
      
      \<ShareName> は共有の名前です
      
      \<FolderName> は、最後の手順で作成したフォルダーの名前です  
      
      \<UserName> は、共有にアクセスするユーザーの名前です
      
      \<Password> はユーザーのパスワードです
      
      \<mssqlUID> は mssql ユーザーの UID です
      
      \<mssqlGID> は mssql ユーザーの GID です。
      
   1. スイッチなしでマウントを発行して、マウントが成功したことを確認します。
   
   1. スーパーユーザーではなくなるよう、「Exit」と入力します。
   
   1. テストするには、そのフォルダーにデータベースを作成します。 次の例では、sqlcmd を使用してデータベースを作成し、コンテキストをそれに切り替え、ファイルが OS レベルで存在することを確認した後、一時的な場所を削除します。 SSMS を使用できます。
   
   1. 共有のマウントを解除します 
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName> は、SMB ホストの IP アドレスまたは名前です
      
      \<ShareName> は共有の名前です
      
      \<FolderMountedIn> は、SMB がマウントされているフォルダーの名前です。
   
1. その他のノードでこれらの手順を繰り返します。

これで、FCI を構成する準備が整いました。

## <a name="next-steps"></a>次のステップ

[フェールオーバー クラスター インスタンスの構成 - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 
