---
title: 追加および確認するデータ接続またはデータ ソース (レポート ビルダーおよび SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1d3b2573-e29d-480d-9dde-d26379c86618
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ca1e5d039a7ea7aacd930f47eb99f854cbce8cac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107517"
---
# <a name="add-and-verify-a-data-connection-or-data-source-report-builder-and-ssrs"></a>データ接続またはデータ ソースの追加および確認 (レポート ビルダーおよび SSRS)
  レポート ビルダーでは、レポート サーバーから共有データ ソースを追加することも、レポートで使用される埋め込みデータ ソースを作成することもできます。 レポート デザイナーでは、共有データ ソースまたは埋め込みデータ ソースを作成して、レポート サーバーに配置することができます。  
  
 レポートに共有データ ソースを追加するには、レポート サーバーを参照して共有データ ソースを選択します。 レポート内の共有データ ソースは、レポート サーバー上の共有データ ソース定義を参照しています。  
  
 埋め込みデータ ソースを作成するには、データの外部ソースへの接続情報が必要で、データへのアクセスに必要な権限を把握している必要があります。 通常、この情報は、データ ソースの所有者から得られます。 接続をテストすることによって、指定されている資格情報が十分かどうかを確認できます。  
  
 詳細については、「[レポート ビルダーでのデータ接続、データ ソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-report-builder.md)」および「[レポート ビルダーでの資格情報の指定](../specify-credentials-in-report-builder.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-reference-to-a-shared-data-source"></a>共有データ ソースの参照を作成するには  
  
1.  ツール バーのレポート データ ペインで、 **[新規作成]** 、 **[データ ソース]** の順にクリックします。 **[データ ソースのプロパティ]** ダイアログ ボックスが表示されます。  
  
2.  **[名前]** ボックスに、データ ソースの名前を入力します。  
  
    > [!NOTE]  
    >  この名前は、ローカル レポート定義に保存されます。 この名前は、レポート サーバー上の共有データ ソースの名前ではありません。  
  
3.  **[共有接続またはレポート モデルを使用する]** を選択します。 最近使用した共有データ ソースおよびレポート モデルの一覧が表示されます。 レポート サーバーから共有データ ソースを 1 つ選択するには、 **[参照]** をクリックし、共有データ ソースを使用できるレポート サーバー上のフォルダーを参照します。  
  
4.  共有データ ソースを選択し、 **[開く]** をクリックします。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 データ ソースがレポート データ ペインに表示されます。  
  
### <a name="to-create-an-embedded-data-source"></a>埋め込みデータ ソースを作成するには  
  
1.  ツール バーのレポート データ ペインで、 **[新規作成]** 、 **[データ ソース]** の順にクリックします。 **[データ ソースのプロパティ]** ダイアログ ボックスが表示されます。  
  
2.  **[名前]** ボックスにデータ ソースの名前を入力するか、既定値をそのまま使用します。  
  
3.  **[個人用レポートに埋め込まれている接続を使用]** がオンになっていることを確認します。  
  
    1.  **[接続の種類の選択]** ボックスの一覧から、データ ソースの種類 ( **[Microsoft SQL Server]** や **[OLE DB]** など) を選択します。  
  
    2.  次の選択肢の 1 つを使用して、接続文字列を指定します。  
  
    -   **[接続文字列]** ボックスに接続文字列を直接入力します。 接続文字列の例の一覧については、「 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-report-builder.md)」を参照してください。  
  
    -   式 ( **[fx]** ) ボタンをクリックして、接続文字列を評価する式を作成します。 **[式]** ダイアログ ボックスで、式ペインに式を直接入力します。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    -   **[構築]** をクリックして、手順 2 で選択したデータ ソースの種類の **[接続のプロパティ]** ダイアログ ボックスを開きます。  
  
         データ ソースの種類に合わせて **[接続のプロパティ]** ダイアログ ボックスのフィールドに入力します。 接続のプロパティには、データ ソースの種類、データ ソースの名前、および使用する資格情報が含まれます。 このダイアログ ボックスで値を指定した後、 **[接続テスト]** をクリックして、データ ソースが使用可能であること、および指定した資格情報が正しいことを確認します。  
  
4.  **[資格情報]** をクリックします。  
  
     このデータ ソースに使用する資格情報を指定します。 サポートされる資格情報の種類は、データ ソースの所有者によって選択されます。 場合によっては、データ ソースの所有者がレポート サーバーで共有データ ソースを管理し、そのデータ ソースで使用可能な資格情報を構成していることがあります。 この情報については、データ ソースの所有者に問い合わせてください。 詳細については、「 [レポート ビルダーでの資格情報の指定](../specify-credentials-in-report-builder.md)」を参照してください。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 データ ソースがレポート データ ペインに表示されます。  
  
### <a name="to-verify-a-data-connection"></a>データ接続を確認するには  
  
1.  レポート データ ペインのツール バーで、データ ソースをダブルクリックします。 **[データ ソースのプロパティ]** ダイアログ ボックスが表示されます。  
  
2.  **[接続テスト]** をクリックします。  
  
3.  接続が成功した場合は、次のメッセージが表示されます。「接続が正常に作成します。」 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  接続が成功しなかった場合は、次のメッセージが表示されます。「データ ソースに接続できません。」  
  
5.  **[詳細]** をクリックし、情報に基づいて問題を修正します。  
  
     詳細については、「 [レポート ビルダーでの資格情報の指定](../specify-credentials-in-report-builder.md)」を参照してください。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](report-datasets-ssrs.md)   
 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [レポートの検索、表示、管理 (レポート ビルダーおよび SSRS)](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
  
