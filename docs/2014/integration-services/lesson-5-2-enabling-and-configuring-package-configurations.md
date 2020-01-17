---
title: 手順 2:有効にして、パッケージの構成 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 005218ab-8dd5-48e9-a185-6bc60cd43a7a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fa75b3a71832eaba4064de5a9dd90e73236e8177
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62891071"
---
# <a name="step-2-enabling-and-configuring-package-configurations"></a>手順 2:パッケージ構成の有効化と構成
  ここでは、パッケージ構成ウィザードを使用することで、プロジェクトをパッケージ配置モデルに変換してパッケージ構成を有効にします。 ここでは、Foreach ループ コンテナーの `Directory` プロパティの構成設定が記述された XML 構成ファイルを生成します。 Directory プロパティの値は、実行時に更新できる新しいパッケージ レベル変数を使って指定します。 また、テスト時に使用する新しいサンプル データを作成します。  
  
### <a name="to-create-a-new-package-level-variable-mapped-to-the-directory-property"></a>Directory プロパティにマップする新しいパッケージ レベル変数を作成するには  
  
1.  **デザイナーで、** [制御フロー] [!INCLUDE[ssIS](../includes/ssis-md.md)] タブの背景をクリックします。 これにより、作成する変数のスコープがこのパッケージに限定されます。  
  
2.  [ [!INCLUDE[ssIS](../includes/ssis-md.md)] ] メニューの **[変数]** をクリックします。  
  
3.  **[変数]** ウィンドウで、[変数の追加] アイコンをクリックします。  
  
4.  **[名前]** ボックスに「 **varFolderName**」と入力します。  
  
    > [!IMPORTANT]  
    >  変数名では大文字と小文字が区別されます。  
  
5.  **[スコープ]** ボックスにパッケージの名前 (Lesson 5) が表示されていることを確認します。  
  
6.  **変数の** [データ型] `varFolderName` ボックスの値を **[String]** に設定します。  
  
7.  **[制御フロー]** タブに戻り、 **[Foreach File in Folder]** コンテナーをダブルクリックします。  
  
8.  **[Foreach ループ エディター]** の **[コレクション]** ページで、 **[Expressions]** をクリックし、参照ボタン ( **[...]** ) をクリックします。  
  
9. **プロパティ式エディター**、クリックして、**プロパティ**一覧`Directory`します。  
  
10. **式**ボックスで、省略記号ボタンをクリックします **([...])。** .  
  
11. **[式ビルダー]** で [変数] フォルダーを展開し、 **User::varFolderName** 変数を **[式]** ボックスへドラッグします。  
  
12. **[OK]** をクリックして **[式ビルダー]** を閉じます。  
  
13. **[OK]** をクリックして **[プロパティ式エディター]** を閉じます。  
  
14. **[OK]** をクリックし、 **[Foreach ループ エディター]** を閉じます。  
  
### <a name="to-enable-package-configurations"></a>パッケージ構成を有効にするには  
  
1.  **[プロジェクト]** メニューの **[パッケージ配置モデルに変換]** をクリックします。  
  
2.  警告のメッセージで **[OK]** をクリックし、変換が完了したら、 **[パッケージ配置モデルに変換]** ダイアログで **[OK]** をクリックします。  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、 **[制御フロー]** タブの背景をクリックします。  
  
4.  **[SSIS]** メニューの **[パッケージ構成]** をクリックします。  
  
5.  **[パッケージ構成オーガナイザー]** ダイアログ ボックスで **[パッケージの構成を有効にする]** をクリックし、 **[追加]** をクリックします。  
  
6.  パッケージ構成ウィザードの初期画面で、 **[次へ]** をクリックします。  
  
7.  **[構成の種類の選択]** ページで、 **[構成の種類]** が **[XML 構成ファイル]** に設定されていることを確認します。  
  
8.  **[構成の種類の選択]** ページで **[参照]** をクリックします。  
  
9. **[構成ファイルの場所の選択]** ダイアログ ボックスが開きます。既定の場所はプロジェクト フォルダーです。  
  
10. **[構成ファイルの場所の選択]** ダイアログ ボックスで、 **[ファイル名]** に「 **SSISTutorial**」と入力し、 **[保存]** をクリックします。  
  
11. **[構成の種類の選択]** ページで **[次へ]** をクリックします。  
  
12. **[エクスポートするプロパティの選択]** ページの **[オブジェクト]** ペインで、 **[変数]** 、 **[varFolderName]** 、 **[Properties]** の順に展開し、 **[Value]** チェック ボックスをオンにします。  
  
13. **[エクスポートするプロパティの選択]** ページで **[次へ]** をクリックします。  
  
14. **[ウィザードの完了]** ページで、作成した構成の構成名を入力します。たとえば、「 **SSIS Tutorial Directory configuration**」と入力します。 ここに入力した構成名が **[パッケージ構成オーガナイザー]** ダイアログ ボックスに表示されます。  
  
15. **[完了]** をクリックします。  
  
16. **[閉じる]** をクリックします。  
  
17. ウィザードの構成設定を含む、SSISTutorial.dtsConfig という名前の構成ファイルを作成する、`value`順番を設定する変数の`Directory`列挙子のプロパティ。  
  
    > [!NOTE]  
    >  通常、構成ファイルにはパッケージのプロパティに関する複雑な情報が含まれていますが、このチュートリアルでは、次の構成情報のみを使用します:  
    > <Configuration ConfiguredType="Property"  
    > Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"\>  
    >  \<ConfiguredValue>\</ConfiguredValue>  
    > \</構成 >。  
  
### <a name="to-create-and-populate-a-new-sample-data-folder"></a>新しいサンプル データ フォルダーを作成して、データを取り込むには  
  
1.  Windows エクスプ ローラーで、ドライブのルート レベル (たとえば、c:\\)、という名前の新しいフォルダーを作成`New Sample Data`します。  
  
2.  コンピューター上でサンプル ファイルを探し、フォルダーから 3 つのファイルをコピーします。  
  
3.  `New Sample Data`フォルダーをコピーしたファイルを貼り付けます。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [ステップ 3:Directory プロパティの構成値の変更](lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
  
