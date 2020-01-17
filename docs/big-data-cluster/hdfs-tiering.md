---
title: HDFS の階層化を構成する
titleSuffix: SQL Server big data clusters
description: この記事では、外部の Azure Data Lake Storage ファイル システムを [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 上の HDFS にマウントするように、HDFS の階層化を構成する方法について説明します。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 673b3eed760af4b36c494e2dd45cdfc8ed8e8dc8
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706053"
---
# <a name="configure-hdfs-tiering-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] で HDFS の階層化を構成する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

HDFS の階層化により、HDFS に外部の HDFS と互換性のあるファイル システムをマウントする機能が提供されます。 この記事では、SQL Server ビッグ データ クラスターで HDFS の階層化を構成する方法について説明します。 現時点では、Azure Data Lake Storage Gen2 および Amazon S3 への接続がサポートされています。 

## <a name="hdfs-tiering-overview"></a>HDFS の階層化の概要

階層化により、アプリケーションは、データがローカル HDFS に存在しているかのように、さまざまな外部ストアのデータにシームレスにアクセスできます。 マウントはメタデータ操作であり、外部ファイル システムの名前空間を記述するメタデータがローカルの HDFS にコピーされます。 このメタデータには、外部ディレクトリおよびファイルに関する情報と共に、そのアクセス許可と ACL が含まれます。 クエリなどを通じてデータ自体にアクセスする場合、対応するデータは要求時にのみコピーされます。 これで、SQL Server ビッグ データ クラスターから外部ファイル システム データにアクセスできるようになりました。 このデータに対して Spark ジョブと SQL クエリを実行する方法は、クラスター上の HDFS に格納されているローカル データに対して実行する方法と同じです。

### <a name="caching"></a>キャッシュ
現在、既定では、HDFS の総ストレージ容量の 1% が、マウントされたデータのキャッシュ用に予約されます。 キャッシュは、マウント全体のグローバル設定です。

> [!NOTE]
> HDFS の階層化は、Microsoft によって開発された機能です。以前のバージョンは、Apache Hadoop 3.1 ディストリビューションの一部としてリリースされています。 詳細については、[https://issues.apache.org/jira/browse/HDFS-9806](https://issues.apache.org/jira/browse/HDFS-9806) を参照してください。

以降のセクションでは、Azure Data Lake Storage Gen2 データソースを使用して HDFS 階層制御を構成する方法の例を示します。

## <a name="refresh"></a>更新

HDFS の階層化は更新をサポートします。 既存のマウントを更新して、リモート データの最新のスナップショットを入手します。

## <a name="prerequisites"></a>Prerequisites

- [展開済みのビッグ データ クラスター](deployment-guidance.md)
- [ビッグ データ ツール](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a name="mounting-instructions"></a>マウントの手順

Azure Data Lake Storage Gen2 および Amazon S3 への接続がサポートされています。 これらのストレージの種類に対するマウント方法については、次の記事を参照してください。

- [ビッグ データ クラスターに HDFS の階層化のための ADLS Gen2 をマウントする方法](hdfs-tiering-mount-adlsgen2.md)
- [ビッグ データ クラスターに HDFS の階層化のための S3 をマウントする方法](hdfs-tiering-mount-s3.md)

## <a id="issues"></a> 既知の問題と制限事項

次の一覧に、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] で HDFS の階層化を使用する場合の既知の問題と現在の制限事項を示します。

- マウントが `CREATING` 状態で長時間停止している場合は、ほとんどの場合、失敗しています。 このような場合は、コマンドを取り消し、必要に応じてマウントを削除します。 パラメーターと資格情報が正しいことを確認してから、再試行してください。

- 既存のディレクトリにマウントを作成することはできません。

- 既存のマウント内にマウントを作成することはできません。

- マウントポイントの先祖がいずれも存在しない場合は、既定値が r-xr-xr-x (555) に設定されたアクセス許可を使用してこれらが作成されます。

- マウントされるファイルの数とサイズによっては、マウントの作成に時間がかかることがあります。 この処理中は、マウントされたファイルはユーザーに表示されません。 マウントの作成時に、すべてのファイルが一時パスに追加されます。既定値は `/_temporary/_mounts/<mount-location>` になります。

- mount creation コマンドは非同期です。 コマンドが実行された後、マウントの状態を確認して、マウントの状態を把握できます。

- マウントの作成時に、 **--mount-path** に使用される引数は、基本的にマウントの一意の識別子です。 後続のコマンドで同じ文字列 (末尾に "/" がある場合はそれも含めて) を使用する必要があります。

- マウントは読み取り専用です。 マウントの下にディレクトリまたはファイルを作成することはできません。

- 変更できるディレクトリとファイルをマウントすることはお勧めしません。 マウントが作成されると、リモートの場所に対する変更や更新は、HDFS のマウントに反映されません。 リモートの場所で変更が発生した場合は、マウントを削除してから再作成して、更新された状態を反映することができます。

## <a name="next-steps"></a>次の手順

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の概要](big-data-cluster-overview.md)」を参照してください。
