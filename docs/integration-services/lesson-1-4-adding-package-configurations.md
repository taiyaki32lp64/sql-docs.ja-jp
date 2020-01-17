---
title: 手順 4:パッケージ構成の追加 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e04a5321-63d5-4ec5-85b9-cb4eaf6c87f6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6ca9674a5bb3128e86d9cceaca4a971066da0fef
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283678"
---
# <a name="lesson-1-4---adding-package-configurations"></a>レッスン 1-4 - パッケージ構成の追加

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


ここでは、各パッケージに構成を追加します。 パッケージ プロパティとパッケージ オブジェクトの値は、構成によって実行時に更新されます。  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] にはさまざまな種類の構成があります。 構成は、環境変数、レジストリ エントリ、ユーザー定義変数、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] テーブル、XML ファイルに格納できます。 さらに柔軟性を高めるため、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では間接構成を使用することもできます。 これは、環境変数を使用して構成の場所を指定し、それによって実際の値を指定する方法です。 Deployment Tutorial プロジェクトのパッケージでは、XML 構成ファイルと間接構成を組み合わせて使用します。 XML 構成ファイルには、複数のプロパティの構成を含めることができ、必要に応じて複数のパッケージから参照できます。 このチュートリアルでは、パッケージごとに異なる構成ファイルを使用します。  
  
