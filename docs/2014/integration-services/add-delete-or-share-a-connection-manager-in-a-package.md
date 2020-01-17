---
title: 追加、削除、または共有パッケージ内の接続マネージャー |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], adding
- adding connection managers
ms.assetid: 6f2ba4ea-10be-4c40-9e80-7efcf6ee9655
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8b7d92800a2f5d55cf85ace3e7746d934b7474b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062008"
---
# <a name="add-delete-or-share-a-connection-manager-in-a-package"></a>パッケージの接続マネージャーを追加、削除、または共有する
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、リレーショナル データベース、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベース、CSV 形式のファイル、XML 形式のファイルなど、さまざまなデータ ソースに接続するための各種接続マネージャーがあります。 接続マネージャーは、パッケージ レベルまたはプロジェクト レベルで作成できます。 プロジェクト レベルで作成した接続マネージャーは、プロジェクト内のすべてのパッケージで使用できます。 一方、パッケージ レベルで作成した接続マネージャーは、特定のパッケージでのみ使用できます。  
  
 データ ソースの代わりにプロジェクト レベルで作成された接続マネージャーを使用して、ソースへの接続を共有します。 プロジェクト レベルで接続マネージャーを追加するには、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトでプロジェクト配置モデルを使用する必要があります。 このモデルを使用するようにプロジェクトが構成されている場合、 **[接続マネージャー]** フォルダーが **ソリューション エクスプローラー**に表示され、 **[データ ソース]** フォルダーが **ソリューション エクスプローラー**から削除されます。  
  
