---
title: レポートまたはモデルを共有データ ソースにバインドする (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
ms.assetid: 23cc15f2-2883-48e2-bc6c-fa0ab61a2e21
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b6d973d4628e9c80b47c4fea0ef3476dbd05131f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107451"
---
# <a name="bind-a-report-or-model-to-a-shared-data-source-ssrs"></a>レポートまたはモデルを共有データ ソースにバインドする (SSRS)
  レポートまたはモデルをテスト サーバーから実稼働サーバーに移動するときなど、ファイルをローカル コンピューターに保存した後で別のレポート サーバーにアップロードする操作が必要になる場合があります。 レポートまたはモデルを新しいサーバーにアップロードしたときは、新しいレポート サーバー上に格納されている共有データ ソースにレポートまたはモデルを再バインドする必要があります。 レポートまたはモデルの再バインドを行わないと、レポートまたはモデルが新しいレポート サーバーからアクセスされたときに正常に動作しない場合があります。  
  
> [!IMPORTANT]  
>  レポートまたはモデルを共有データ ソースに再バインドする前に、データ ソースがレポート サーバーまたは SharePoint ライブラリに存在している必要があります。 データ ソースの詳細については、「[共有データ ソースを作成、変更、および削除する (SSRS)](create-modify-and-delete-shared-data-sources-ssrs.md)」を参照してください。  
  
### <a name="to-bind-a-report-or-model-to-a-shared-data-source-on-a-report-server-running-in-native-mode"></a>ネイティブ モードで実行されているレポート サーバー上の共有データ ソースにレポートまたはモデルをバインドするには  
  
1.  **レポート マネージャー**で、サーバーにアップロードしたレポートまたはモデルの名前をクリックします。  
  
     [プロパティ] タブが開きます。  
  
2.  **[データ ソース]** をクリックします。  
  
3.  **[参照]** をクリックし、レポートまたはモデルをバインドするデータ ソースを参照します。  
  
4.  データ ソースを選択し、 **[OK]** をクリックします。  
  
5.  **[適用]** をクリックします。  
  
     選択したデータ ソースにレポートまたはモデルがバインドされます。  
  
### <a name="to-bind-a-report-or-model-to-a-shared-data-source-on-a-report-server-running-in-sharepoint-integrated-mode"></a>SharePoint 統合モードで実行されているレポート サーバー上の共有データ ソースにレポートまたはモデルをバインドするには  
  
1.  まだライブラリが開いていない場合は、クイック起動バーでライブラリの名前をクリックします。 ライブラリの名前が表示されていない場合は、 **[すべてのサイト コンテンツの表示]** をクリックし、ライブラリの名前をクリックします。  
  
2.  レポートまたはモデルをポイントし、下矢印をクリックします。  
  
3.  **[データ ソースの管理]** をクリックします。  
  
4.  **[dataSource1]** をクリックします。  
  
5.  **[接続の種類]** 領域で、 **[共有データ ソース]** が選択されていることを確認します。  
  
6.  **[データ ソース リンク]** 領域で、省略記号ボタン ( [...] ) をクリックします。  
  
7.  使用するデータ ソースを探します。  
  
8.  データ ソースを選択し、 **[OK]** をクリックします。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. **[閉じる]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [ファイルまたはレポートをアップロードする (レポート マネージャー)](../reports/upload-a-file-or-report-report-manager.md)   
 [SharePoint ライブラリへのドキュメントのアップロード (Reporting Services の SharePoint モード)](../upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)   
 [共有データ ソースを作成および管理する (Reporting Services の SharePoint 統合モード)](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)   
 [共有データ ソースを作成、削除、または変更する &#40;レポート マネージャー&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [データ接続、データ ソース、および Reporting Services の接続文字列](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Reporting Services でサポートされるデータ ソース (SSRS)](../create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
