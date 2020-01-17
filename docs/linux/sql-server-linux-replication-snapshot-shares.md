---
title: スナップショット フォルダー共有の構成
titleSuffix: SQL Server on Linux
description: Linux 上の SQL Server レプリケーションでスナップショット フォルダーの共有を構成する方法について説明します。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c5deaf7fbe62b30140f476a37ad096d080e00c49
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558355"
---
# <a name="configure-replication-snapshot-folder-with-shares"></a>共有を含むレプリケーション スナップショット フォルダーを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

スナップショット フォルダーは、共有として指定したディレクトリです。このフォルダーの読み取りと書き込みをするエージェントには、このフォルダーへのアクセスを可能にする十分な権限が必要です。

![レプリケーションの図][1]

### <a name="replication-snapshot-folder-share-explained"></a>レプリケーション スナップショット フォルダー共有の説明

例の前に、SQL Server がレプリケーションで samba 共有を使用する方法について説明します。 このしくみの基本的な例は次のとおりです。

1. samba 共有は、パブリッシャー上のレプリケーション エージェント によって `/local/path1` に書き込まれるファイルを、サブスクライバーが参照できるように構成されます。
2. SQL Server は、ディストリビューション サーバー上にパブリッシャーを設定するときに共有パスを使用するように構成されます。これによって、すべてのインスタンスが `//share/path` を参照します。
3. SQL Server は、`//share/path` からローカル パスを探して、ファイルを見つける場所を認識します。
4. SQL Server は、samba 共有によってサポートされるローカル パスに対して読み取りと書き込みを行います。


## <a name="configure-a-samba-share-for-the-snapshot-folder"></a>スナップショット フォルダーの samba 共有を構成する 

レプリケーション エージェントは、他のマシンのスナップショット フォルダーにアクセスするために、レプリケーション ホスト間の共有ディレクトリを必要とします。 たとえば、トランザクション プル レプリケーションでは、ディストリビューション エージェントはサブスクライバーに存在するため、アーティクルを取得するためにディストリビューターへのアクセスが必要です。 このセクションでは、2 つのレプリケーション ホストに対して samba 共有を構成する方法の例について説明します。


## <a name="steps"></a>手順

例としては、Samba を使用して、ホスト 1 (ディストリビューター) 上のスナップショット フォルダーがホスト 2 (サブスクライバー) で共有されるように構成します。 

### <a name="install-and-start-samba-on-both-machines"></a>両方のマシンに Samba をインストールして起動する 

Ubuntu の場合:

```bash
sudo apt-get -y install samba
sudo service smbd restart
```

RHEL の場合:

```bash
sudo yum install samba
sudo service smb start
sudo service smb status
```

### <a name="on-host-1-distributor-set-up-the-samba-share"></a>ホスト 1 (ディストリビューター) で Samba 共有を設定する 

1. Samba のユーザーとパスワードを設定します。

  ```bash
  sudo smbpasswd -a mssql 
  ```

1. `/etc/samba/smb.conf` を編集して次のエントリを含め、*share_name* および *path* フィールドに入力します。
 ```bash
  <[share_name]>
  path = </local/path/on/host/1>
  writable = yes
  create mask = 770
  directory mask 
  valid users = mssql 
  ```

  **例**

  ```bash
  [mssql_data]    <- Name of the shared directory
  path = /var/opt/mssql/repldata <- location of directory we wish to share
  writable = yes  <- determines if the share is writable from other hosts
  create mask = 770  <- Linux permissions for files created 
  directory mask = 770 <- Linux permissions for directories created
  valid users = mssql   <- list of users who can login to this share
  ```

### <a name="on-host-2-subscriber--mount-the-samba-share"></a>ホスト 2 (サブスクライバー) で Samba 共有をマウントする

正しいパスを使用するようにコマンドを編集し、machine2 で次のコマンドを実行します。

  ```bash
  sudo mount //<name_of_host_1>/<share_name> </local/path/on/host/2> -o user=mssql,uid=mssql,gid=mssql
  ```

  **例**

  ```bash
  mount //host1/mssql_data /var/opt/mssql/repldata_shared -o user=mssql,uid=mssql,gid=mssql

  user=mssql <- sets the login name for samba
  uid=mssql   <- makes the mssql user as the owner of the mounted directory
  gid=mssql   <- sets the mssql group as the owner of the mounted directory
  ```

### <a name="on-both-hosts--configure-sql-server-on-linux-instances-to-use-snapshot-share"></a>両方のホストでスナップショット共有を使用するように SQL Server on Linux インスタンスを構成する

次のセクションを両方のマシンの `mssql.conf` に追加します。 どこであっても //share/path の samba 共有を使用します。 この例では、`//host1/mssql_data` です。

  ```bash
  [uncmapping]
  //share/path = /local/path/on/hosts/
  ```

  **例**

  host1:

  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/1
  ```

  host2:
  
  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/2
  ```

### <a name="configuring-publisher-with-shared-paths"></a>共有パスを使用するようにパブリッシャーを構成する

* レプリケーションを設定するときに、共有パス (`//host1/mssql_data` など) を使用します。
* `//host1/mssql_data` をローカル ディレクトリにマップすると、マッピングが `mssql.conf` に追加されます。

## <a name="next-steps"></a>次のステップ

[概念:Linux での SQL Server のレプリケーション](sql-server-linux-replication.md)

[レプリケーション ストアド プロシージャ](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

[1]: ./media/sql-server-linux-replication-snapshot-shares/image1.png
