---
title: Reporting Services の REST API による開発 | Microsoft Docs
ms.description: The REST API provides programmatic access to the objects in a SQL Server 2017 Reporting Services report server catalog.
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: developer
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/12/2018
ms.openlocfilehash: ba424fa0c79249a8870962d0df4cdaf383c9aa39
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263030"
---
# <a name="develop-with-the-rest-apis-for-reporting-services"></a>Reporting Services の REST API による開発

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

Microsoft SQL Server 2017 Reporting Services では、Representational State Transfer (REST) API がサポートされます。 REST API は、一連の HTTP 操作 (メソッド) をサポートするサービス エンドポイントであり、レポート サーバー内のリソースに対する作成、取得、更新、削除アクセスを提供します。

REST API を使用すると、SQL Server 2017 Reporting Services レポート サーバー カタログ内のオブジェクトにプログラムでアクセスできます。 オブジェクトの例としては、フォルダー、レポート、KPI、データ ソース、データセット、更新計画、サブスクリプションなどがあります。 REST API を使用すると、たとえば、フォルダー階層内の移動、フォルダーの内容の検出、レポート定義のダウンロードなどを行うことができます。 また、オブジェクトの作成、更新、および削除を行うこともできます。 オブジェクトの操作の例としては、レポートのアップロード、更新計画の実行、フォルダーの削除などがあります。

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-hybrid-note.md)]

## <a name="components-of-a-rest-api-requestresponse"></a>REST API の要求/応答のコンポーネント

REST API の要求/応答ペアは、次の 5 つのコンポーネントに分けることができます。

* **要求 URI**。`{URI-scheme} :// {URI-host} / {resource-path} ? {query-string}` で構成されます。 要求 URI は要求メッセージ ヘッダーに含まれていますが、ほとんどの言語やフレームワークでは要求メッセージとは別に渡す必要があるため、ここでは独立した項目にしてあります。

    * URI スキーム: 要求の送信に使用されるプロトコルを示します。 たとえば、`http` や `https` などです。
    * URI ホスト: `myserver.contoso.com` など、REST サービス エンドポイントがホストされているサーバーのドメイン名または IP アドレスを指定します。
    * リソース パス: リソースまたはリソース コレクションを指定します。リソースの選択を決定するときにサービスによって使用される複数のセグメントを含むことができます。 たとえば、`CatalogItems(01234567-89ab-cdef-0123-456789abcdef)/Properties` を使用して、CatalogItem の指定したプロパティを取得できます。
    * クエリ文字列 (省略可能): API のバージョンやリソースの選択条件など、簡単な追加パラメーターを提供します。

* HTTP 要求メッセージ ヘッダーのフィールド:

    * 必須の [HTTP メソッド](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) (操作または動詞ともいう)。要求する操作の種類をサービスに通知します。 Reporting Services REST API では、DELETE、GET、HEAD、PUT、POST、および PATCH の各メソッドがサポートされます。
    * 省略可能な追加ヘッダー フィールド。指定された URI および HTTP メソッドで必要です。

* 省略可能な HTTP **要求メッセージ本文**のフィールド。URI および HTTP 操作をサポートするためのものです。 たとえば、POST 操作には、複合パラメーターとして渡される MIME でエンコードされたオブジェクトが含まれます。 POST または PUT 操作の場合、本文の MIME エンコードの種類を `Content-type` 要求ヘッダーでも指定する必要があります。 一部のサービスでは、`application/json` などの特定の MINE の種類を使用する必要があります。

* HTTP **応答メッセージ ヘッダー**のフィールド:

    * [HTTP 状態コード](http://www.w3.org/Protocols/HTTP/HTRESP.html)。成功コードの 2xx から、エラー コードの 4xx または 5xx までの範囲です。 または、API のドキュメントに記載されているように、サービスで定義された状態コードが返されることもあります。
    * 省略可能な追加ヘッダー フィールド。要求の応答をサポートするために必要です (`Content-type` 応答ヘッダーなど)。

* 省略可能な HTTP **応答メッセージ本文**のフィールド:

    * MIME でエンコードされた応答オブジェクトが HTTP 応答の本文で返されます (データを返す GET メソッドからの応答など)。 通常、これらのオブジェクトは、`Content-type` 応答ヘッダーで示される、JSON や XML などの構造化された形式で返されます。

## <a name="api-documentation"></a>API のドキュメント

最新の REST API には最新の API ドキュメントが必要です。 REST API は OpenAPI 仕様 (Swagger 仕様ともいう) に基づいてビルドされており、ドキュメントは [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0) で入手できます。 SwaggerHub は、API の文書化だけでなく、任意の言語 (JavaScript、TypeScript、C#、Java、Python、Ruby など) でのクライアント ライブラリの作成にも役立ちます。

## <a name="testing-api-calls"></a>API 呼び出しのテスト

HTTP 要求/応答メッセージをテストするためのツールは [Fiddler](https://www.telerik.com/fiddler) です。 Fiddler は、REST 要求をインターセプトできる無料の Web デバッグ プロキシであり、HTTP 要求/応答メッセージの診断が容易になります。

## <a name="next-steps"></a>次の手順

[SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0) で利用可能な API を確認します。

サンプルは [GitHub](https://github.com/Microsoft/Reporting-Services) で入手できます。 このサンプルには、TypeScript、React、webpack でビルドされた HTML5 アプリと、PowerShell の例が含まれます。

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
