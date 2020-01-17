---
title: 表示拡張機能の配置 | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- deploying [Reporting Services], extensions
- rendering extensions [Reporting Services], deploying
ms.assetid: 9fb8c887-5cb2-476e-895a-7b0e2dd11398
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 10c822b8cd292c975309443f9196fb7ceb66cbc5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193699"
---
# <a name="deploying-a-rendering-extension"></a>表示拡張機能の配置
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のレポート表示拡張機能は、作成して [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ライブラリにコンパイルした後、レポート サーバーおよびレポート デザイナーで検出できるようにする必要があります。 それには、拡張機能を適切なディレクトリにコピーし、適切な [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 構成ファイルにエントリを追加します。  
  
## <a name="configuration-file-rendering-extension-element"></a>構成ファイルの表示拡張機能要素  
 表示拡張機能を .DLL にコンパイルした後、rsreportserver.config ファイルにエントリを追加します。 既定では、%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<InstanceName>\Reporting Services\ReportServer にあります。 親要素は \<Render> です。 Render 要素の下には、各表示拡張機能の Extension 要素があります。 **Extension** 要素には、Name と Type という 2 つの属性があります。  
  
 次の表では、表示拡張機能の **Extension** 要素の属性について説明します。  
  
|属性|[説明]|  
|---------------|-----------------|  
|**[名前]**|拡張機能の一意の名前。 **Name** 属性の最大文字数は 255 文字です。 名前は、構成ファイルの **Extensions** 要素内のすべてのエントリの中で一意にする必要があります。 重複する名前がある場合には、レポート サーバーによってエラーが返されます。|  
|**型**|アセンブリの名前と共に完全修飾名前空間を含むコンマ区切りの一覧。|  
|**[表示]**|値が **false** の場合、表示拡張機能がユーザー インターフェイスに表示されないことを示します。 この属性が指定されない場合、既定値は **true**になります。|  
|**LogAllExecutionRequests**|値が **false** の場合、エントリがログに記録されるのは、セッションでレポートが最初に実行されるときのみであることを示します。 この属性が指定されない場合、既定値は **true**になります。<br /><br /> この設定によって、レポートに最初に表示されるページについてのみエントリをログに記録するか ( **false**の場合)、レポートに表示されるページごとにエントリをログに記録するか ( **true**の場合) が決まります。|  
  
 詳細については、「 [RsReportServer.config 構成ファイル](../../../reporting-services/report-server/rsreportserver-config-configuration-file.md)」を参照してください。  
  
## <a name="deploying-the-extension-to-the-report-server"></a>レポート サーバーへの拡張機能の配置  
 レポート サーバーでは、レポートを他の形式にエクスポートするとき、表示拡張機能を使用します。 レポート サーバーにプライベート アセンブリとして表示拡張機能アセンブリを配置する必要があります。 また、レポート サーバーの構成ファイル rsreportserver.config にエントリを作成する必要もあります。  
  
### <a name="to-deploy-the-assembly"></a>アセンブリを配置するには  
  
1.  ステージング場所から、表示拡張機能を使用するレポート サーバーの bin ディレクトリにアセンブリをコピーします。 レポート サーバーの Bin ディレクトリの既定の場所は、%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<InstanceName>\Reporting Services\ReportServer\Bin です。  
  
2.  アセンブリ ファイルをコピーした後、rsreportserver.config ファイルを開きます。 rsreportserver.config ファイルもレポート サーバーの bin ディレクトリにあります。 構成ファイルに拡張機能アセンブリ ファイルのエントリを作成する必要があります。 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] または簡単なテキスト エディターを使用して、ファイルを開くことができます。  
  
     詳細については、「 [RsReportServer.config 構成ファイル](../../../reporting-services/report-server/rsreportserver-config-configuration-file.md)」を参照してください。  
  
3.  Rsreportserver.config ファイルで **Render** 要素を探します。 新しく作成した拡張機能のエントリは、次の場所に作成する必要があります。  
  
    ```  
    <Extensions>  
       <Render>  
          <extension configuration>  
       </Render>  
    </Extensions>  
    ```  
  
4.  表示拡張機能のエントリを追加します。 エントリには、 **Name** および **Type**の値で構成される要素を含める必要があります。このエントリは次のようになります。  
  
    ```  
    <Extension Name="My Rendering Extension Name" Type="CompanyName.ExtensionName.MyRenderingProvider, AssemblyName" />  
    ```  
  
     **Name** の値は、表示拡張機能の一意な名前です。 **Type** の値は、<xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension> 実装の完全修飾名前空間に続けて、アセンブリの名前 (.dll ファイル拡張子を含まない) をコンマで区切って指定したものです。 既定では、表示拡張機能が表示されます。 レポート マネージャーなどのユーザー インターフェイスで拡張機能を非表示にするには、 **Extension** 要素に **Visible** 属性を追加して、 **false**に設定します。  
  
## <a name="verifying-the-deployment"></a>配置の確認  
 また、レポート マネージャーを開き、配信拡張機能がレポートに有効なエクスポートの種類の一覧に含まれていることを確認することもできます。  
  
## <a name="see-also"></a>参照  
 [表示拡張機能の実装](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [表示拡張機能の概要](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [IRenderingExtension インターフェイスの実装](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [拡張機能のセキュリティに関する考慮事項](../../../reporting-services/extensions/security-considerations-for-extensions.md)  
  
  
