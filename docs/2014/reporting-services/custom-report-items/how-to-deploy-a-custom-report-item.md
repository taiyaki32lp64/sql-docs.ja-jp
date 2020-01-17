---
title: 操作方法:カスタム レポート アイテムの展開 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom report items, deploying
ms.assetid: 80e97b0d-e355-4240-aebd-08cbc84089ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2b41519ee6a6d31be33d92c8fbdf2ab503c93ec1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63265080"
---
# <a name="how-to-deploy-a-custom-report-item"></a>操作方法:カスタム レポート アイテムを配置する
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] でカスタム レポート アイテムを配置するには、レポート サーバー構成ファイルを変更し、デザイン時と実行時のコンポーネント アセンブリをレポート デザイナーとレポート サーバーの両方に対する適切なアプリケーション フォルダーにコピーする必要があります。  
  
### <a name="to-deploy-a-custom-report-item"></a>カスタム レポート アイテムを配置するには  
  
1.  Rsreportdesigner.config ファイルを編集して、デザイナーで使用するカスタム レポート アイテムの実行時とデザイン時のコンポーネントを構成します。 `ReportItemName` エントリは `CustomReportItemAttribute` クラス内で使用される `CustomReportItemDesigner` 属性と一致する必要があることに注意してください。 例 :  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    <ReportItemDesigner>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsDesigner, PolygonsDesigner" />  
    </ReportItemDesigner>  
    <ReportItemConverter>  
       <Converter Source="Chart" Target="Polygons" Type="PolygonsCRI.PolygonsConverter, PolygonsDesigner" />  
    </ReportItemConverter>  
    ```  
  
2.  Rsreportserver.config ファイルを編集して、カスタム レポート アイテムの実行時コンポーネントを登録します。 例 :  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    ```  
  
3.  Rsssrvpolicy.config ファイルを編集して、カスタム レポート アイテムに適切な権限を許可する `CodeGroup` を追加します。 以下に例を示します。  
  
    ```  
    <CodeGroup   
       class="UnionCodeGroup"   
       version="1"   
       PermissionSetName="FullTrust"  
       Description="This code group grants MyCustomReportItem.dll FullTrust permission. ">  
       <IMembershipCondition   
          class="UrlMembershipCondition"  
          version="1"  
       Url="C:\Program Files\Microsoft SQL Server\ MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin\MyCustomReportItem.dll" />  
    </CodeGroup>  
    ```  
  
4.  カスタム レポート アイテムの実行時コンポーネント DLL を、%ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies ディレクトリと \Program Files\Microsoft SQL Server\MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin ディレクトリにコピーします。  
  
5.  カスタム レポート アイテムのデザイン時コンポーネント DLL を %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies ディレクトリにコピーします。  
  
## <a name="see-also"></a>関連項目  
 [Reporting Services 構成ファイル](../report-server/reporting-services-configuration-files.md)   
 [カスタム レポート アイテムのクラス ライブラリ](custom-report-item-class-libraries.md)  
  
  
