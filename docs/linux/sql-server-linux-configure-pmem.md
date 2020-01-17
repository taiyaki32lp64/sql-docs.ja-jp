---
title: SQL Server on Linux 用に永続メモリ (PMEM) を構成する
description: この記事では、Linux で PMEM を構成する手順について説明します。
ms.custom: seo-lt-2019
author: briancarrig
ms.author: brcarrig
ms.reviewer: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 0b5f86dac62c371a9e4dda607cbd9ec7533a187a
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558615"
---
# <a name="how-to-configure-persistent-memory-pmem-for-sql-server-on-linux"></a>SQL Server on Linux 用に永続メモリ (PMEM) を構成する方法

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、SQL Server on Linux 用に永続メモリ (PMEM) を構成する方法について説明します。 Linux での PMEM のサポートは SQL Server 2019 で導入されました。

## <a name="overview"></a>概要

SQL Server 2016 では、非揮発性 DIMM のサポートと、[NVDIMM でのログ末尾のキャッシング]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/)と呼ばれる最適化が導入されました。 このような最適化によって、ログ バッファーを強化して永続ストレージにするために必要な操作数を削減することができました。 これは、DAX モードでの永続メモリ デバイスに対する Windows Server の直接アクセスを活用しています。

SQL Server 2019 では、Linux に対する永続メモリ (PMEM) デバイスのサポートが拡張されています。これにより、PMEM に配置されるデータ ファイルとトランザクション ログ ファイルの完全なエンライトメントが提供されます。 エンライトメントは、効率的なユーザー スペースの `memcpy()` 操作を使用してストレージ デバイスにアクセスする方法を意味します。 SQL Server は、ファイル システムとストレージ スタックを経由せずに、Linux での DAX サポートを利用してデータをデバイスに直接配置します。これにより待機時間が短縮されます。

## <a name="enable-enlightenment-of-database-files"></a>データベース ファイルのエンライトメントを有効にする
SQL Server on Linux でデータベースファイルのエンライトメントを有効にするには、次の手順に従います。

1. デバイスを構成します。

  Linux では `ndctl` ユーティリティを使用します。

  - `ndctl` をインストールして、PMEM デバイスを構成します。 詳しくは[こちら](https://docs.pmem.io/getting-started-guide/installing-ndctl)をご覧ください。
  - [ndctl] を使用して名前空間を作成します。

  ```bash 
  ndctl create-namespace -f -e namespace0.0 --mode=fsdax* --map=mem
  ```

  >[!NOTE]
  >バージョンが 59 よりも前の `ndctl` を使用している場合は `--mode=memory`を使用します。

  `ndctl` を使用して名前空間を確認します。 サンプル出力を次に示します。

```bash
ndctl list
[
  {
    "dev":"namespace0.0",
    "mode":"memory",
    "size":1099511627776,
    "blockdev":"pmem0",
    "numa_node":0
  }
]
```

  - PMEM デバイスの作成とマウント

    例: XFS

    ```bash
    mkfs.xfs -f /dev/pmem0
    mount -o dax,noatime /dev/pmem0 /mnt/dax
    xfs_io -c "extsize 2m" /mnt/dax
    ```

    例: EXT4

    ```bash
    mkfs.ext4 -b 4096 -E stride=512 -F /dev/pmem0
    mount -o dax,noatime /dev/pmem0 /mnt/dax
    ```

  デバイスを ndctl を使用して構成し、フォーマットとマウントを行ったら、データベース ファイルを配置できます。 また、新しいデータベースを作成することもできます。 

1. PMEM デバイスは O_DIRECT セーフであるため、トレース フラグ 3979 を有効にして強制フラッシュ メカニズムを無効にします。 このトレース フラグはスタートアップ トレース フラグであるため、mssql-conf ユーティリティを使用して有効にする必要があります。 これはサーバー全体の構成変更であることに注意してください。データ整合性を確保するために強制フラッシュ メカニズムが必要となる O_DIRECT 非準拠デバイスがある場合は、このトレース フラグを使用しないでください。 詳しくは、 https://support.microsoft.com/help/4131496/enable-forced-flush-mechanism-in-sql-server-2017-on-linux をご覧ください。

1. SQL Server を再起動してください。

## <a name="next-steps"></a>次のステップ

SQL Server on Linux について詳しくは、「[SQL Server on Linux](sql-server-linux-overview.md)」をご覧ください。