構成ファイルには、接続文字列などの機密情報が含まれる場合があります。 したがって、アクセス制御リスト (ACL) を使用して、ファイルを保存する場所やフォルダーへのアクセスを制限し、パッケージの実行が許可されているユーザーまたはアカウントにのみアクセス権を与える必要があります。 詳細については、「 [パッケージで使用されるファイルへのアクセス](../integration-services/security/security-overview-integration-services.md#files)」を参照してください。  
  
前の作業で Deployment Tutorial プロジェクトに追加したパッケージ (DataTransfer と LoadXMLData) は、ターゲット サーバーに配置した後で正常に実行できるようにするには、構成が必要になります。 構成を実装するには、最初に XML 構成ファイルの間接構成を作成し、次に XML 構成ファイルを作成します。  
  
DataTransferConfig.dtsConfig と LoadXMLData.dtsConfig の 2 つの構成ファイルを作成します。 これらのファイルには、パッケージで使用されるデータ ファイルとログ ファイルの場所を指定する名前と値のペアが含まれており、パッケージのプロパティはこれらの値で更新されます。 後で、配置プロセスの手順として、配置先のコンピューターのファイルの新しい場所が反映されるように構成ファイルの値を更新します。  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で、DataTransferConfig.dtsConfig と LoadXMLData.dtsConfig が DataTransfer および LoadXMLData パッケージと依存関係にあることが認識され、次のレッスンで配置バンドルを作成するときに構成ファイルが自動的に追加されます。  
  
### <a name="to-create-indirect-configuration-for-the-datatransfer-package"></a>DataTransfer パッケージの間接構成を作成するには  

プロジェクトの現在の配置モデルを確認し、必要に応じて **[パッケージ配置モデル]** に設定します。 **[プロジェクト]** メニューの **[パッケージ配置モデルに変換]** をクリックします。
  
1.  ソリューション エクスプローラーで DataTransfer.dtsx をダブルクリックします。  
  
2.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、制御フロー デザイン画面の背景をクリックします。  
  
3.  **[SSIS]** メニューの **[パッケージ構成]** をクリックします。  
  
4.  **[パッケージ構成オーガナイザー]** ダイアログ ボックスで、 **[パッケージの構成を有効にする]** をオンにして、 **[追加]** をクリックします。  
  
5.  パッケージ構成ウィザードの初期画面で、 **[次へ]** をクリックします。  
  
6.  [構成の種類の選択] ページで、 **[構成の種類]** ボックスの一覧から **[XML 構成ファイル]** を選択し、 **[構成の場所を環境変数に格納する]** オプションを選択して「 **DataTransfer** 」と入力するか、一覧から **[DataTransfer]** 環境変数を選択します。  
  
    > [!NOTE]  
    > 環境変数を一覧で選択できるようにするには、変数を追加した後でコンピューターを再起動する必要があります。 コンピューターの再起動を避けたい場合は、環境変数の名前を入力してください。  
  
7.  **[次へ]** をクリックします。  
  
8.  [ウィザードの完了] ページで、 **[構成名]** ボックスに「 **DataTransfer EV Configuration** 」と入力し、 **[プレビュー]** ペインで構成の内容を確認してから、 **[完了]** をクリックします。  
  
9. **[パッケージ構成オーガナイザー]** ダイアログ ボックスを閉じます。  
  
### <a name="to-create-the-xml-configuration-for-the-datatransfer-package"></a>DataTransfer パッケージの XML 構成を作成するには  
  
1.  ソリューション エクスプローラーで DataTransfer.dtsx をダブルクリックします。  
  
2.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、制御フロー デザイン画面の背景をクリックします。  
  
3.  **[SSIS]** メニューの **[パッケージ構成]** をクリックします。  
  
4.  [パッケージ構成オーガナイザー] ダイアログ ボックスで、 **[パッケージの構成を有効にする]** チェック ボックスをオンにし、 **[追加]** をクリックします。  
  
5.  パッケージ構成ウィザードの初期画面で、 **[次へ]** をクリックします。  
  
6.  [構成の種類の選択] ページで、 **[構成の種類]** ボックスの一覧から **[XML 構成ファイル]** を選択し、 **[参照]** をクリックします。  
  
7.  **[構成ファイルの場所の選択]** ダイアログ ボックスで、C:\DeploymentTutorial に移動し、 **[ファイル名]** ボックスに「 **DataTransferConfig** 」と入力してから、 **[保存]** をクリックします。  
  
8.  [構成の種類の選択] ページで **[次へ]** をクリックします。  
  
9. [エクスポートするプロパティの選択] ページで、DataTransfer、接続マネージャー、Deployment Tutorial Log、および Properties を展開し、 **[接続文字列]** チェック ボックスをオンにします。  
  
10. 接続マネージャー内で NewCustomers を展開し、 **[接続文字列]** チェック ボックスをオンにします。  
  
11. **[次へ]** をクリックします。  
  
12. [ウィザードの完了] ページで、 **[構成名]** ボックスに「 **DataTransfer Configuration** 」と入力し、構成の内容を確認してから、 **[完了]** をクリックします。  
  
13. **[パッケージ構成オーガナイザー]** ダイアログ ボックスで、DataTransfer EV Configuration が最初に、DataTransfer Configuration が 2 番目に表示されていることを確認し、 **[閉じる]** をクリックします。  
  
### <a name="to-create-indirect-configuration-for-the-loadxmldata-package"></a>LoadXMLData パッケージの間接構成を作成するには  
  
1.  ソリューション エクスプローラーで LoadXMLData.dtsx をダブルクリックします。  
  
2.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、制御フロー デザイン画面の背景をクリックします。  
  
3.  **[SSIS]** メニューの **[パッケージ構成]** をクリックします。  
  
4.  **[パッケージ構成オーガナイザー]** ダイアログ ボックスの **[追加]** をクリックします。  
  
5.  パッケージ構成ウィザードの初期画面で、 **[次へ]** をクリックします。  
  
6.  [構成の種類の選択] ページで、 **[構成の種類]** ボックスの一覧から **[XML 構成ファイル]** を選択し、 **[構成の場所を環境変数に格納する]** オプションを選択して「 **LoadXMLData** 」と入力するか、一覧から **[LoadXMLData]** 環境変数を選択します。  
  
    > [!NOTE]  
    > 環境変数を一覧で選択できるようにするには、変数を追加した後でコンピューターを再起動する必要があります。  
  
7.  **[次へ]** をクリックします。  
  
8.  [ウィザードの完了] ページで、 **[構成名]** ボックスに「 **LoadXMLData EV Configuration** 」と入力し、構成の内容を確認してから、 **[完了]** をクリックします。  
  
### <a name="to-create-the-xml-configuration-for-the-loadxmldata-package"></a>LoadXMLData パッケージの XML 構成を作成するには  
  
1.  ソリューション エクスプローラーで LoadXMLData.dtsx をダブルクリックします。  
  
2.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、制御フロー デザイン画面の背景をクリックします。  
  
3.  **[SSIS]** メニューの **[パッケージ構成]** をクリックします。  
  
4.  [パッケージ構成オーガナイザー] ダイアログ ボックスで、 **[パッケージの構成を有効にする]** チェック ボックスをオンにし、 **[追加]** をクリックします。  
  
5.  パッケージ構成ウィザードの初期画面で、 **[次へ]** をクリックします。  
  
6.  [構成の種類の選択] ページで、 **[構成の種類]** ボックスの一覧から **[XML 構成ファイル]** を選択し、 **[参照]** をクリックします。  
  
7.  **[構成ファイルの場所の選択]** ダイアログ ボックスで、C:\DeploymentTutorial に移動し、 **[ファイル名]** ボックスに「 **LoadXMLDataConfig** 」と入力してから、 **[保存]** をクリックします。  
  
8.  [構成の種類の選択] ページで **[次へ]** をクリックします。  
  
9. [エクスポートするプロパティの選択] ページで、LoadXMLData、実行可能ファイル、Load XML Data、および Properties を展開し、 **[XMLSource].[XMLData]** チェック ボックスと **[XMLSource].[XMLSchemaDefinition]** チェック ボックスをオンにします。  
  
10. **[次へ]** をクリックします。  
  
11. [ウィザードの完了] ページで、 **[構成名]** ボックスに「 **LoadXMLData Configuration** 」と入力し、構成の内容を確認してから、 **[完了]** をクリックします。  
  
12. **[パッケージ構成オーガナイザー]** ダイアログ ボックスで、LoadXMLData EV Configuration が最初に、LoadXMLData Configuration が 2 番目に表示されていることを確認し、 **[閉じる]** をクリックします。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
[手順 5:更新したパッケージのテスト](../integration-services/lesson-1-5-testing-the-updated-packages.md)  
  
## <a name="see-also"></a>参照  
[[パッケージ構成]](../integration-services/packages/package-configurations.md)  
[パッケージ構成を作成する](../integration-services/packages/create-package-configurations.md)  
[パッケージで使用されるファイルへのアクセス](../integration-services/security/security-overview-integration-services.md#files)  