> [!NOTE]  
>  パッケージでデータ ソースを使用する場合は、プロジェクトをパッケージ配置モデルに変換する必要があります。  
>   
>  2 つのモデルの詳細については、「 [プロジェクトとパッケージの展開](packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。 プロジェクト配置モデルへのプロジェクトの変換の詳細については、「 [Integration Services サーバーへのプロジェクトの配置](../../2014/integration-services/deploy-projects-to-integration-services-server.md)」を参照してください。  
  
 次の手順はすべての種類の接続マネージャーに適用されます。次のタスクの実行方法について説明します。  
  
-   [パッケージの作成時に、接続マネージャーを追加するには](#wizard)  
  
-   [接続マネージャーを既存のパッケージに追加するには](#package)  
  
-   [プロジェクト レベルの接続マネージャーを追加するには](#project)  
  
-   [接続マネージャーのプロパティのパラメーターを作成するには](#parameter)  
  
-   [接続マネージャーをパッケージから削除するには](#DeletePackageLevel)  
  
-   [共有接続マネージャー (プロジェクト レベルの接続マネージャー) を削除するには](#DeleteProjectLevel)  
  
##  <a name="wizard"></a> パッケージの作成時に、接続マネージャーを追加するには  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードを使用します。  
  
     接続マネージャーの作成と構成に加えて、このウィザードでは、接続マネージャーを使用する変換元および変換先の作成と構成を行うこともできます。 詳細については、「 [SQL Server データ ツールでのパッケージの作成](create-packages-in-sql-server-data-tools.md)」を参照してください。  
  
##  <a name="package"></a> 接続マネージャーを既存のパッケージに追加するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、 **[制御フロー]** タブ、 **[データ フロー]** タブ、または **[イベント ハンドラー]** タブをクリックして、 **[接続マネージャー]** 領域を表示します。  
  
4.  **[接続マネージャー]** 領域で任意の場所を右クリックし、次のいずれかの操作を行います。  
  
    -   パッケージに追加する接続マネージャーの種類をクリックします。  
  
         \- または -  
  
    -   追加する種類が一覧にない場合は、 **[新しい接続]** をクリックして **[SSIS 接続マネージャーの追加]** ダイアログ ボックスを開き、接続マネージャーの種類を選択してから **[OK]** をクリックします。  
  
     選択した接続マネージャーの種類に応じたカスタム ダイアログ ボックスが開きます。 接続マネージャーの種類と設定可能なオプションの詳細については、次のオプションの表を参照してください。  
  
    |[ODBC 入力元エディター]|および|  
    |------------------------|-------------|  
    |[ADO 接続マネージャー](connection-manager/ado-connection-manager.md)|[[OLE DB 接続マネージャーの構成]](configure-ole-db-connection-manager.md)|  
    |[ADO.NET 接続マネージャー](connection-manager/ado-net-connection-manager.md)|[[ADO.NET の接続マネージャーの構成]](configure-ado-net-connection-manager.md)|  
    |[Analysis Services 接続マネージャー](connection-manager/analysis-services-connection-manager.md)|[[Analysis Services 接続マネージャーの追加] ダイアログ ボックスの UI リファレンス](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 接続マネージャー](connection-manager/excel-connection-manager.md)|[Excel 接続マネージャー エディター](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[ファイル接続マネージャー](connection-manager/file-connection-manager.md)|[ファイル接続マネージャー エディター](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[複数ファイル接続マネージャー](connection-manager/multiple-files-connection-manager.md)|[[ファイル接続マネージャーの追加] ダイアログ ボックスの UI リファレンス](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[フラット ファイル接続マネージャー](connection-manager/flat-file-connection-manager.md)|[[フラット ファイル接続マネージャー エディター] &#40;[全般] ページ&#41;](general-page-of-integration-services-designers-options.md)<br /><br /> [[フラット ファイル接続マネージャー エディター] &#40;[列] ページ&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [[フラット ファイル接続マネージャー エディター] &#40;[詳細設定] ページ&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [[フラット ファイル接続マネージャー エディター] ([プレビュー] ページ)](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[複数フラット ファイル接続マネージャー](connection-manager/multiple-flat-files-connection-manager.md)|[[複数フラット ファイル接続マネージャー エディター] ([全般] ページ)](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [[複数フラット ファイル接続マネージャー エディター] ([列] ページ)](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [[複数フラット ファイル接続マネージャー エディター] ([詳細設定] ページ)](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [[複数フラット ファイル接続マネージャー エディター] &#40;[プレビュー] ページ&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 接続マネージャー](connection-manager/ftp-connection-manager.md)|[FTP 接続マネージャー エディター](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[HTTP 接続マネージャー](connection-manager/http-connection-manager.md)|[[HTTP 接続マネージャー エディター] ([サーバー] ページ)](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [[HTTP 接続マネージャー エディター] ([プロキシ] ページ)](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 接続マネージャー](connection-manager/msmq-connection-manager.md)|[MSMQ 接続マネージャー エディター](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[ODBC 接続マネージャー](connection-manager/odbc-connection-manager.md)|[ODBC 接続マネージャーの UI リファレンス](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 接続マネージャー](connection-manager/ole-db-connection-manager.md)|[[OLE DB 接続マネージャーの構成]](configure-ole-db-connection-manager.md)|  
    |[SMO 接続マネージャー](connection-manager/smo-connection-manager.md)|[SMO 接続マネージャー エディター](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[SMTP 接続マネージャー](connection-manager/smtp-connection-manager.md)|[SMTP 接続マネージャー エディター](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 接続マネージャー](connection-manager/sql-server-compact-edition-connection-manager.md)|[[SQL Server Compact Edition 接続マネージャー エディター] &#40;[接続] ページ&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [[SQL Server Compact Edition 接続マネージャー エディター] &#40;[すべて] ページ&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 接続マネージャー](connection-manager/wmi-connection-manager.md)|[WMI 接続マネージャー エディター](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
     **[接続マネージャー]** 領域に、追加した接続マネージャーが一覧表示されます。  
  
5.  必要に応じて、接続マネージャーを右クリックし、 **[名前の変更]** をクリックして、接続マネージャーの既定の名前を変更します。  
  
6.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
##  <a name="project"></a> プロジェクト レベルの接続マネージャーを追加するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  **ソリューション エクスプローラー**で **[接続マネージャー]** を右クリックし、 **[新しい接続マネージャー]** をクリックします。  
  
3.  **[SSIS 接続マネージャーの追加]** ダイアログ ボックスで、接続マネージャーの種類を選択し、 **[追加]** をクリックします。  
  
     選択した接続マネージャーの種類に応じたカスタム ダイアログ ボックスが開きます。 接続マネージャーの種類と設定可能なオプションの詳細については、次のオプションの表を参照してください。  
  
    |[ODBC 入力元エディター]|および|  
    |------------------------|-------------|  
    |[ADO 接続マネージャー](connection-manager/ado-connection-manager.md)|[[OLE DB 接続マネージャーの構成]](configure-ole-db-connection-manager.md)|  
    |[ADO.NET 接続マネージャー](connection-manager/ado-net-connection-manager.md)|[[ADO.NET の接続マネージャーの構成]](configure-ado-net-connection-manager.md)|  
    |[Analysis Services 接続マネージャー](connection-manager/analysis-services-connection-manager.md)|[[Analysis Services 接続マネージャーの追加] ダイアログ ボックスの UI リファレンス](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 接続マネージャー](connection-manager/excel-connection-manager.md)|[Excel 接続マネージャー エディター](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[ファイル接続マネージャー](connection-manager/file-connection-manager.md)|[ファイル接続マネージャー エディター](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[複数ファイル接続マネージャー](connection-manager/multiple-files-connection-manager.md)|[[ファイル接続マネージャーの追加] ダイアログ ボックスの UI リファレンス](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[フラット ファイル接続マネージャー](connection-manager/flat-file-connection-manager.md)|[[フラット ファイル接続マネージャー エディター] &#40;[全般] ページ&#41;](general-page-of-integration-services-designers-options.md)<br /><br /> [[フラット ファイル接続マネージャー エディター] &#40;[列] ページ&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [[フラット ファイル接続マネージャー エディター] &#40;[詳細設定] ページ&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [[フラット ファイル接続マネージャー エディター] ([プレビュー] ページ)](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[複数フラット ファイル接続マネージャー](connection-manager/multiple-flat-files-connection-manager.md)|[[複数フラット ファイル接続マネージャー エディター] ([全般] ページ)](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [[複数フラット ファイル接続マネージャー エディター] ([列] ページ)](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [[複数フラット ファイル接続マネージャー エディター] ([詳細設定] ページ)](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [[複数フラット ファイル接続マネージャー エディター] &#40;[プレビュー] ページ&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 接続マネージャー](connection-manager/ftp-connection-manager.md)|[FTP 接続マネージャー エディター](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[HTTP 接続マネージャー](connection-manager/http-connection-manager.md)|[[HTTP 接続マネージャー エディター] ([サーバー] ページ)](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [[HTTP 接続マネージャー エディター] ([プロキシ] ページ)](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 接続マネージャー](connection-manager/msmq-connection-manager.md)|[MSMQ 接続マネージャー エディター](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[ODBC 接続マネージャー](connection-manager/odbc-connection-manager.md)|[ODBC 接続マネージャーの UI リファレンス](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 接続マネージャー](connection-manager/ole-db-connection-manager.md)|[[OLE DB 接続マネージャーの構成]](configure-ole-db-connection-manager.md)|  
    |[SMO 接続マネージャー](connection-manager/smo-connection-manager.md)|[SMO 接続マネージャー エディター](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[SMTP 接続マネージャー](connection-manager/smtp-connection-manager.md)|[SMTP 接続マネージャー エディター](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 接続マネージャー](connection-manager/sql-server-compact-edition-connection-manager.md)|[[SQL Server Compact Edition 接続マネージャー エディター] &#40;[接続] ページ&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [[SQL Server Compact Edition 接続マネージャー エディター] &#40;[すべて] ページ&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 接続マネージャー](connection-manager/wmi-connection-manager.md)|[WMI 接続マネージャー エディター](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
     追加した接続マネージャーが、 **ソリューション エクスプローラー** の **[接続マネージャー]** ノードの下に表示されます。 また、プロジェクト内のすべてのパッケージの **[SSIS デザイナー]** ウィンドウの **[接続マネージャー]** タブにも表示されます。 このタブに表示される接続マネージャーの名前の前には **(プロジェクト)** と表記され、パッケージ レベルの接続マネージャーと区別されます。  
  
4.  必要に応じて、 **[ソリューション マネージャー]** ウィンドウの **[接続マネージャー]** ノードまたは **[SSIS デザイナー]** ウィンドウの **[接続マネージャー]** タブで接続マネージャーを右クリックし、 **[名前の変更]** をクリックして、接続マネージャーの既定の名前を変更します。  
  
    > [!NOTE]  
    >  **[SSIS デザイナー]** ウィンドウの **[接続マネージャー]** タブでは、接続マネージャーの名前の前に表示されている **(プロジェクト)** を上書きすることはできません。 これは仕様です。  
  
##  <a name="parameter"></a> 接続マネージャーのプロパティのパラメーターを作成するには  
  
1.  **[接続マネージャー]** 領域で、パラメーターを作成する接続マネージャーを右クリックし、 **[パラメーター化]** をクリックします。  
  
2.  **[パラメーター化]** ダイアログ ボックスでパラメーター設定を構成します。 詳細については、「 [[パラメーター化] ダイアログ ボックス](../../2014/integration-services/parameterize-dialog-box.md)」を参照してください。  
  
##  <a name="DeletePackageLevel"></a> 接続マネージャーをパッケージから削除するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、 **[制御フロー]** タブ、 **[データ フロー]** タブ、または **[イベント ハンドラー]** タブをクリックして、 **[接続マネージャー]** 領域を表示します。  
  
4.  削除する接続マネージャーを右クリックして、 **[削除]** をクリックします。  
  
     SQL 実行タスクや OLE DB ソースなどのパッケージ要素が使用している接続マネージャーを削除すると、結果は次のようになります。  
  
    -   削除された接続マネージャーを使用していたパッケージ要素にエラー アイコンが表示されます。  
  
    -   パッケージの検証に失敗します。  
  
    -   パッケージを実行できません。  
  
5.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
##  <a name="DeleteProjectLevel"></a> 共有接続マネージャー (プロジェクト レベルの接続マネージャー) を削除するには  
  
1.  プロジェクト レベルの接続マネージャーを削除するには、 **[ソリューション エクスプローラー]** ウィンドウの **[接続マネージャー]** ノードで接続マネージャーを右クリックし、 **[削除]** をクリックします。 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] で次のような警告メッセージが表示されます。  
  
    > [!WARNING]  
    >  プロジェクト接続マネージャーを削除すると、その接続マネージャーを使用するパッケージが動作しなくなる場合があります。 この操作を元に戻すことはできません。 接続マネージャーを削除しますか。  
  
2.  接続マネージャーを削除するには [OK] をクリックし、削除しない場合は [キャンセル] をクリックします。  
  
    > [!NOTE]  
    >  プロジェクトのパッケージに対して開いた **[SSIS デザイナー]** ウィンドウの **[接続マネージャー]** タブから、プロジェクト レベルの接続マネージャーを削除することもできます。 そのためには、タブで接続マネージャーを右クリックし、 **[削除]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; の接続](connection-manager/integration-services-ssis-connections.md)   
 [接続マネージャーのプロパティを設定する](../../2014/integration-services/set-the-properties-of-a-connection-manager.md)  
  
  
