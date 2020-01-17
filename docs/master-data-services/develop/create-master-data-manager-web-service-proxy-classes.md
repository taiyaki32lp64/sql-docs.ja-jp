---
title: マスター データ マネージャー Web サービス プロキシ クラスの作成
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 8bdab026-a0c0-41f3-9d36-f3919c23247f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1096da19a45e15ab2216cea2f4a4a38ecb05233e
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729321"
---
# <a name="create-master-data-manager-web-service-proxy-classes"></a>マスター データ マネージャー Web サービス プロキシ クラスの作成

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web サービスを使用すると、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web サイトにアクセスできる任意のコンピューターから、[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] の機能をプログラム経由で使用できます。 Web サービスにアクセスするコードの記述を開始する前に、プロキシ クラスを生成する必要があります。 Web サービス操作の実行に使用する主要なプロキシ クラスは、<xref:Microsoft.MasterDataServices.ServiceClient> クラスです。このクラスは、<xref:Microsoft.MasterDataServices.IService> インターフェイスを実装します。  
  
## <a name="enable-web-service-metadata-publishing"></a>Web サービス メタデータ パブリッシュの有効化  
 プロキシ クラスを生成する前に、Web サービス メタデータ パブリッシュを有効にする必要があります。 これを行うには、次の手順を実行します。  
  
1.  テキスト エディターで [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web.config ファイルを開きます。 このファイルは、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] インストール パスの WebApplication フォルダーにあります。  
  
2.  serviceBehaviors> **の下で \<mdsWsHttpBehavior** セクションを見つけます。 **\<serviceMetadata>** 要素の場合、**httpGetEnabled** を **true** に設定します。  
  
    > [!NOTE]  
    >  Web サービスを SSL (Secure Sockets Layer) を介して有効にするには、web.config ファイルの **mdsWsHttpBehavior** セクションで、**httpsGetEnabled** を **true** に設定します。 さらに、SSL 用に構成されるように **mdsWsHTTPBinding** を変更し、非 SSL セクションをコメント アウトする必要もあります。  
  
3.  変更をファイルに保存します。  
  
4.  サービス URL (たとえば、`https://yourserver/MDS/service/service.svc`) を参照して、メタデータのパブリッシュをテストします。 メタデータ パブリッシュが有効化されると、   
    "サービスを作成しました。" で始まるページが表示されます。  
  
## <a name="creating-proxy-classes-by-using-visual-studio"></a>Visual Studio を使用してプロキシ クラスを作成する  
 Visual Studio 2010 がインストールされている場合、プロキシ クラスを生成する最もシンプルな方法は、プロジェクトに**サービス参照**を追加することです。 サービス参照のアドレスは、[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションの URL に、/service/service.svc を付加したものです。 たとえば、 `https://yourserver/MDS/service/service.svc`のようにします。 詳細については、「[方法: サービス参照を追加、更新、または削除する](https://go.microsoft.com/fwlink/?LinkId=221167)」を参照してください。  
  
## <a name="creating-proxy-classes-by-using-svcutilexe"></a>Svcutil.exe を使用してプロキシ クラスを作成する  
 Svcutil.exe を使用するには、コンピューターに [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] または [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows SDK がインストールされている必要があります。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] を使用する場合は、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] コマンド プロンプトでコマンドを実行する必要があります。 詳細については、「[ServiceModel メタデータ ユーティリティ ツール (Svcutil.exe)](https://go.microsoft.com/fwlink/?LinkId=165027)」および「[サービス メタデータからの WCF クライアントの生成](https://go.microsoft.com/fwlink/?LinkId=164821)」を参照してください。  
  
 Svcutil.exe を使用して一連の C# プロキシ クラスを作成するには、次のようなコマンドを使用します。  
  
```  
svcutil.exe https://<server_name:port>/<virtual_path>/Service/Service.svc   
/out:<proxy_name>.cs /messageContract /tcv:Version35   
/noconfig /ct:System.Collections.ObjectModel.Collection`1   
/namespace:*,Microsoft.MasterDataServices  
```  
  
 各要素の説明は次のとおりです。  
  
-   *servername*:*port* は、[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] をホストするコンピューターのコンピューター名およびポート番号を指定します。  
  
-   *virtual_path* には、インターネット インフォメーション サービス (IIS) の [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] の仮想パスを指定します。  
  
-   *proxy_name* には、生成されるプロキシ ファイルの名前を指定します。  
  
## <a name="see-also"></a>参照  
 [Web サービス操作の分類 &#40;マスター データ サービス&#41;](../../master-data-services/develop/categorized-web-service-operations-master-data-services.md)  
  
  
