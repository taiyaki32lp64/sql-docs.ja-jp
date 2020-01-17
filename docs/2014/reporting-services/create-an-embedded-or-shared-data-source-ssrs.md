---
title: 埋め込みまたは共有データ ソース (SSRS) を作成する |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], creating
ms.assetid: b111a8d0-a60d-4c8b-b00a-51644b19c34b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 088889518d88c5fd45f988fe03185e22f041b627
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109658"
---
# <a name="create-an-embedded-or-shared-data-source-ssrs"></a>埋め込みデータ ソースまたは共有データ ソースを作成する (SSRS)
  レポートのデータ ソースは名前と接続情報を指定します。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] は、"埋め込み" と "共有" の 2 種類のデータ ソースをサポートしています。 埋め込みデータ ソースは、レポート定義内で定義され、そのレポートでのみ使用されます。 共有データ ソースは、個別のアイテムとして定義され、複数のレポートで使用できます。 詳細については、次を参照してください。[埋め込みと共有のデータ接続またはデータ ソース&#40;レポート ビルダーおよび SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)します。  
  
 レポート ビルダーで、レポート サーバーまたは SharePoint サイト上の保存先を参照してデータ ソースを選択するか、または埋め込みデータ ソースを作成します。 共有データ ソースをレポート ビルダーで作成することはできません。  
  
 レポート デザイナーでは、共有データ ソースも埋め込みデータ ソースも作成できます。 レポート データ ペインからデータ ソースの参照の作成を開始し、選択、**新規**オプション。 データ ソースの参照を作成すると、ソリューション エクスプローラーの [共有データ ソース] フォルダーに新しい共有データ ソースが自動的に追加されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
 レポート サーバー上または SharePoint サイト上で共有データ ソースを直接作成することもできます。 詳細については、次を参照してください[作成、削除、または共有データ ソースを変更&#40;レポート マネージャー&#41; ](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)または[の作成と共有データ ソースの管理&#40;Reporting Services の SharePoint 統合モード&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md).  
  
### <a name="to-create-an-embedded-or-shared-data-source"></a>埋め込みデータ ソースまたは共有データ ソースを作成するには  
  
1.  ツール バーのレポート データ ペインで、 **[新規作成]** 、 **[データ ソース]** の順にクリックします。 **[データ ソースのプロパティ]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  レポート データ ペインが表示されていない場合は、 **[表示]** メニューの **[レポート データ]** をクリックします。  
  
2.  **[名前]** ボックスにデータ ソースの名前を入力するか、既定値をそのまま使用します。 データ ソース名は、レポートの内部で使用されます。 判別がつきやすいように、データ ソース名には、接続文字列に指定するデータベース名を含めることをお勧めします。  
  
3.  埋め込みデータ ソースのことを確認します**埋め込み接続**が選択されています。  
  
    1.  **[種類]** ボックスの一覧から、データ ソースの種類 ( **[Microsoft SQL Server]** や **[OLE DB]** など) を選択します。  
  
    2.  次の選択肢の 1 つを使用して、接続文字列を指定します。  
  
    -   **[接続文字列]** ボックスに接続文字列を直接入力します。 接続文字列の例の一覧は、次を参照してください[データ接続、データ ソース、およびレポート ビルダーでの接続文字列](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)または[データ接続、データ ソース、および Reporting Services内の接続文字列](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
    -   式 ( **[fx]** ) ボタンをクリックして、接続文字列を評価する式を作成します。 **[式]** ダイアログ ボックスで、式ペインに式を直接入力します。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    -   **[編集]** をクリックして、手順 2 で選択したデータ ソースの種類の **[接続のプロパティ]** ダイアログ ボックスを開きます。  
  
         データ ソースの種類に合わせて **[接続のプロパティ]** ダイアログ ボックスのフィールドに入力します。 接続のプロパティには、データ ソースの種類、データ ソースの名前、および使用する資格情報が含まれます。 このダイアログ ボックスで値を指定した後、 **[接続テスト]** をクリックして、データ ソースが使用可能であること、および指定した資格情報が正しいことを確認します。 特定のデータ ソースの種類の詳細については、「[外部データ ソースのデータを追加する (SSRS)](report-data/add-data-from-external-data-sources-ssrs.md)」のトピックを参照してください。  
  
4.  共有データ ソースのことを確認します**共有データ ソースの参照を使用する**が選択されています。  
  
    1.  **[新規]** をクリックします。 **[共有データ ソース]** のプロパティ ダイアログ ボックスで、手順 2. および 3. を実行して新規データ ソースを作成します。  
  
    2.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
         ソリューション エクスプローラーの [共有データ ソース] フォルダーに、新しい共有データ ソースが表示されます。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     データ ソースがレポート データ ペインに表示されます。 レポート データ ペイン内の共有データ ソースは、そのデータ ソースの定義を参照しています。 レポート ビルダーでは、データ ソースの定義は、レポート サーバー上または SharePoint サイト上に存在します。 レポート デザイナーでは、ソリューション エクスプローラーの [共有データ ソース] フォルダーにあるファイルがデータ ソースの定義です。  
  
### <a name="to-import-an-existing-data-source-in-report-designer"></a>レポート デザイナーで既存のデータ ソースをインポートするには  
  
1.  ソリューション エクスプローラーで、レポート サーバー プロジェクトの **[共有データ ソース]** フォルダーを右クリックして、 **[既存項目の追加]** をクリックします。 **[既存項目の追加]** ダイアログ ボックスが表示されます。  
  
2.  既存のレポート定義共有データ ソース (rds) ファイルを参照して、 **[開く]** をクリックします。  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-convert-an-embedded-data-source-to-a-shared-data-source-in-report-designer"></a>レポート デザイナーで埋め込みデータ ソースを共有データ ソースに変換するには  
  
-   レポート データ ペインで、データ ソースを右クリックし、**共有データ ソースに変換**します。  
  
### <a name="to-convert-a-shared-data-source-to-an-embedded-data-source-in-report-builder"></a>レポート ビルダーで共有データ ソースを埋め込みデータ ソースに変換するには  
  
-   レポート データ ペインでデータ ソースを右クリックし、開く**データ ソースのプロパティ**します。  
  
-   クリックして**埋め込まれた接続**前述の手順」の説明に従って、埋め込みデータ ソースの作成を完了します。  
  
## <a name="see-also"></a>参照  
 [Reporting Services データ ソースに資格情報を保存する](report-data/store-credentials-in-a-reporting-services-data-source.md)   
 [埋め込みおよび共有のデータ接続またはデータ ソース (レポート ビルダーおよび SSRS)](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [共有データ ソースからデータ ソースが埋め込まれた変換&#40;レポート ビルダーおよび SSRS&#41;](report-data/convert-data-sources-report-builder-and-ssrs.md)   
 [レポートまたはモデルを共有データ ソースにバインドする (SSRS)](report-data/bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [レポートのデータ ソースのプロパティを構成する (レポート マネージャー)](report-data/configure-data-source-properties-for-a-report-report-manager.md)   
 [Reporting Services でサポートされるデータ ソース (SSRS)](create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
