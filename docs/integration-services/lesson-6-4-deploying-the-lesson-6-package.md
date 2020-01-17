---
title: 手順 4:レッスン 6 のパッケージを配置する | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: b613cef7-7993-4d89-a429-a8251d74d435
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2a16cd38eef12584f8d876e610bfda5d602c3076
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283013"
---
# <a name="lesson-6-4-deploy-the-lesson-6-package"></a>レッスン 6-4:レッスン 6 のパッケージを配置する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



パッケージを配置するには、SQL Server インスタンスの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の SSISDB カタログにパッケージを追加する必要があります。 このレッスンでは、SSISDB カタログにレッスン 6 のパッケージを追加し、新しいパラメーターを設定し、パッケージを実行します。 このレッスンでは、SQL Server Management Studio を使用して SSISDB カタログにレッスン 6 パッケージを追加し、パッケージを配置します。 パッケージを配置したら、新しい場所を指すようにパラメーターを変更し、パッケージを実行します。   
このタスクの内容:  

1. SQL Server の SSIS ノードの SSISDB カタログにパッケージを追加します。  
  
2. パッケージを配置します。  
  
3. パッケージ パラメーターの値を設定します。  

4. SSMS でパッケージを実行します。  
  
## <a name="locate-or-add-the-ssisdb-catalog"></a>SSISDB カタログを検索または追加する  
  
1.  **[スタート]**  >  **[すべてのプログラム]**  >  **[Microsoft SQL Server 2017]** の順に選択し、 **[SQL Management Studio]** を選択します。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスで既定の設定を確認し、 **[接続]** を選択します。 接続するには、SQL Server がインストールされているコンピューターの名前と**サーバー**名が一致する必要があります。 **データベース エンジン**が名前付きインスタンスの場合は、**サーバー**名は *\<コンピューター名>\\\<インスタンス名>* という形式のインスタンス名になります。 
  
3.  **オブジェクト エクスプローラー**で、 **[Integration Services カタログ]** を展開します。  
  
4.  **[Integration Services カタログ]** の下にカタログが表示されない場合は、SSISDB カタログを追加します。  
  
5.  SSISDB カタログを追加するには、 **[Integration Services カタログ]** を右クリックし、 **[カタログの作成]** を選択します。  
  
6.  **[カタログの作成]** ダイアログ ボックスで、 **[CLR 統合を有効にする]** を選択します。  
  
7.  **[パスワード]** ボックスにパスワードを入力し、 **[パスワードの再入力]** ボックスにもう一度入力します。 
  
8.  **[OK]** を選択して SSISDB カタログを追加します。  
  
## <a name="add-the-package-to-the-ssisdb-catalog"></a>SSISDB カタログにパッケージを追加する  
  
1.  **オブジェクト エクスプローラー**で、 **[SSISDB]** を右クリックし、 **[フォルダーの作成]** を選択します。  
  
2.  **[フォルダーの作成]** ダイアログ ボックスで、[フォルダー名] ボックスに「SSIS Tutorial」と入力し、 **[OK]** を選択します。  
  
3.  **SSIS Tutorial** フォルダーを展開し、 **[プロジェクト]** を右クリックし、 **[パッケージのインポート]** を選択します。  
  
4.  **[Integration Services プロジェクトの変換ウィザードの概要]** **ページで**、 **[次へ]** を選択します。  
  
5.  **[パッケージの検索]** ページの **[ソース]** の一覧で、**ファイル システム**が選択されていることを確認し、 **[参照]** を選択します。  
  
6.  **[フォルダーの参照]** ダイアログ ボックスで、この SSIS Tutorial プロジェクトを含むフォルダーに移動し、 **[OK]** を選択します。  
  
7.  **[次へ]** を選択します。  
  
8.  [パッケージの選択] ページに SSIS Tutorial の 6 つパッケージがすべて表示されます。 **[パッケージ]** の一覧で、 **[Lesson 6.dtsx]** を選択し、 **[次へ]** を選択します。  
  
