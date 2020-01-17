---
title: HDFS の階層制御の S3 のマウント
titleSuffix: SQL Server big data clusters
description: この記事では、外部の S3 ファイル システムを [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]上の HDFS にマウントして HDFS の階層化を構成する方法について説明します。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 653f9a48c03df18fc0591f7bd8060d951567c779
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652302"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>ビッグ データ クラスターに HDFS 階層制御のための S3 をマウントする方法

次のセクションでは、S3 ストレージ データ ソースを使用して HDFS 階層制御を構成する方法の例を示します。

## <a name="prerequisites"></a>Prerequisites

- [展開済みのビッグ データ クラスター](deployment-guidance.md)
- [ビッグ データ ツール](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**
- S3 バケットにデータを作成してアップロードする 
  - CSV または Parquet ファイルを S3 バケットにアップロードします。 これは、ビッグ データ クラスターの HDFS にマウントされる外部 HDFS データです。

## <a name="access-keys"></a>アクセス キー

### <a name="set-environment-variable-for-access-key-credentials"></a>アクセス キー資格情報の環境変数を設定する

ビッグ データ クラスターにアクセスできるクライアント マシンでコマンド プロンプトを開きます。 次の形式を使用して環境変数を設定します。 資格情報はコンマ区切りの一覧に含まれている必要があります。 Windows では 'set' コマンドが使用されます。 Linux を使用している場合は、代わりに 'export' を使用してください。

   ```text
    set MOUNT_CREDENTIALS=fs.s3a.access.key=<Access Key ID of the key>,
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > S3 アクセスキーを作成する方法の詳細については、[S3 アクセス キー](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys)に関する記事を参照してください。

## <a id="mount"></a> リモート HDFS ストレージをマウントする

アクセス キーを使用して資格情報ファイルを準備したので、マウントを開始することができます。 次の手順では、S3 のリモート HDFS ストレージを、ビッグ データ クラスターのローカル HDFS ストレージにマウントします。

1. **kubectl** を使用して、ビッグ データ クラスター内のエンドポイント **controller-svc-external** サービスの IP アドレスを検索します。 **External-IP** を検索します。

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. クラスターのユーザー名とパスワードによるコントローラー エンドポイントの外部 IP アドレスを使用して **azdata** でログインします。

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
   
1. 上の手順に続けて環境変数 MOUNT_CREDENTIALS を設定する

1. **azdata bdc hdfs mount create** を使用して、Azure でリモート HDFS ストレージをマウントします。 次のコマンドを実行する前に、プレースホルダーの値を置き換えます。

   ```bash
   azdata bdc hdfs mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > mount create コマンドは非同期です。 現時点では、マウントが成功したかどうかを示すメッセージはありません。 [[状態]](#status) セクションで、マウントの状態を確認してください。

正常にマウントされていれば、HDFS データに対してクエリを実行し、そのデータに対して Spark ジョブを実行できます。 これは、`--mount-path` によって指定された場所にあるビッグ データ クラスターの HDFS に表示されます。

## <a id="status"></a> マウントの状態を取得する

ビッグ データ クラスター内のすべてのマウントの状態を一覧表示するには、次のコマンドを使用します。

```bash
azdata bdc hdfs mount status
```

HDFS で指定されたパスのマウントの状態を一覧表示するには、次のコマンドを使用します。

```bash
azdata bdc hdfs mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>マウントを更新する

次の例では、マウントを更新しています。

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> マウントを削除する

マウントを削除するには、**azdata bdc hdfs mount delete** コマンドを使用して、HDFS で次のマウント パスを指定します。

```bash
azdata bdc hdfs mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>次の手順

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の概要](big-data-cluster-overview.md)」を参照してください。
