---
title: 開発者向けドキュメント
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 067b1f69-84eb-4a13-b220-120cd63704b4
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 415e20eb08041780b8d20fb124151cc700cacbe6
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728259"
---
# <a name="master-data-services-developer-documentation"></a>マスター データ サービスの開発者向けドキュメント

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  ここでは、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] の操作方法を、コードの記述によってカスタマイズする方法について説明します。 具体的には、次の方法を学習します。  
  
-   [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web サービスにアクセスするプログラムを記述する。 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web サービスは、開発者がコードを通じて [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 機能を制御するために使用する、Windows Communication Foundation (WCF) サービスです。  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 機能を既存のアプリケーション内に組み込む。  
  
-   [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] UI を使用した場合では難しい、反復的なアクションや複雑なアクションを実行するためのコードを記述する。  
  
-   指定したビジネス ルールに応答して実行されるカスタム ワークフローを作成する。 カスタム ワークフローでは、開発者が記述したコードを呼び出すことで、ワークフローの処理に必要な任意のアクションを実行できます。  
  
## <a name="master-data-manager-web-service"></a>マスター データ マネージャー Web サービス  
 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web サービスを使用すると、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web サイトにアクセスできる任意のコンピューターから、[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] の機能をプログラム経由で使用できます。 Web サービスにアクセスするコードの記述を開始する前に、指定した名前空間に含まれるプロキシ クラスを生成する必要があります。 このドキュメントでは、<xref:Microsoft.MasterDataServices> をプロキシ名前空間として使用します。 Web サービス操作の実行に使用する主要なプロキシ クラスは、<xref:Microsoft.MasterDataServices.ServiceClient> クラスです。このクラスは、<xref:Microsoft.MasterDataServices.IService> インターフェイスを実装します。 コードから <xref:Microsoft.MasterDataServices.ServiceClient> クラスのメソッドを呼び出して、[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web サービスにアクセスできます。 この名前空間の残りのクラスは、Web サービス操作で使用されます。  
  
### <a name="web-service-content"></a>Web サービスに関するコンテンツ  
 [マスター データ マネージャー Web サービス プロキシ クラスの作成](../../master-data-services/develop/create-master-data-manager-web-service-proxy-classes.md)  
 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web サイトからのメタデータ パブリッシュを有効にする方法と、Web サービス操作にプログラム経由でアクセスするために使用できるプロキシ クラスの作成方法について説明します。  
  
 [Web サービス操作の分類 &#40;マスター データ サービス&#41;](../../master-data-services/develop/categorized-web-service-operations-master-data-services.md)  
 <xref:Microsoft.MasterDataServices.ServiceClient> クラスの Web サービス操作のカテゴリ別一覧です。  
  
## <a name="custom-workflows"></a>カスタム ワークフロー  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] は、ビジネス ルールを使用して基本的なワークフロー ソリューションを作成します。 開発者は、指定した条件に基づいてデータを自動的に更新および検証したり、電子メール通知を送信することができます。 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 内のビジネス ルールは、最も一般的なワークフロー シナリオを管理するためのものです。 複数階層の承認や複雑な意思決定ツリーなど、より高度な複合イベント処理を必要とするワークフローの場合は、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] を構成することで、作成したカスタム アセンブリにデータを送ることができます。 カスタム ワークフローを操作するには、Web アプリケーション コンピューター上で SQL Server MDS Workflow Integration Service を構成および開始し、<xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender> インスタンスを実装するアセンブリを作成する必要があります。  
  
### <a name="custom-workflow-content"></a>カスタム ワークフローに関するコンテンツ  
 [カスタム ワークフローの作成 &#40;マスター データ サービス&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)  
 ワークフロー ハンドラー アセンブリを作成する方法、SQL Server MDS Workflow Integration Service を構成および開始する方法、カスタム ワークフローを開始するビジネス ルールを [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 内に作成する方法について説明します。  
  
## <a name="web-server-namespaces"></a>Web サーバー名前空間  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] は、一連のアセンブリを Web サーバー コンピューターにインストールします。 これらのアセンブリには、Web サーバー コンピューターの動作をカスタマイズする高度なシナリオに使用できる名前空間が含まれます。 次の表では、これらの名前空間について説明します。  
  
|名前空間|説明|  
|---------------|-----------------|  
|<xref:Microsoft.MasterDataServices.Deployment>|モデルからの配置パッケージの作成と [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースへのパッケージの配置に使用できるクラスが含まれます。|  
|<xref:Microsoft.MasterDataServices.Services>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションを通じて Web サーバー コンピューターに対して行われた Web サービス操作を取得および処理するクラスが含まれます。|  
|<xref:Microsoft.MasterDataServices.Services.DataContracts>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションを通じてクライアント コンピューターから Web サーバー コンピューターにデータを渡す方法を定義するクラスが含まれます。|  
|<xref:Microsoft.MasterDataServices.Services.MessageContracts>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションを通じてクライアント コンピューターから Web サーバー コンピューターに要求と応答を渡す方法を定義するクラスが含まれます。|  
|<xref:Microsoft.MasterDataServices.Services.ServiceContracts>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web サービスを通じて呼び出すことのできる操作を定義するインターフェイスが含まれます。|  
  
  