9. **[配置先の選択]** ページで、 **[プロジェクト名]** ボックスに「**SSIS Tutorial Deployment**」と入力し、 **[次へ]** を選択します。

10. 残りのウィザードの各ページで **[次へ]** を選択し、 **[確認]** ページまで進みます。  
  
11. **[確認]** ページで **[変換]** を選択します。  
  
12. 変換が完了したら、 **[閉じる]** を選択します。  
  
Integration Services プロジェクトの変換ウィザードを閉じると、Integration Services 配置ウィザードが表示されます。 次に、このウィザードを使用してレッスン 6 パッケージを配置します。  
  
1.  **[Integration Services 配置ウィザードの概要]** **ページで** 、プロジェクトを配置する手順を確認し、 **[次へ]** を選択します。  
  
2.  **[配置先の選択]** ページで、サーバー名が SSISDB カタログを含む SQL Server のインスタンスであることと、パスが **SSIS Tutorial Deployment** を示していることを確認し、 **[次へ]** を選択します。  
  
3.  **[確認]** ページで**概要**を確認し、 **[配置]** を選択します。  
  
4.  配置が完了したら、 **[閉じる]** を選択します。  
  
5.  **オブジェクト エクスプローラー**で、 **[Integration Services カタログ]** を右クリックし、 **[更新]** を選択します。  
  
6.  **[Integration Services カタログ]** を展開し、 **[SSISDB]** を展開します。 プロジェクトが完全に展開されるまで、**SSIS Tutorial** の下のツリーを展開します。 **SSIS Tutorial Deployment** ノードの**パッケージ** ノードの下に **Lesson 6.dtsx** が表示されます。  
  
7.  パッケージが完了したことを確認するには、 **[Lesson 6.dtsx]** を右クリックし、 **[構成]** を選択します。 **[構成]** ダイアログ ボックスで **[パラメーター]** を選択し、 **[コンテナー]** に **Lesson 6.dtsx** のエントリ、 **[名前]** に **VarFolderName**、[値] に**新しいサンプル データ**へのパスがあることを確認し、 **[閉じる]** を選択します。  
  
## <a name="create-and-populate-a-new-sample-data-folder"></a>新しいサンプル データ フォルダーを作成して、データを取り込む  
  
1.  **Windows エクスプローラー**で、ドライブのルート レベル (**C:\\** など) にフォルダーを作成します。このフォルダーには "**Sample Data Two**" という名前を付けてください。  
  
2.  [レッスン 1 の前提条件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)から **Sample Data** フォルダーを開き、サンプル ファイルを 3 つコピーします。  
  
3.  **Sample Data Two** フォルダーに進み、コピーしたファイルを貼り付けます。  
  
## <a name="change-the-package-parameter-to-point-to-the-new-sample-data"></a>新しいサンプル データを指すようにパッケージ パラメーターを変更する  
  
1.  **オブジェクト エクスプローラー**で、 **[Lesson 6.dtsx]** を右クリックし、 **[構成]** を選択します。  
  
2.  **[構成]** ダイアログ ボックスで、パラメーター値を **Sample Data Two** へのパスに変更します。たとえば、**C:\\Sample Data Two** にします。  
  
3.  **[OK]** を選択して **[構成]** ダイアログ ボックスを閉じます。  
  
## <a name="test-the-lesson-6-package-deployment"></a>レッスン 6 パッケージの配置をテストする  
  
1.  **オブジェクト エクスプローラー**で、 **[Lesson 6.dtsx]** を右クリックし、 **[実行]** を選択します。  
  
2.  **[パッケージの実行]** ダイアログ ボックスで、 **[OK]** を選択します。  
  
3.  [メッセージ] ダイアログ ボックスで **[はい]** を選択し、 **[概要レポート]** を開きます。  
  
パッケージの**概要レポート**には、パッケージの名前と状態の概要が表示されます。 **[実行の概要]** セクションには、パッケージの各タスクの結果が表示されます。 **[使用されたパラメーター]** セクションには、パッケージの実行で使用されたすべてのパラメーターの名前と値が表示されます (**VarFolderName** など)。  
  
