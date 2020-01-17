---
title: SQL Server | のクラウドアダプターMicrosoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Cloud adapter
- Deploy to Azure
ms.assetid: 82ed0d0f-952d-4d49-aa36-3855a3ca9877
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bf57adb31330f5b0c0f18fbcccd4d71f47d3c933
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176019"
---
# <a name="cloud-adapter-for-sql-server"></a>SQL Server のクラウド アダプター
  クラウドアダプターサービスは、Azure VM での[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]プロビジョニングの一部として作成されます。 クラウド アダプター サービスは、最初の実行時に自己署名 SSL 証明書を生成し、 **Local System** アカウントとして実行されます。 その際に、自身を構成するために使用される構成ファイルを生成します。 クラウド アダプターは、Windows ファイアウォール ルールを作成し、既定のポート 11435 で着信する TCP 接続を許可します。  
  
 クラウド アダプターは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の内部設置型インスタンスからメッセージを受信するステートレスな同期サービスです。 クラウド アダプター サービスが停止すると、リモート アクセス クラウド アダプターが停止され、SSL 証明書のバインドが解除され、Windows ファイアウォールのルールが無効になります。  
  
## <a name="cloud-adapter-requirements"></a>クラウド アダプターの要件  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に対してクラウド アダプターをインストールして有効にし、実行するには、次の要件が必要です。  
  
-   クラウド アダプターは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012 以降でサポートされます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012 では、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のクラウド アダプターは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012 に対応する SQL 管理オブジェクトを必要とします。  
  
-   クラウド アダプター Web サービスは **ローカル システム** アカウントとして実行され、タスクを実行する前にクライアントの資格情報を確認します。 クライアントによって指定された資格情報は、リモートコンピューターのローカル**管理者**グループのメンバーである使用アカウントに属している必要があります。  
  
-   クラウド アダプターでは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証のみがサポートされます。  
  
-   クラウド アダプターは、ローカル コンピューター上のコマンドを実行するために sa アカウントではなく仮想マシンのローカル管理者アカウントを使用します。  
  
-   クラウド アダプターは TCP/IP をリッスンします。 既定のポートは 11435 です。  
  
-   クラウド アダプターは Windows ファイアウォール ルールを作成および変更する権限を必要とします。  
  
## <a name="cloud-adapter-configuration-settings"></a>クラウド アダプター構成の設定  
 クラウド アダプターの設定を変更するには、クラウド アダプターの構成の詳細を使用します。  
  
-   **構成ファイルの既定のパス**-C:\PROGRAM "SQL \" \ "  
  
-   **構成ファイルのパラメーター** -  
  
    -   \<configuration>  
  
        -   \<appSettings >  
  
            -   \<add key = "WebServicePort" value = ""/>  
  
            -   \<add key = "WebServiceCertificate" value = "GUID"/>  
  
            -   \<add key="ExposeExceptionDetails" value="true" />  
  
        -   \</appSettings >  
  
    -   \</構成 >  
  
-   **証明書の詳細**-証明書の値は次のとおりです。  
  
    -   Subject-"CN = cloudadapter\<VMName >, dc = SQL Server, dc = Microsoft"  
  
    -   証明書ではサーバー認証 EKU のみを有効にします。  
  
    -   証明書キーの長さは 2,048 です。  
  
 **構成ファイルの値**:  
  
|設定|値|既定|コメント|  
|-------------|------------|-------------|--------------|  
|WebServicePort|1-65535|11435|指定しない場合、11435 が使用されます。|  
|WebServiceCertificate|Thumbprint|Empty|空の場合、新しい自己署名証明書が生成されます。|  
|ExposeExceptionDetails|True/False|False||  
  
## <a name="cloud-adapter-troubleshooting"></a>クラウド アダプターのトラブルシューティング  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のクラウド アダプターのトラブルシューティングを行うには、次の情報を使用します。  
  
-   **エラー処理とログ記録**-エラーと状態メッセージがアプリケーションイベントログに書き込まれます。  
  
-   **トレース、イベント**: すべてのイベントがアプリケーションイベントログに書き込まれます。  
  
-   **コントロール、構成**: 次の場所にある構成ファイルを使用します。C:\Program ・ SQL server \ 120 \ ツール (\\cloudadapter)  
  
|Error|エラー ID|原因|解決方法|  
|-----------|--------------|-----------|----------------|  
|証明書ストアに証明書を追加中に例外が発生しました。 {例外テキスト}。|45560|コンピューター証明書ストアのアクセス許可|クラウドアダプターサービスに、コンピューター証明書ストアに証明書を追加するためのアクセス許可があることを確認します。|  
|ポート {ポート番号} と証明書 {サムプリント} の SSL バインドを構成しようとして例外が発生しました。 {例外}。|45561|他のアプリケーションが既にポートを使用しているか、証明書をバインドされています。|既存のバインドを削除するか、または構成ファイルのクラウド アダプターのポートを変更します。|  
|証明書ストアで SSL 証明書 [{サムプリント}] が見つかりませんでした。|45564|証明書のサムプリントが構成ファイルにありますが、そのサービスのための個人証明書ストアに証明書が含まれていません。<br /><br /> 権限が不足しています。|サービスの個人証明書ストアに証明書を置きます。<br /><br /> サービスに、ストアへの適切な権限があることを確認します。|  
|Web サービスを開始できませんでした。 {例外テキスト}。|45570|例外で説明されています。|ExposeExceptionDetails を有効にし、例外の拡張情報を使用します。|  
|証明書 [{サムプリント}] の有効期限が切れています。|45565|構成ファイルから参照される期限切れの証明書。|有効な証明書を追加し、サムプリントを使用して構成ファイルを更新します。|  
|Web サービスエラー: {0}。|45571|例外で説明されています。|ExposeExceptionDetails を有効にし、例外の拡張情報を使用します。|  
  
## <a name="see-also"></a>関連項目  
 [Microsoft Azure Virtual Machine への SQL Server データベースの配置](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md)  
  
  
