---
title: HTTP 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.httpconnection.server.f1
- sql13.dts.designer.httpconnection.proxy.f1
helpviewer_keywords:
- HTTP connection manager
- Web site connections [Integration Services]
- connection managers [Integration Services], HTTP
- Web server connections [Integration Services]
- connections [Integration Services], HTTP
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 106b0d08ec24143ba497fb5b631fcbd5003a4872
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294407"
---
# <a name="http-connection-manager"></a>HTTP 接続マネージャー

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  HTTP 接続により、パッケージが HTTP を使用してファイルを送受信することで、Web サーバーにアクセスできるようになります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に含まれる Web サービス タスクには、この接続マネージャーを使用します。  
  
 HTTP 接続マネージャーをパッケージに追加するときは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によって、実行時に HTTP 接続を解決する接続マネージャーを作成し、接続マネージャーのプロパティを設定して、接続マネージャーをパッケージの **Connections** コレクションに追加します。  
  
 接続マネージャーの **ConnectionManagerType** プロパティは、 **HTTP**に設定されます。  
  
 HTTP 接続マネージャーは、次の方法で構成できます。  
  
-   資格情報を使用します。 接続マネージャーが資格情報を使用する場合、プロパティにユーザー名、パスワード、およびドメインが含まれます。  
  
    > [!IMPORTANT]  
    >  HTTP 接続マネージャーでは、匿名認証と基本認証のみがサポートされています。 Windows 認証はサポートされていません。  
  
-   クライアント証明書を使用します。 接続マネージャーがクライアント証明書を使用する場合、プロパティに証明書名が含まれます。  
  
-   サーバーへの接続のタイムアウトと、データを書き込むチャンク サイズを指定します。  
  
-   プロキシ サーバーを使用します。 プロキシ サーバーは、資格情報を使用するように構成することや、プロキシ サーバーをバイパスして、代わりにローカル アドレスを使用するように構成することもできます。  
  
## <a name="configuration-of-the-http-connection-manager"></a>HTTP 接続マネージャーの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 プログラムによる接続マネージャーの構成の詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>」を参照してください。  
  
## <a name="http-connection-manager-editor-server-page"></a>[HTTP 接続マネージャー エディター] ([サーバー] ページ)
  **[HTTP 接続マネージャー エディター]** ダイアログ ボックスの **[サーバー]** タブを使用すると、URL やセキュリティ資格情報などのプロパティを指定して、HTTP 接続マネージャーを構成できます。 HTTP 接続により、パッケージが HTTP を使用してファイルを送受信することで、Web サーバーにアクセスできるようになります。 HTTP 接続マネージャーを構成した後に接続をテストすることもできます。  
  
> [!IMPORTANT]  
>  HTTP 接続マネージャーでは、匿名認証と基本認証のみがサポートされています。 Windows 認証はサポートされていません。  
  
 HTTP 接続マネージャーの詳細については、「 [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md)」を参照してください。 HTTP 接続マネージャーの一般的な使用シナリオの詳細については、「 [Web Service Task](../../integration-services/control-flow/web-service-task.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **[サーバー URL]**  
 サーバーの URL を入力します。  
  
 **[Web サービス タスク エディター]** の **[全般]** ページにある **[WSDL のダウンロード]** ボタンを使用する場合は、WSDL ファイルの URL を入力します。 この URL は "?wsdl" で終わります。  
  
 **[資格情報を使用する]**  
 HTTP 接続マネージャーで、認証のためにユーザーのセキュリティ資格情報を使用するかどうかを指定します。  
  
 **User name**  
 HTTP 接続マネージャーで資格情報を使用する場合は、ユーザー名、パスワード、およびドメインを指定する必要があります。  
  
 **パスワード**  
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
  
## <a name="http-connection-manager-editor-proxy-page"></a>[HTTP 接続マネージャー エディター] ([プロキシ] ページ)
  **[HTTP 接続マネージャー エディター]** の **[プロキシ]** タブを使用すると、HTTP 接続マネージャーがプロキシ サーバーを使用するように設定できます。 HTTP 接続により、パッケージが HTTP を使用してファイルを送受信することで、Web サーバーにアクセスできるようになります。  
  
 HTTP 接続マネージャーの詳細については、「 [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md)」を参照してください。 HTTP 接続マネージャーの一般的な使用シナリオの詳細については、「 [Web Service Task](../../integration-services/control-flow/web-service-task.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **[プロキシを使用する]**  
 HTTP 接続マネージャーでプロキシ サーバーを使用して接続するかどうかを指定します。  
  
 **[プロキシ URL]**  
 プロキシ サーバーの URL を入力します。  
  
 **[ローカルではプロキシを使用しない]**  
 HTTP 接続マネージャーで、ローカル アドレスの場合はプロキシ サーバーを使用しないかどうかを指定します。  
  
 **[資格情報を使用する]**  
 HTTP 接続マネージャーで、プロキシ サーバーに対してセキュリティ資格情報を使用するかどうかを指定します。  
  
 **User name**  
 HTTP 接続マネージャーで資格情報を使用する場合は、ユーザー名、パスワード、およびドメインを指定する必要があります。  
  
 **パスワード**  
 HTTP 接続マネージャーで資格情報を使用する場合は、ユーザー名、パスワード、およびドメインを指定する必要があります。  
  
 **[ドメイン]**  
 HTTP 接続マネージャーで資格情報を使用する場合は、ユーザー名、パスワード、およびドメインを指定する必要があります。  
  
 **[プロキシ バイパス一覧]**  
 プロキシ サーバーを使用しないアドレスの一覧です。  
  
 **[追加]**  
 プロキシ サーバーを使用しないアドレスを入力します。  
  
 **[削除]**  
 アドレスを選択した後、 **[削除]** をクリックするとアドレスが削除されます。  
  
## <a name="see-also"></a>参照  
 [Web サービス タスク](../../integration-services/control-flow/web-service-task.md)   
 [Integration Services &#40;SSIS&#41; の接続](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
