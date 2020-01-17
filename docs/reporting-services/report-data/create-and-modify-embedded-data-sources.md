---
title: 埋め込みデータ ソースを作成および変更する | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 1c38c2e8-7a29-4f79-a4a3-85ed2b13723b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0daca68faa97a59b9c98b13ab9ca8f867341917c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66500466"
---
# <a name="create-and-modify-embedded-data-sources"></a>埋め込みデータ ソースを作成および変更する
  埋め込みデータ ソースは、レポート定義内で定義され、そのレポートでのみ使用されます。  
  
## <a name="to-create-an-embedded-data-source-in-report-designer"></a>レポート デザイナーで埋め込みデータ ソースを作成するには  
  
1.  ツール バーのレポート データ ペインで、 **[新規作成]** 、 **[データ ソース]** の順にクリックします。 **[データ ソースのプロパティ]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  レポート データ ペインが表示されていない場合は、 **[表示]** メニューの **[レポート データ]** をクリックします。  
  
2.  **[名前]** ボックスにデータ ソースの名前を入力するか、既定値をそのまま使用します。 データ ソース名は、レポートの内部で使用されます。 判別がつきやすいように、データ ソース名には、接続文字列に指定するデータベース名を含めることをお勧めします。  
  
3.  **[埋め込み接続]** が選択されていることを確認し、以下のことを行います。  
  
    1.  **[種類]** ボックスの一覧から、データ ソースの種類 ( **[Microsoft SQL Server]** や **[OLE DB]** など) を選択します。  
  
    2.  次の選択肢の 1 つを使用して、接続文字列を指定します。  
  
        -   **[接続文字列]** ボックスに接続文字列を直接入力します。 接続文字列の例の一覧については、「[レポート ビルダーでのデータ接続、データ ソース、および接続文字列](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)」または[データ接続、データ ソース、および接続文字列 (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)に関するページを参照してください。  
  
        -   式 ( **[fx]** ) ボタンをクリックして、接続文字列を評価する式を作成します。 **[式]** ダイアログ ボックスで、式ペインに式を直接入力します。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
        -   **[編集]** をクリックして、手順 2 で選択したデータ ソースの種類の **[接続のプロパティ]** ダイアログ ボックスを開きます。  
  
             データ ソースの種類に合わせて **[接続のプロパティ]** ダイアログ ボックスのフィールドに入力します。 接続のプロパティには、データ ソースの種類、データ ソースの名前、および使用する資格情報が含まれます。 このダイアログ ボックスで値を指定した後、 **[接続テスト]** をクリックして、データ ソースが使用可能であること、および指定した資格情報が正しいことを確認します。 特定のデータ ソースの種類の詳細については、「[外部データ ソースのデータを追加する (SSRS)](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md)」のトピックを参照してください。  
  
    3.  **[資格情報]** をクリックします。  
  
         このデータ ソースに使用する資格情報を指定します。 サポートされる資格情報の種類は、データ ソースの所有者によって選択されます。  
  
4.  新しい埋め込みデータ ソースがレポート データ ペインに表示されます。  
  
## <a name="to-create-an-embedded-data-source-in-report-builder"></a>レポート ビルダーで埋め込みデータ ソースを作成するには  
  
1.  ツール バーのレポート データ ペインで、 **[新規作成]** 、 **[データ ソース]** の順にクリックします。 **[データ ソースのプロパティ]** ダイアログ ボックスが表示されます。  
  
2.  **[名前]** ボックスにデータ ソースの名前を入力するか、既定値をそのまま使用します。  
  
3.  **[個人用レポートに埋め込まれている接続を使用]** がオンになっていることを確認します。  
  
    1.  **[接続の種類の選択]** ボックスの一覧から、データ ソースの種類 ( **[Microsoft SQL Server]** や **[OLE DB]** など) を選択します。  
  
    2.  次の選択肢の 1 つを使用して、接続文字列を指定します。  
  
        -   **[接続文字列]** ボックスに接続文字列を直接入力します。 接続文字列の例の一覧については、「 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)」を参照してください。  
  
        -   式 ( **[fx]** ) ボタンをクリックして、接続文字列を評価する式を作成します。 **[式]** ダイアログ ボックスで、式ペインに式を直接入力します。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
        -   **[構築]** をクリックして、手順 2 で選択したデータ ソースの種類の **[接続のプロパティ]** ダイアログ ボックスを開きます。  
  
             データ ソースの種類に合わせて **[接続のプロパティ]** ダイアログ ボックスのフィールドに入力します。 接続のプロパティには、データ ソースの種類、データ ソースの名前、および使用する資格情報が含まれます。 このダイアログ ボックスで値を指定した後、 **[接続テスト]** をクリックして、データ ソースが使用可能であること、および指定した資格情報が正しいことを確認します。  
  
4.  **[資格情報]** をクリックします。  
  
     このデータ ソースに使用する資格情報を指定します。 サポートされる資格情報の種類は、データ ソースの所有者によって選択されます。 詳細については、「 [レポート データ ソースに関する資格情報と接続情報を指定する](specify-credential-and-connection-information-for-report-data-sources.md)」をご覧ください。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     データ ソースがレポート データ ペインに表示されます。  
  
## <a name="see-also"></a>参照  
 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [レポート データ ソースに関する資格情報と接続情報を指定する](specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
