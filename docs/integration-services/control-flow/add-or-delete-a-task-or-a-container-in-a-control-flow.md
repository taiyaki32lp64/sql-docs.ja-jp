---
title: 制御フローのタスクまたはコンテナーを追加または削除する | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], adding
- adding tasks
- adding containers
- tasks [Integration Services], adding
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 76e7db001469b141df5633228927135c6d01af53
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298438"
---
# <a name="add-or-delete-a-task-or-a-container-in-a-control-flow"></a>制御フローのタスクまたはコンテナーを追加または削除する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  制御フロー デザイナーでの作業中、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーのツールボックスには、パッケージの制御フローの作成用に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で用意されているタスクが一覧表示されます。 ツールボックスの詳細については、「 [SSIS ツールボックス](../../integration-services/ssis-toolbox.md)」を参照してください。  
  
 1 つのパッケージには、同じタスクのインスタンスを複数含めることができます。 タスクの各インスタンスは、パッケージ内で一意に識別され、各インスタンスは個別に構成できます。  
  
 タスクを削除すると、そのタスクを制御フロー内の別のタスクやコンテナーに連結する優先順位制約も、同様に削除されます。  
  
 次の手順では、パッケージの制御フローのタスクまたはコンテナーを追加または削除する方法について説明します。  
  
## <a name="add-a-task-or-a-container-to-a-control-flow"></a>制御フローにタスクまたはコンテナーを追加する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。  
  
4.  **[ツールボックス]** を開くには、 **[表示]** メニューの **[ツールボックス]** をクリックします。  
  
5.  **[制御フロー項目]** と **[メンテナンス タスク]** を展開します。  
  
6.  タスクとコンテナーを、 **[ツールボックス]** から **[制御フロー]** タブのデザイン画面にドラッグします。  
  
7.  パッケージの制御フロー内のタスクまたはコンテナーのコネクタをドラッグし、タスクまたはコンテナーを制御フロー内の別のコンポーネントに連結します。  
  
8.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="delete-a-task-or-a-container-from-a-control-flow"></a>制御フローからタスクまたはコンテナーを削除する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。 次のいずれかの操作を行います。  
  
    -   **[制御フロー]** タブをクリックし、削除するタスクまたはコンテナーを右クリックして **[削除]** をクリックします。  
  
    -   **パッケージ エクスプローラー**を開きます。 **[実行可能ファイル]** フォルダーで削除するタスクまたはコンテナーを右クリックし、 **[削除]** をクリックします。  
  
3.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  

## <a name="set-the-properties-of-a-task-or-container"></a>タスクまたはコンテナーのプロパティを設定する
タスクおよびコンテナーのほとんどのプロパティは、 **[プロパティ]** ウィンドウを使用して設定できます。 例外は、タスク コレクションのプロパティと、 **[プロパティ]** ウィンドウを使用して設定するには複雑すぎるプロパティです。 たとえば、Foreach ループ コンテナーが使用する列挙子を **[プロパティ]** ウィンドウで構成することはできません。 これらの複雑なプロパティを設定するには、タスク エディターまたはコンテナー エディターを使用する必要があります。 ほとんどの場合、タスク エディターとコンテナー エディターには複数のノードがあり、各ノードには関連プロパティが含まれています。 ノードの名前は、ノードに含まれるプロパティの対象を示します。  
  
 次の手順では、 **[プロパティ]** ウィンドウを使用するか、対応するタスク エディターまたはコンテナー エディターを使用してタスクまたはコンテナーのプロパティを設定する方法を説明します。  
  
### <a name="set-the-properties-of-a-task-or-container-with-the-properties-window"></a>プロパティ ウィンドウを使用してタスクまたはコンテナーのプロパティを設定する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。  
  
4.  **[制御フロー]** タブのデザイン画面でタスクまたはコンテナーを右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[プロパティ]** ウィンドウで、プロパティの値を更新します。  
  
    > [!NOTE]  
    >  ほとんどのプロパティは、テキスト ボックスに値を直接入力するか、一覧から値を選択することによって設定できます。 ただし、カスタムのプロパティ エディターが用意されている複雑なプロパティもあります。 このプロパティを設定するには、テキスト ボックス内をクリックしてから、作成ボタン ( **[...]** ) をクリックしてカスタム エディターを開きます。  
  
6.  必要に応じて、タスクまたはコンテナーのプロパティを動的に更新するプロパティ式を作成します。 詳細については、「 [プロパティ式を追加または変更する](../../integration-services/expressions/add-or-change-a-property-expression.md)」を参照してください。  
  
7.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="set-the-properties-of-a-task-or-container-with-the-task-or-container-editor"></a>タスクまたはコンテナー エディターを使用してタスクまたはコンテナーのプロパティを設定する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。  
  
4.  **[制御フロー]** タブのデザイン画面でタスクまたはコンテナーを右クリックし、ショートカット メニューの **[編集]** をクリックして、対応するタスク エディターまたはコンテナー エディターを開きます。  
  
     For ループ コンテナーの構成方法については、「 [Configure a For Loop Container](https://msdn.microsoft.com/library/b9cd7ea7-b198-4a35-8b16-6acf09611ca5)」(For ループ コンテナーを構成する) を参照してください。  
  
     Foreach ループ コンテナーの構成方法については、「 [Configure a Foreach Loop Container](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)」(Foreach ループ コンテナーを構成する) を参照してください。  
  
    > [!NOTE]  
    >  シーケンス コンテナーには、カスタム エディターはありません。  
  
5.  タスク エディターまたはコンテナー エディターに複数のノードがある場合、設定するプロパティが含まれるノードをクリックします。  
  
6.  必要に応じて **[式]** をクリックし、 **[式]** ページで、タスクまたはコンテナーのプロパティを動的に更新するプロパティ式を作成します。 詳細については、「 [プロパティ式を追加または変更する](../../integration-services/expressions/add-or-change-a-property-expression.md)」を参照してください。  
  
7.  プロパティ値を更新します。  
  
8.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)   
 [Integration Services コンテナー](../../integration-services/control-flow/integration-services-containers.md)   
 [[制御フロー]](../../integration-services/control-flow/control-flow.md)  
  
  
