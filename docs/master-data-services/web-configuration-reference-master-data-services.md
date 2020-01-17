---
title: Web 設定リファレンス
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e9d3cd20fc219a7159de0b271dafcc0e9fb2c3ba
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728834"
---
# <a name="web-configuration-reference-master-data-services"></a>Web 設定リファレンス (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] では Web.config ファイルを使用することで、インターネット インフォメーション サービス (IIS) を有効にして [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションおよび Web サービスをホストできるようにする構成設定を取り込みます。 この Web.config ファイルは、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] インストール パスの WebApplication フォルダーにあります。 パスと権限の詳細については、「[フォルダーとファイルの権限 (マスター データ サービス)](../master-data-services/folder-and-file-permissions-master-data-services.md)」を参照してください。  
  
## <a name="webconfig-elements"></a>Web.Config 要素  
 Web.config ファイルには、標準 IIS、.NET Framework、ASP.NET、および Windows Communication Foundation (WCF) の構成の要素以外に、カスタム [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 要素 **\<masterDataServices>** が含まれています。 次の表では、Web.config ファイルに含まれている要素について説明します。  
  
|Configuration 要素|説明|  
|---------------------------|-----------------|  
|**masterDataServices**|Custom 要素。 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web サービスを [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースに接続します。|  
|**connectionStrings**|ASP.NET 要素。 詳細については、MSDN ライブラリの「 [connectionStrings 要素 (ASP.NET 設定スキーマ)](https://go.microsoft.com/fwlink/?LinkId=178347) 」を参照してください。|  
|**system.web**|ASP.NET 要素。 詳細については、MSDN ライブラリの「 [system.web 要素 (ASP.NET 設定スキーマ)](https://go.microsoft.com/fwlink/?LinkId=178348) 」を参照してください。|  
|**startup**|.NET Framework 要素。 詳細については、MSDN ライブラリの「[\<startup> 要素](https://go.microsoft.com/fwlink/?LinkId=178349)」を参照してください。|  
|**runtime**|.NET Framework 要素。 詳細については、MSDN ライブラリの「[\<runtime> 要素](https://go.microsoft.com/fwlink/?LinkId=178350)」を参照してください。|  
|**system.codedom**|.NET Framework 要素。 詳細については、MSDN ライブラリの「[\<system.codedom> 要素](https://go.microsoft.com/fwlink/?LinkId=178351)」を参照してください。|  
|**system.web.extensions**|ASP.NET 要素。 詳細については、MSDN ライブラリの「 [system.web.extensions 要素 (ASP.NET 設定スキーマ)](https://go.microsoft.com/fwlink/?LinkId=178352) 」を参照してください。|  
|**system.webServer**|IIS 要素を含んだセクション グループ。 詳細については、MSDN ライブラリの「[system.webServer セクション グループ \[IIS 7 設定スキーマ\]](https://go.microsoft.com/fwlink/?LinkId=178353)」を参照してください。|  
|**system.serviceModel**|WCF 要素。 詳細については、MSDN ライブラリの「[\<system.serviceModel>](https://go.microsoft.com/fwlink/?LinkId=178354)」を参照してください。|  
|**system.diagnostics**|.NET Framework 要素。 詳細については、MSDN ライブラリの「[\<system.diagnostics> 要素](https://go.microsoft.com/fwlink/?LinkId=178355)」を参照してください。|  
|**appSettings**|ASP.NET 要素。 詳細については、MSDN ライブラリの「 [appSettings 要素 (全般設定スキーマ)](https://go.microsoft.com/fwlink/?LinkId=178356) 」を参照してください。|  
  
## <a name="masterdataservices-element"></a>masterDataServices 要素  
 **\<masterDataServices>** 要素は、[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web サービスを [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースに接続するのに使用するカスタム要素です。  
  
### <a name="syntax"></a>構文  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>要素と属性  
  
|アイテム|説明|  
|----------|-----------------|  
|**インスタンス (instance)**|子要素。 Web サービスとデータベース接続文字列の情報を指定する属性を含みます。|  
|**virtualPath**|Attribute。 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションとサービスの仮想パスを指定します。 これは、IIS ApplicationHost.config ファイルのsite> **要素にある \<** application> **要素の \<path** 属性に対応します。|  
|**SiteName**|Attribute。 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションとサービスをホストするサイトの名前を指定します。 これは、IIS ApplicationHost.config ファイルのsites> **にある \<** site> **要素の \<name** 属性に対応します。|  
|**connectionName**|Attribute。 使用する接続の名前を指定します。 これは、Web.config のconnectionStrings> **要素にある \<** add> **要素の \<name** 属性に対応します。|  
|**serviceName**|Attribute。 Web サービスの名前を指定します。 これは、Web.config のservices> **要素にある \<** service> **要素の \<name** 属性に対応します。|  
  
### <a name="example"></a>例  
 次の例は、Contoso サイト上の MDS1 という名前のサービスと、MDSDB によって指定された接続文字列を使用した /MDS パスを示しています。  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
