---
title: 接続マネージャーのプロパティを設定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], modifying
- modifying connection managers
ms.assetid: 54793114-2198-4d80-8091-e241d5a5d13c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1e3d0780e761cb5b0cdd4fd267bdfb2662f55cf4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055834"
---
# <a name="set-the-properties-of-a-connection-manager"></a>接続マネージャーのプロパティを設定する
  すべての接続マネージャーは **[プロパティ]** ウィンドウを使用して構成できます。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のさまざまな種類の接続マネージャーを変更するためのカスタム ダイアログ ボックスも用意されています。 ダイアログ ボックスに表示されるオプションは、接続マネージャーの種類によって異なります。  
  
### <a name="to-modify-a-connection-manager-using-the-properties-window"></a>[プロパティ] ウィンドウを使用して接続マネージャーを変更するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  SSIS デザイナーで、 **[制御フロー]** タブ、 **[データ フロー]** タブ、または **[イベント ハンドラー]** タブをクリックして、 **[接続マネージャー]** 領域を表示します。  
  
4.  接続マネージャーを右クリックして、 **[プロパティ]** をクリックします。  
  
5.  **[プロパティ]** ウィンドウで、プロパティの値を編集します。 **[プロパティ]** ウィンドウでは、接続マネージャーの標準エディターで構成できないプロパティにもアクセスできます。  
  
6.  **[OK]** をクリックします。  
  
7.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="to-modify-a-connection-manager-using-a-connection-manager-dialog-box"></a>接続マネージャーのダイアログ ボックスを使用して接続マネージャーを変更するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、 **[制御フロー]** タブ、 **[データ フロー]** タブ、または **[イベント ハンドラー]** タブをクリックして、 **[接続マネージャー]** 領域を表示します。  
  
4.  **[接続マネージャー]** 領域で接続マネージャーをダブルクリックして、 **[接続マネージャー]** ダイアログ ボックスを開きます。 特定の種類の接続マネージャーおよび各種類で使用するオプションの詳細については、次の表を参照してください。  
  
    |[接続マネージャー]|および|  
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
  
5.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; の接続](connection-manager/integration-services-ssis-connections.md)   
 [パッケージの接続マネージャーを追加、削除、または共有する](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)  
  
  
