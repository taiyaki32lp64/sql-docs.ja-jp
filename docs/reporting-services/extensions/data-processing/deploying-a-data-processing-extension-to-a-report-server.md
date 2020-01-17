---
title: データ処理拡張機能をレポート サーバーに配置する方法 | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- assemblies [Reporting Services], data processing extension deployments
ms.assetid: e00dface-70f8-434b-9763-8ebee18737d2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3f0b775b53244cd0a428bb4ce4023906d2f5119
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194124"
---
# <a name="deploying-a-data-processing-extension-to-a-report-server"></a>データ処理拡張機能のレポート サーバーへの配置
  レポート サーバーは、表示レポートのデータを取得および処理するためにデータ処理拡張機能を使用します。 データ処理拡張機能のアセンブリは、プライベート アセンブリとしてレポート サーバーに配置してください。 また、レポート サーバーの構成ファイル RSReportServer.config にエントリを作成する必要もあります。  
  
## <a name="procedures"></a>手順  
  
#### <a name="to-deploy-a-data-processing-extension-assembly"></a>データ処理拡張機能のアセンブリを配置するには  
  
1.  ステージング場所から、データ処理拡張機能を使用するレポート サーバーの bin ディレクトリにアセンブリをコピーします。 レポート サーバーの bin ディレクトリの既定場所は、%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<*インスタンス名*>\Reporting Services\ReportServer\bin です。  
  
    > [!NOTE]  
    >  この手順により、SQL Server の新しいインスタンスへのアップグレードが回避されます。 詳細については、「 [Upgrade and Migrate Reporting Services](../../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)」を参照してください。  
  
2.  アセンブリ ファイルをコピーした後、RSReportServer.config ファイルを開きます。 RSReportServer.config ファイルは、ReportServer ディレクトリにあります。 データ処理拡張機能アセンブリ ファイルの構成ファイルにエントリを作成する必要があります。 Visual Studio またはメモ帳などの簡単なテキスト エディターを使用して、構成ファイルを開くことができます。  
  
3.  RSReportServer.config ファイルで **Data** 要素を探します。 新しく作成したデータ処理拡張機能のエントリは、次の場所に作成する必要があります。  
  
    ```  
    <Extensions>  
       <Data>  
          <Your extension configuration information goes here>  
       </Data>  
    </Extensions>  
    ```  
  
4.  データ処理拡張機能のエントリを追加します。 エントリには、**Name** および **Type** の値で構成される **Extension** 要素を含める必要があります。このエントリは次のようになります。  
  
    ```  
    <Extension Name="ExtensionName" Type="CompanyName.ExtensionName.MyConnectionClass, MyExtensionAssembly" />  
    ```  
  
     **Name** の値は、データ処理拡張機能の一意の名前です。 **Type** の値は、<xref:Microsoft.ReportingServices.Interfaces.IExtension> インターフェイスおよび <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> インターフェイスを実装するクラスの完全修飾名前空間のエントリを含むコンマ区切りの一覧であり、その後にアセンブリの名前が続きます (.dll ファイル拡張子は含まない)。 既定では、データ処理拡張機能が表示されます。 レポート マネージャーなどのユーザー インターフェイスで拡張機能を非表示にするには、 **Extension** 要素に **Visible** 属性を追加して、 **false**に設定します。  
  
5.  最後に、拡張機能の **FullTrust** アクセス許可を付与するカスタム アセンブリのコード グループを追加します。 これを行うには、コード グループを rssrvpolicy.config ファイルに追加します。既定では、このファイルは %ProgramFiles%\Microsoft SQL Server\\<MSRS10_50.\<*インスタンス名*>\Reporting Services\ReportServer にあります。 このコード グループは、次のようになります。  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my data processing extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.<Instance Name>\Reporting Services\ReportServer\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 URL 構成要素は、データ処理拡張機能に選択できる多くの構成要素条件のうちの 1 つにすぎません。 [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のコード アクセス セキュリティの詳細については、「[セキュリティで保護された配置 &#40;Reporting Services&#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)」を参照してください。  
  
## <a name="verifying-the-deployment"></a>配置の確認  
 データ処理拡張機能がレポート サーバーに正常に配置されたかどうかを確認するには、Web サービス <xref:ReportService2010.ReportingService2010.ListExtensions%2A> メソッドを使用します。 レポート マネージャーを開いて、拡張機能が使用可能なデータ ソース一覧に含まれていることを確認することもできます。 レポート マネージャーとデータ ソースの詳細については、「[共有データ ソースを作成、変更、および削除する &#40;SSRS&#41;](../../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ処理拡張機能の配置](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Reporting Services の拡張機能](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [データ処理拡張機能の実装](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
