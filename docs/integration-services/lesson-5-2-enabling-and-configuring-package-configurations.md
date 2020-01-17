---
title: 手順 2:パッケージ構成の有効化と構成 | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 005218ab-8dd5-48e9-a185-6bc60cd43a7a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7706c124160f1f08f39279956d7685085859badd
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283137"
---
# <a name="lesson-5-2-enable-and-configure-package-configurations"></a>レッスン 5-2:パッケージ構成の有効化と構成

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



ここでは、パッケージ構成ウィザードを使用することで、プロジェクトをパッケージ配置モデルに変換してパッケージ構成を有効にします。 このウィザードを使用し、Foreach ループ コンテナーの **Directory** プロパティの構成設定が記述された XML 構成ファイルを生成します。 **Directory** プロパティの値は、実行時に更新できる新しいパッケージ レベル変数を使って指定します。 また、テストで使用するために、新しいサンプル データ フォルダーにデータを入力します。  
  
## <a name="create-a-package-level-variable-mapped-to-the-directory-property"></a>Directory プロパティにマップするパッケージ レベル変数を作成する  
  
1.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、 **[制御フロー]** タブの背景を選択します。 この選択により、作成する変数のスコープがこのパッケージに限定されます。  
  
2.  [ [!INCLUDE[ssIS](../includes/ssis-md.md)] ] メニューの **[変数]** をクリックします。  
  
3.  **[変数]** ウィンドウで、 **[変数の追加]** アイコンを選択します。  
  
4.  **[名前]** ボックスに「**varFolderName**」と入力します。  
  
    > [!IMPORTANT]  
    > 変数名の大文字と小文字は区別されます。  
  
5.  **[スコープ]** ボックスにパッケージの名前 (**Lesson 5**) が表示されていることを確認します。  
  
6.  **変数の** [データ型] `varFolderName` ボックスの値を **[String]** に設定します。  
  
7.  **[制御フロー]** タブに戻り、 **[Foreach File in Folder]** コンテナーをダブルクリックします。  
  
8.  **[Foreach ループ エディター]** の **[コレクション]** ページで、 **[Expressions]** を選択し、参照ボタン ( **...** ) を選択します。  
  
9. **[プロパティ式エディター]** で、 **[プロパティ]** 一覧内をクリックして **[Directory]** を選択します。  
  
10. **[式]** ボックスで、参照ボタン ( **...** ) を選択します。  
  
11. **[式ビルダー]** で **[変数とパラメーター]** フォルダーを展開し、**User::varFolderName** 変数を **[式]** ボックスへドラッグします。  
  
12. **[OK]** を選択して **[式ビルダー]** を閉じます。  
  
13. **[OK]** を選択して **[プロパティ式エディター]** を閉じます。  
  
14. **[OK]** を選択し、 **[Foreach ループ エディター]** を閉じます。  
  
## <a name="enable-package-configurations"></a>[パッケージの構成を有効にする]  
  
1.  **[プロジェクト]** メニューの **[パッケージ配置モデルに変換]** を選択します。  
  
2.  警告のメッセージで **[OK]** を選択し、変換が完了したら、 **[パッケージ配置モデルに変換]** ダイアログ ボックスで **[OK]** を選択します。  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、 **[制御フロー]** タブの背景を選択します。  
  
4.  **[SSIS]** メニューの **[パッケージ構成]** を選択します。  
  
5.  **[パッケージ構成オーガナイザー]** ダイアログ ボックスで **[パッケージの構成を有効にする]** を選択し、 **[追加]** を選択します。  
  
6.  **パッケージ構成ウィザード**の初期画面で、 **[次へ]** を選択します。  
  
7.  **[構成の種類の選択]** ページで、 **[構成の種類]** が **[XML 構成ファイル]** に設定されていることを確認します。  
  
8.  **[構成の種類の選択]** ページで **[参照]** を選択します。  
  
9. プロジェクト フォルダーで **[構成ファイルの場所の選択]** ダイアログ ボックスが開きます。  
  
10. **[構成ファイルの場所の選択]** ダイアログ ボックスで、 **[ファイル名]** に「**SSISTutorial**」と入力し、 **[保存]** を選択します。  
  
11. **[構成の種類の選択]** ページで **[次へ]** を選択します。
  
12. **[エクスポートするプロパティの選択]** ページの **[オブジェクト]** ペインで、 **[変数]** 、 **[varFolderName]** 、 **[Properties]** の順に展開し、 **[Value]** チェック ボックスをオンにします。  
  
13. **[エクスポートするプロパティの選択]** ページで **[次へ]** を選択します。  
  
14. **[ウィザードの完了]** ページで、構成の構成名を入力します。たとえば、「**SSIS Tutorial Directory configuration**」と入力します。 構成名は **[パッケージ構成オーガナイザー]** ダイアログ ボックスに表示されます。  
  
15. **[完了]** を選択します。  
  
16. **[閉じる]** を選択します。  
  
17. **SSISTutorial.dtsConfig** という名前の構成ファイルが作成されます。この構成ファイルには、変数の **Value** に対応する構成設定が含まれています。また、この変数値により、列挙子の **Directory** プロパティが設定されます。  
  
    > [!NOTE]  
    > 通常、構成ファイルにはパッケージのプロパティに関する複雑な情報が含まれていますが、このチュートリアルでは、次の構成情報のみを使用します。

    ```
    <Configuration 
        ConfiguredType="Property"  
        Path="\Package.Variables[User::varFolderName].Properties[Value]" 
        ValueType="String">  
      <ConfiguredValue></ConfiguredValue>  
    </Configuration>
    ```
  
## <a name="create-and-populate-a-new-sample-data-folder"></a>新しいサンプル データ フォルダーを作成して、データを取り込む  
  
1.  Windows エクスプローラーで、ドライブのルート レベル (**C:\\** など) にフォルダーを作成します。このフォルダーには「**New Sample Data**」という名前を付けてください。  
  
2.  コンピューター上でサンプル ファイルを探し、フォルダーから 3 つのファイルをコピーします。  
  
3.  コピーしたファイルを **New Sample Data** フォルダーに貼り付けます。  
  
## <a name="go-to-next-task"></a>次のタスクに進む  
[ステップ 3:Directory プロパティの構成値の変更](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
