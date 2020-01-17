---
title: 手順 2:配置バンドルの確認 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 6c13f5c9-c75e-4e52-94dc-2d2db2c578fe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 127044042eed7f082b6f1f7ba7ae6918232ba9ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62891771"
---
# <a name="step-2-verifying-the-deployment-bundle"></a>手順 2:配置バンドルの確認
  レッスン 1 では、Deployment Tutorial プロジェクトを作成し、パッケージと補助ファイルをプロジェクトに追加しました。前のタスクでプロジェクトの配置ユーティリティを構築しました。  
  
 このタスクでは、配置バンドルの内容を確認します。 配置バンドルとは、目的のコンピューターにコピーしてパッケージのインストールに使用するフォルダーです。 配置ユーティリティの場所として既定値の bin\Deployment を使用した場合は、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトの Deployment Tutorial フォルダー内にある Bin\Deployment フォルダーが配置バンドルです。  
  
### <a name="to-verify-the-content-of-deployment-bundle"></a>配置バンドルの内容を確認するには  
  
1.  コンピューターで bin\Deployment フォルダーを見つけます。  
  
2.  次のファイルがあることを確認します。  
  
    -   DataTransfer.dtsx  
  
    -   datatransferconfig.dtsconfig  
  
    -   Deployment Tutorial.SSISDeploymentManifest  
  
    -   LoadXMLData.dtsx  
  
    -   loadxmldataconfig.dtsconfig  
  
    -   NewCustomers.txt  
  
    -   orders.xml  
  
    -   orders.xsd  
  
    -   Readme.txt  
  
3.  [Deployment Tutorial.SSISDeploymentManifest] を右クリックし、 **[ファイルを開くアプリケーションの選択]** をポイントして、 **[Internet Explorer]** をクリックします。 メモ帳などのテキスト エディターでもファイルを開くことができます。 ファイルの XML コードは次のようになっています。  
  
     `<?xml version="1.0"?><DTSDeploymentManifest GeneratedBy="Domain\UserName" GeneratedFromProjectName="Deployment Tutorial" GeneratedDate="2006-02-24T13:29:02.6537669-08:00" AllowConfigurationChanges="true"><Package>DataTransfer.dtsx</Package><Package>LoadXMLData.dtsx</Package><ConfigurationFile>datatransferconfig.dtsconfig</ConfigurationFile><ConfigurationFile>loadxmldataconfig.dtsconfig</ConfigurationFile><MiscellaneousFile>Readme.txt</MiscellaneousFile><MiscellaneousFile>orders.xml</MiscellaneousFile><MiscellaneousFile>NewCustomers.txt</MiscellaneousFile><MiscellaneousFile>orders.xsd</MiscellaneousFile></DTSDeploymentManifest>`  
  
4.  いることを確認の値、`AllowConfigurationChanges`属性が**true** XML に含まれて、`Package`の 2 つのパッケージの各要素を`MiscellaneousFile`パッケージ以外の 4 つのファイルの各要素と`ConfigurationFile`それぞれの 2 つの XML 構成ファイルの要素です。  
  
5.  Internet Explorer またはテキスト エディターを終了します。  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 3:パッケージをインストールします。](../integration-services/lesson-3-install-ssis-package.md)  
  
![Integration Services のアイコン (小)](media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
  
