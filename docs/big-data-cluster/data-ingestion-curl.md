---
title: Curl を使用して、SQL Server 2019 ビッグ データ クラスターで HDFS にデータを読み込む |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 1a7c7691ec20f459f39a39270e9a78fc9d8ad96f
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017548"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-2019-big-data-clusters"></a>Curl を使用して、SQL Server 2019 ビッグ データ クラスターで HDFS にデータを読み込む

この記事は、使用する方法を説明します**curl** SQL Server 2019 ビッグ データ クラスター (プレビュー) で、HDFS にデータを読み込めません。

## <a name="obtain-the-service-external-ip"></a>サービスの外部 ip アドレスを取得します。

配置が完了したらとそのアクセスを通過 Knox、WebHDFS が開始されます。 呼ばれる Kubernetes サービスを介して Knox エンドポイントが公開される**エンドポイント セキュリティ**します。  ファイルのアップロード/ダウンロードするために必要な WebHDFS URL を作成する必要があります、**エンドポイント セキュリティ**サービスの外部 IP アドレスとクラスターの名前。 取得することができます、**エンドポイント セキュリティ**次のコマンドを実行して外部 IP アドレスをサービスします。

```bash
kubectl get service endpoint-security -n <cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> `<cluster name>`を実行したときに指定したクラスターの名前を次に示します`mssqlctl cluster create --name <cluster name>`します。

## <a name="construct-the-url-to-access-webhdfs"></a>WebHDFS へのアクセスに URL を構築します。

ここで、次のように、WebHDFS へのアクセスに URL を構築できます。

`https://<endpoint-security service external IP address>:30443/gateway/default/webhdfs/v1/`

以下に例を示します。

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>ファイルを一覧表示します。

一覧のファイルに**hdfs:///airlinedata**、次の curl コマンドを使用します。

```bash
curl -i -k -u root:root-password -X GET 'https://<endpoint-security IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>ローカル ファイルを HDFS に入れる

新しいファイルを配置する**test.csv** airlinedata ディレクトリにローカル ディレクトリから次の curl コマンドを使用して、(、 **Content-type**パラメーターが必要です)。

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<endpoint-security IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>ディレクトリを作成します。

ディレクトリを作成する**テスト** `hdfs:///`、次のコマンドを使用します。

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<endpoint-security IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>次のステップ

SQL Server のビッグ データ クラスターの詳細については、次を参照してください。[ビッグ データの SQL Server クラスターとは何ですか?](big-data-cluster-overview.md)します。
