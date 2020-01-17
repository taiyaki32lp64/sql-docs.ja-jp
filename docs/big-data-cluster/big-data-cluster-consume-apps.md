---
title: アプリケーションの使用
titleSuffix: SQL Server Big Data Clusters
description: RESTful Web サービスを使用して SQL Server ビッグ データ クラスターに展開されたアプリケーションを使用します。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 32b3884b48e20b73da186f8c0d80e6c85516a8ed
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73707181"
---
# <a name="consume-an-app-deployed-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-using-a-restful-web-service"></a>RESTful Web サービスを使用して [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]に展開されたアプリを使用する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、RESTful Web サービスを使用して SQL Server ビッグ データ クラスターに展開されたアプリを使用する方法について説明します。

## <a name="prerequisites"></a>Prerequisites

- [SQL Server ビッグ データ クラスター](deployment-guidance.md)
- [azdata コマンドライン ユーティリティ](deploy-install-azdata.md)
- [azdata](big-data-cluster-create-apps.md) または [App Deploy](app-deployment-extension.md) 拡張機能を使用して展開されたアプリ

## <a name="capabilities"></a>Capabilities

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]にアプリケーションを展開した後は、RESTful Web サービスを使用してそのアプリケーションにアクセスして使用することができます。 これにより、そのアプリを他のアプリケーションやサービス (モバイル アプリや Web サイトなど) と統合できるようになります。 次の表では、**azdata** と共に使用して、アプリの RESTful Web サービスに関する情報を取得できるアプリケーションの展開コマンドについて説明します。

|コマンド |[説明] |
|:---|:---|
|`azdata app describe` | アプリケーションについて記述します。 |

次の例のように、`--help` パラメーターを使用してヘルプを取得できます。

```bash
azdata app describe --help
```

以下のセクションでは、アプリケーションのエンドポイントを取得する方法と、アプリケーション統合のために RESTful Web サービスを使用する方法について説明します。

## <a name="retrieve-the-endpoint"></a>エンドポイントを取得する

**azdata app describe** コマンドでは、クラスター内のエンド ポイントを含め、アプリに関する詳細情報が提供されます。 通常、これは、アプリ開発者が swagger クライアントを使用してアプリを構築するときや、Web サービスを使用して RESTful 方式でアプリと対話するときに使用されます。

次の例のようなコマンドを実行して、アプリについて記述します。

```bash
azdata app describe --name add-app --version v1
```

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30080/app/addpy/v1",
    "swagger": "https://10.1.1.3:30080/app/addpy/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

出力の IP アドレス (この例では `10.1.1.3`) とポート番号 (`30080`) に注意してください。

この情報を取得する他の方法の 1 つとして、Azure Data Studio でサーバー上の [管理] を右クリックする方法があります。ここで、一覧表示されているサービスのエンドポイントを確認できます。

![ADS エンドポイント](media/big-data-cluster-consume-apps/ads_end_point.png)

## <a name="generate-a-jwt-access-token"></a>JWT アクセス トークンを生成する

展開したアプリの RESTful Web サービスにアクセスするには、まず JWT アクセス トークンを生成する必要があります。 ブラウザーで、上の `https://[IP]:[PORT]/docs/swagger.json` コマンドを実行して取得した IP アドレスとポートを使用して、URL `describe` を開きます。 `azdata login` に使用したものと同じ資格情報を使用してサインインする必要があります。

`swagger.json` の内容を [Swagger エディター](https://editor.swagger.io)に貼り付けて、使用できるメソッドを確認します。

![API Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

`app` GET メソッド と `token` POST メソッドに注意してください。 アプリの認証には JWT トークンが使用されるため、`token` メソッドへの POST 呼び出しを行うには、任意のツールを使用してトークンを取得する必要があります。 [Postman](https://www.getpostman.com/) でこれを行う方法の例を次に示します。

![Postman トークン](media/big-data-cluster-consume-apps/postman_token.png)

この要求の結果から、JWT `access_token` を取得できます。この場合、アプリを実行するために URL を呼び出す必要があります。

## <a name="execute-the-app-using-the-restful-web-service"></a>RESTful Web サービスを使用してアプリを実行する

> [!NOTE]
> 必要に応じて、ブラウザーで `azdata app describe --name [appname] --version [version]` を実行したときに返された `swagger` の URL を開くことができます。これは、`https://[IP]:[PORT]/app/[appname]/[version]/swagger.json` のようになります。 `azdata login` に使用したものと同じ資格情報を使用してログインする必要があります。 `swagger.json` の内容を [Swagger エディター](https://editor.swagger.io)に貼り付けることができます。 Web サービスで `run` メソッドが公開されていることがわかります。 また、上部に表示されているベース URL にも注意してください。

任意のツールを使用して `run` メソッド (`https://[IP]:30778/api/app/[appname]/[version]/run`) を呼び出し、json として POST 要求の本文でパラメーターを渡すことができます。 この例では、[Postman](https://www.getpostman.com/) を使用します。 呼び出しを行う前に、`Authorization` を `Bearer Token` に設定し、前の手順で取得したトークンを貼り付ける必要があります。 これにより、要求にヘッダーが設定されます。 次のスクリーンショットを見てください。

![Postman の実行ヘッダー](media/big-data-cluster-consume-apps/postman_run_1.png)

次に、要求本文で、呼び出しているアプリにパラメーターを渡し、`content-type` を `application/json` に設定します。

![Postman の実行本文](media/big-data-cluster-consume-apps/postman_run_2.png)

要求を送信すると、`azdata app run` を介してアプリを実行したときと同じ出力が得られます。

![Postman の実行結果](media/big-data-cluster-consume-apps/postman_result.png)

これで、Web サービスを介してアプリが正常に呼び出されるようになりました。 同様の手順に従って、この Web サービスをアプリケーションに統合することができます。

## <a name="next-steps"></a>次の手順

その他のサンプルにはついては、[アプリの展開サンプル](https://aka.ms/sql-app-deploy)に関するページを参照してください。

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の概要](big-data-cluster-overview.md)」を参照してください。
