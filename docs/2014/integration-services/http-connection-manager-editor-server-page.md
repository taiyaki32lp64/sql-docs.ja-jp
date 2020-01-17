---
title: HTTP 接続マネージャー エディター (サーバー ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.httpconnection.server.f1
helpviewer_keywords:
- HTTP Connection Manager Editor
ms.assetid: 774778a0-ece6-4971-b93f-b121d8fc1fc1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 197a2668beb60acf2473a1f53786d7b553e08cf6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058250"
---
# <a name="http-connection-manager-editor-server-page"></a>[HTTP 接続マネージャー エディター] ([サーバー] ページ)
  **[HTTP 接続マネージャー エディター]** ダイアログ ボックスの **[サーバー]** タブを使用すると、URL やセキュリティ資格情報などのプロパティを指定して、HTTP 接続マネージャーを構成できます。 HTTP 接続により、パッケージが HTTP を使用してファイルを送受信することで、Web サーバーにアクセスできるようになります。 HTTP 接続マネージャーを構成した後に接続をテストすることもできます。  
  
> [!IMPORTANT]  
>  HTTP 接続マネージャーでは、匿名認証と基本認証のみがサポートされています。 Windows 認証はサポートされていません。  
  
 HTTP 接続マネージャーの詳細については、「 [HTTP Connection Manager](connection-manager/http-connection-manager.md)」を参照してください。 HTTP 接続マネージャーの一般的な使用シナリオの詳細については、「 [Web Service Task](control-flow/web-service-task.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[サーバー URL]**  
 サーバーの URL を入力します。  
  
 **[Web サービス タスク エディター]** の **[全般]** ページにある **[WSDL のダウンロード]** ボタンを使用する場合は、WSDL ファイルの URL を入力します。 この URL は "?wsdl" で終わります。  
  
 **[資格情報を使用する]**  
 HTTP 接続マネージャーで、認証のためにユーザーのセキュリティ資格情報を使用するかどうかを指定します。  
  
 **ユーザー名**  
 HTTP 接続マネージャーで資格情報を使用する場合は、ユーザー名、パスワード、およびドメインを指定する必要があります。  
  
 **Password**  
 HTTP 接続マネージャーで資格情報を使用する場合は、ユーザー名、パスワード、およびドメインを指定する必要があります。  
  
 **[ドメイン]**  
 HTTP 接続マネージャーで資格情報を使用する場合は、ユーザー名、パスワード、およびドメインを指定する必要があります。  
  
 **[クライアント証明書を使用する]**  
 HTTP 接続マネージャーで、認証のためにクライアント証明書を使用するかどうかを指定します。  
  
 **Certificate**  
 **[証明書の選択]** ダイアログ ボックスを使用して、一覧から証明書を選択します。 テキスト ボックスに、この証明書に関連付けられている名前が表示されます。  
  
 **[タイムアウト (秒)]**  
 Web サーバーへの接続のタイムアウトを指定します。 このプロパティの既定値は 30 秒です。  
  
 **[チャンク サイズ (KB)]**  
 データを書き込むためのチャンクのサイズを指定します。  
  
 **[接続テスト]**  
 HTTP 接続マネージャーを構成した後に、 **[接続テスト]** をクリックして、接続が利用可能であることを確認します。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [[HTTP 接続マネージャー エディター] ([プロキシ] ページ)](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)  
  
  
