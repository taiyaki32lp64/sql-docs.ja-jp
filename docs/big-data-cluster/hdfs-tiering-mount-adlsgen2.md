---
title: HDFS の階層制御の ADLS Gen2 のマウント
titleSuffix: How to mount ADLS Gen2
description: この記事では、外部の Azure Data Lake Storage ファイル システムを [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 上の HDFS にマウントするように、HDFS の階層化を構成する方法について説明します。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ddf088bc8f7ba3d53bb989145e778deb3472e2a7
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632780"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>ビッグ データ クラスターに HDFS 階層制御のための ADLS Gen2 をマウントする方法

次のセクションでは、Azure Data Lake Storage Gen2 データソースを使用して HDFS 階層制御を構成する方法の例を示します。

## <a name="prerequisites"></a>Prerequisites

- [展開済みのビッグ データ クラスター](deployment-guidance.md)
- [ビッグ データ ツール](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a id="load"></a> Azure Data Lake Storage にデータを読み込む

次のセクションでは、HDFS 階層制御をテストするための Azure Data Lake Storage Gen2 の設定方法について説明します。 Azure Data Lake Storage に既にデータが格納されている場合は、このセクションを省略して独自のデータを使用することができます。

1. [Data Lake Storage Gen2 機能を持つストレージ アカウントを作成します](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account)。

1. このストレージ アカウントに外部データ用の [BLOB コンテナー/ファイル システムを作成します](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal)。

1. CSV ファイルまたは Parquet ファイルをコンテナーにアップロードします。 これは、ビッグ データ クラスターの HDFS にマウントされる外部 HDFS データです。

## <a name="credentials-for-mounting"></a>マウントのための資格情報

### <a name="use-oauth-credentials-to-mount"></a>OAuth 資格情報を使用してマウントする

OAuth 資格情報を使用してマウントするには、次の手順に従う必要があります。

1. [Azure portal](https://portal.azure.com) にアクセスします
1. [Azure Active Directory] に移動します。 このサービスは、左側のナビゲーション バーに表示されています。
1. 右のナビゲーション バーで [アプリの登録] を選択し、新しい登録を作成します
1. Web アプリケーションを作成し、ウィザードに従います。 **ここで作成したアプリの名前を忘れないでください**。 この名前を承認されたユーザーとして ADLS アカウントに追加する必要があります。 また、アプリを選択したときの [概要] のアプリケーション クライアント ID も記録しておきます。
1. Web アプリケーションが作成されたら、[Certificates&secrets]\(証明書とシークレット\) に移動し、**新しいクライアント シークレット**を作成して、キーの期間を選択します。 シークレットを**追加**します。
1.  [アプリの登録] ページに戻り、上部にある [エンドポイント] をクリックします。 **OAuth トークン エンドポイント (v2) の URL を記録しておきます**
1. ここまでで、OAuth に関する次の内容をメモしておく必要があります。

    - Web アプリケーションの "アプリケーション クライアント ID"
    - クライアント シークレット
    - トークン エンドポイント

### <a name="adding-the-service-principal-to-your-adls-account"></a>ADLS アカウントへのサービス プリンシパルの追加

1. ポータルにもう一度移動し、お使いの ADLS ストレージ アカウントのファイル システムに移動して、左側のメニューで [アクセス制御 (IAM)] を選択します。
1. [ロールの割り当てを追加する] を選択します 
1. [ストレージ BLOB データ共同作成者] ロールを選択します
1. 上で作成した名前を検索します (一覧には表示されませんが、フル ネームを検索すると見つかります)。
1. ロールを保存します。

マウントで資格情報を使用するまで、5 分から 10 分お待ちください

### <a name="set-environment-variable-for-oauth-credentials"></a>OAuth 資格情報の環境変数を設定する

ビッグ データ クラスターにアクセスできるクライアント マシンでコマンド プロンプトを開きます。 次の形式を使用して環境変数を設定します。資格情報はコンマ区切りの一覧にする必要があります。 Windows では 'set' コマンドが使用されます。 Linux を使用している場合は、代わりに 'export' を使用してください。

資格情報を指定するときは、コンマ "," の間の改行または空白文字を削除する必要があることに**注意してください**。 以下の書式設定は、読みやすくするためのものです。

   ```text
    set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
    fs.azure.account.oauth2.client.endpoint=[token endpoint],
    fs.azure.account.oauth2.client.id=[Application client ID],
    fs.azure.account.oauth2.client.secret=[client secret]
   ```

## <a name="use-access-keys-to-mount"></a>アクセス キーを使用してマウントする

Azure portal で ADLS アカウント用に取得できるアクセス キーを使用してマウントすることもできます。

 > [!TIP]
   > ストレージ アカウントのアクセス キー (`<storage-account-access-key>`) を検索する方法の詳細については、「[アカウント キーと接続文字列を表示する](/azure/storage/common/storage-account-manage#view-account-keys-and-connection-string)」を参照してください。

### <a name="set-environment-variable-for-access-key-credentials"></a>アクセス キー資格情報の環境変数を設定する

1. ビッグ データ クラスターにアクセスできるクライアント マシンでコマンド プロンプトを開きます。

1. ビッグ データ クラスターにアクセスできるクライアント マシンでコマンド プロンプトを開きます。 次の形式を使用して環境変数を設定します。 資格情報はコンマ区切りの一覧にする必要があります。 Windows では 'set' コマンドが使用されます。 Linux を使用している場合は、代わりに 'export' を使用してください。

資格情報を指定するときは、コンマ "," の間の改行または空白文字を削除する必要があることに**注意してください**。 以下の書式設定は、読みやすくするためのものです。

   ```text
   set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a> リモート HDFS ストレージをマウントする

アクセス キーまたは OAuth を使用するための MOUNT_CREDENTIALS 環境変数を設定したので、マウントを開始することができます。 次の手順では、Azure Data Lake のリモート HDFS ストレージを、ビッグ データ クラスターのローカル HDFS ストレージにマウントします。

1. **kubectl** を使用して、ビッグ データ クラスター内のエンドポイント **controller-svc-external** サービスの IP アドレスを検索します。 **External-IP** を検索します。

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. クラスターのユーザー名とパスワードによるコントローラー エンドポイントの外部 IP アドレスを使用して **azdata** でログインします。

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080
   ```
1. 環境変数 MOUNT_CREDENTIALS を設定する (手順については上へスクロール)

1. **azdata bdc hdfs mount create** を使用して、Azure でリモート HDFS ストレージをマウントします。 次のコマンドを実行する前に、プレースホルダーの値を置き換えます。

   ```bash
   azdata bdc hdfs mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
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

次の例では、マウントを更新しています。 この更新により、マウント キャッシュもクリアされます。

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
