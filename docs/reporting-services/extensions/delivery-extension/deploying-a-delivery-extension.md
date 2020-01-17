---
title: 配信拡張機能の配置 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: 4436ce48-397d-42c7-9b5d-2a267e2a1b2c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 06cffe614eaa55713fed862dc03f7c81da7bc287
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193764"
---
# <a name="deploying-a-delivery-extension"></a>配信拡張機能の配置
  配信拡張機能では、その構成情報を XML 構成ファイルの形式で指定します。 XML ファイルは、配信拡張機能に定義された XML スキーマに従います。 配信拡張機能により、構成ファイルを設定および変更するためのインフラストラクチャが提供されます。  
  
 配信拡張機能を置き換えたり、アップグレードしたりしても、配信拡張機能を参照するすべてのサブスクリプションは有効なままです。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の配信拡張機能を [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] のライブラリに書き込み、コンパイルした後、レポート サーバーがその拡張機能を検出できるように、その拡張機能を適切なディレクトリにコピーし、適切な [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の構成ファイルにエントリを追加する必要があります。  
  
## <a name="configuration-file-extension-element"></a>構成ファイルの Extension 要素  
 構成ファイルでは、レポート サーバーに配置する配信拡張機能を **Extension** 要素として入力する必要があります。 レポート サーバーの構成ファイルは、RSReportServer.config です。  
  
 次の表では、配信拡張機能の **Extension** 要素の属性について説明します。  
  
|属性|[説明]|  
|---------------|-----------------|  
|**[名前]**|拡張機能の一意な名前 (たとえば、電子メール配信拡張機能の場合は "レポート サーバーの電子メール"、ファイル共有配信拡張機能の場合は "レポート サーバーのファイル共有")。 **Name** 属性の最大文字数は 255 文字です。 名前は、構成ファイルの **Extension** 要素内にあるすべてのエントリの間で一意にする必要があります。 重複する名前がある場合には、レポート サーバーによってエラーが返されます。|  
|**型**|アセンブリの名前と共に完全修飾名前空間を含むコンマ区切りの一覧。|  
|**[表示]**|**false** の値は、配信拡張機能がユーザー インターフェイスに表示されないことを示します。 この属性が指定されない場合、既定値は **true**になります。|  
  
 RSReportServer.config ファイルの詳細については、「[Reporting Services 構成ファイル](../../../reporting-services/report-server/reporting-services-configuration-files.md)」を参照してください。  
  
## <a name="deploying-the-extension-to-the-report-server"></a>レポート サーバーへの拡張機能の配置  
 レポート サーバーでは、通知またはレポートを処理して配信するために配信拡張機能を使用します。 レポート サーバーには、プライベート アセンブリとして配信拡張機能アセンブリを配置する必要があります。 また、レポート サーバーの構成ファイル RSReportServer.config にエントリを作成する必要もあります。  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-a-report-server"></a>配信拡張機能アセンブリをレポート サーバーに配置するには  
  
1.  ステージング場所から、配信拡張機能を使用するレポート サーバーの bin ディレクトリにアセンブリをコピーします。 レポート サーバーの Bin ディレクトリの既定の場所は、%ProgramFiles%\Microsoft SQL Server\MSRS13.\<InstanceName>\Reporting Services\ReportServer\bin です。  
  
    > [!IMPORTANT]  
    >  既存の配信拡張機能アセンブリを上書きする場合、まず、レポート サーバー サービスを停止してから、更新済みのアセンブリをコピーする必要があります。 そのアセンブリをコピーした後で、サービスを再起動します。  
  
2.  アセンブリ ファイルをコピーした後、RSReportServer.config ファイルを開きます。 RSReportServer.config ファイルは、%ProgramFiles%\Microsoft SQL Server\MSRS13.\<InstanceName>\Reporting Services\ReportServer ディレクトリに格納されています。 配信拡張機能アセンブリ ファイルの構成ファイルにエントリを作成する必要があります。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] またはメモ帳などの簡単なテキスト エディターを使用して、構成ファイルを開くことができます。  
  
3.  RSReportServer.config ファイルで **Delivery** 要素を探します。 新しく作成した配信拡張機能のエントリは、次の場所に作成する必要があります。  
  
    ```  
    <Extensions>  
       <Delivery>  
          <Your extension configuration information goes here>  
       </Delivery>  
    </Extensions>  
    ```  
  
4.  配信拡張機能のエントリを追加します。 エントリには、**Name** および **Type** の値で構成される **Extension** 要素を含める必要があります。このエントリは次のようになります。  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryExtensionClass, AssemblyName" />  
    ```  
  
     **Name** の値は、配信拡張機能の一意な名前です。 **Type** の値は、<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> インターフェイスを実装するクラスの完全修飾名前空間のエントリを含むコンマ区切りの一覧であり、その後にアセンブリの名前 (.dll ファイル拡張子は付けない) が続きます。 既定では、配信拡張機能が表示されます。 Web ポータルなどのユーザー インターフェイスで拡張機能を非表示にするには、**Extension** 要素に **Visible** 属性を追加して、**false** に設定します。  
  
5.  最後に、配信拡張機能の **FullTrust** アクセス許可を与えるカスタム アセンブリのコード グループを追加します。 これを行うには、コード グループを rssrvpolicy.config ファイルに追加します。既定では、このファイルは %ProgramFiles%\Microsoft SQL Server\MSRS13.\<InstanceName>\Reporting Services\ReportServer にあります。 このコード グループは、次のようになります。  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my delivery extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS13.<InstanceName>\Reporting Services\ReportServer\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
     URL 構成要素は、配信拡張機能に選択できる多くの構成要素条件のうちの 1 つにすぎません。 [!INCLUDE[ssRS](../../../includes/ssrs.md)] のコード アクセス セキュリティの詳細については、「[セキュリティで保護された配置 &#40;Reporting Services&#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)」を参照してください。  
   
## <a name="verifying-the-deployment"></a>配置の確認  
 配信拡張機能が正常にレポート サーバーに配置されたかどうかを確認するには、Web サービスの <xref:ReportService2010.ReportingService2010.ListExtensions%2A> メソッドを使用します。 また、Web ポータルを開き、配信拡張機能がサブスクリプションに有効な配信拡張機能の一覧に含まれていることを確認する方法もあります。 Web ポータルとサブスクリプションの詳細については、「[サブスクリプションと配信 &#40;Reporting Services&#41;](../../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [配信拡張機能の実装](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
