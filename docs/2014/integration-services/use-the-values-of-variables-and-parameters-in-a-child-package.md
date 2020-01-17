---
title: 子パッケージで変数とパラメーターの値の使用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], passing between packages
- configurations [Integration Services]
- packages [Integration Services], configurations
- variables [Integration Services], adding
ms.assetid: 9b939edb-4e17-48e5-8428-855beb10049c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2425c15428dbaa05e9d29b2d9a89f8fc7d68f6c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054730"
---
# <a name="use-the-values-of-variables-and-parameters-in-a-child-package"></a>子パッケージでの変数およびパラメーターの値の使用
  この手順では、構成の種類として親変数を使用するパッケージ構成を作成する方法について説明します。 この構成の種類を使用すると、親パッケージから実行される子パッケージが親内の変数にアクセスできるようになります。  
  
> [!NOTE]  
>  親パッケージの変数またはパラメーター、またはプロジェクトのパラメーターを子パッケージのパラメーターにマップするようにパッケージ実行タスクを構成することで、値を子パッケージに渡すこともできます。 詳細については、「 [パッケージ実行タスク](control-flow/execute-package-task.md)」を参照してください。  
  
 親パッケージ内のこの変数は、子パッケージのパッケージ構成を作成する前に作成する必要はありません。 変数はいつでも親パッケージに追加できますが、パッケージ構成では親変数の正確な名前を使用する必要があります。 ただし、親変数パッケージ構成を作成するには、子パッケージ内に、この構成で更新できる変数が既に存在している必要があります。 変数の追加と構成の詳細については、「 [パッケージ内のユーザー定義変数のスコープの追加、削除、変更](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)」を参照してください。  
  
 親変数パッケージ構成で使用される親パッケージ内の変数のスコープは、パッケージ実行タスク、タスクを含むコンテナー、またはパッケージに設定できます。 パッケージ内で同じ名前の複数の変数が定義されている場合、パッケージ実行タスクのスコープ内で最も近い変数が使用されます。 パッケージ実行タスクに最も近いスコープは、タスク自体です。  
  
### <a name="to-add-a-variable-to-a-parent-package"></a>親パッケージに変数を追加するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、子パッケージに渡す変数の追加先パッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、変数のスコープを定義するには、次のいずれかの操作を行います。  
  
    -   スコープをパッケージに設定するには、 **[制御フロー]** タブのデザイン画面上の任意の場所をクリックします。  
  
    -   スコープをパッケージ実行タスクの親コンテナーに設定するには、コンテナーをクリックします。  
  
    -   スコープをパッケージ実行タスクに設定するには、タスクをクリックします。  
  
4.  変数を追加および構成します。  
  
    > [!NOTE]  
    >  変数で格納するデータと互換性のあるデータ型を選択します。  
  
5.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="to-add-a-variable-to-a-child-package"></a>子パッケージに変数を追加するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、親変数パッケージ構成の追加先パッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、スコープをパッケージに設定するには、 **[制御フロー]** タブのデザイン画面上の任意の場所をクリックします。  
  
4.  変数を追加および構成します。  
  
    > [!NOTE]  
    >  変数で格納するデータと互換性のあるデータ型を選択します。  
  
5.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="to-add-a-parent-package-configuration-to-a-child-package"></a>親パッケージ構成を子パッケージに追加するには  
  
1.  子パッケージが開かれていない場合は、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で開きます。  
  
2.  **[制御フロー]** タブのデザイン画面で任意の場所をクリックします。  
  
3.  **[SSIS]** メニューの **[パッケージ構成]** をクリックします。  
  
4.  **[パッケージ構成オーガナイザー]** ダイアログ ボックスで、 **[パッケージの構成を有効にする]** を選択し、 **[追加]** をクリックします。  
  
5.  パッケージ構成ウィザードの初期画面で、 **[次へ]** をクリックします。  
  
6.  [構成の種類の選択] ページの **[構成の種類]** ボックスの一覧で、 **[親パッケージ変数]** を選択して、次のいずれかの操作を行います。  
  
    -   **[構成設定を直接指定する]** を選択し、 **[親変数]** ボックスで、その構成で使用する親パッケージ内の変数名を指定します。  
  
        > [!IMPORTANT]  
        >  変数名では大文字と小文字が区別されます。  
  
    -   **[構成の場所を環境変数に格納する]** を選択し、 **[環境変数]** ボックスの一覧で、変数の名前を含む環境変数を選択します。  
  
7.  [**次へ**] をクリックします。  
  
8.  [対象になるプロパティの選択] ページで、 **[変数]** ノードを展開し、構成する変数の **[プロパティ]** ノードを展開した後、構成によって設定されるプロパティをクリックします。  
  
9. [**次へ**] をクリックします。  
  
10. [ウィザードの完了] ページで、必要に応じて、構成の既定の名前を変更し、構成情報を確認します。  
  
11. **[完了]** をクリックしてウィザードを完了し、 **[パッケージ構成オーガナイザー]** ダイアログ ボックスに戻ります。  
  
12. **[パッケージ構成オーガナイザー]** ダイアログ ボックスの **[構成]** タブに、新しい構成が表示されます。  
  
13. **[閉じる]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [[パッケージ構成]](../../2014/integration-services/package-configurations.md)   
 [パッケージ構成を作成する](../../2014/integration-services/create-package-configurations.md)   
 [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)   
 [パッケージで変数を使用する](../../2014/integration-services/use-variables-in-packages.md)  
  
  
