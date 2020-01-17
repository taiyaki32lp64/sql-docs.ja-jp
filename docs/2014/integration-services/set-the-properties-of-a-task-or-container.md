---
title: タスクまたはコンテナーのプロパティを設定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], properties
ms.assetid: 52d47ca4-fb8c-493d-8b2b-48bb269f859b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 05e98e0a735cc54e129b82c65841c6db688953de
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055670"
---
# <a name="set-the-properties-of-a-task-or-container"></a>タスクまたはコンテナーのプロパティを設定する
  タスクおよびコンテナーのほとんどのプロパティは、 **[プロパティ]** ウィンドウを使用して設定できます。 例外は、タスク コレクションのプロパティと、 **[プロパティ]** ウィンドウを使用して設定するには複雑すぎるプロパティです。 たとえば、Foreach ループ コンテナーが使用する列挙子を **[プロパティ]** ウィンドウで構成することはできません。 これらの複雑なプロパティを設定するには、タスク エディターまたはコンテナー エディターを使用する必要があります。 ほとんどの場合、タスク エディターとコンテナー エディターには複数のノードがあり、各ノードには関連プロパティが含まれています。 ノードの名前は、ノードに含まれるプロパティの対象を示します。  
  
 次の手順では、 **[プロパティ]** ウィンドウを使用するか、対応するタスク エディターまたはコンテナー エディターを使用してタスクまたはコンテナーのプロパティを設定する方法を説明します。  
  
### <a name="to-set-the-properties-of-a-task-or-container-by-using-the-properties-window"></a>[プロパティ] ウィンドウを使用してタスクまたはコンテナーのプロパティを設定するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。  
  
4.  **[制御フロー]** タブのデザイン画面でタスクまたはコンテナーを右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[プロパティ]** ウィンドウで、プロパティの値を更新します。  
  
    > [!NOTE]  
    >  ほとんどのプロパティは、テキスト ボックスに値を直接入力するか、一覧から値を選択することによって設定できます。 ただし、カスタムのプロパティ エディターが用意されている複雑なプロパティもあります。 このプロパティを設定するには、テキスト ボックス内をクリックしてから、作成ボタン ( **[...]** ) をクリックしてカスタム エディターを開きます。  
  
6.  必要に応じて、タスクまたはコンテナーのプロパティを動的に更新するプロパティ式を作成します。 詳細については、「 [プロパティ式を追加または変更する](expressions/add-or-change-a-property-expression.md)」を参照してください。  
  
7.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="to-set-the-properties-of-a-task-or-container-by-using-a-task-or-container-editor"></a>タスク エディターまたはコンテナー エディターを使用してタスクまたはコンテナーのプロパティを設定するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。  
  
4.  **[制御フロー]** タブのデザイン画面でタスクまたはコンテナーを右クリックし、ショートカット メニューの **[編集]** をクリックして、対応するタスク エディターまたはコンテナー エディターを開きます。  
  
     For ループ コンテナーの構成方法については、「 [Configure a For Loop Container](control-flow/for-loop-container.md)」(For ループ コンテナーを構成する) を参照してください。  
  
     Foreach ループ コンテナーの構成方法については、「 [Configure a Foreach Loop Container](control-flow/foreach-loop-container.md)」(Foreach ループ コンテナーを構成する) を参照してください。  
  
    > [!NOTE]  
    >  シーケンス コンテナーには、カスタム エディターはありません。  
  
5.  タスク エディターまたはコンテナー エディターに複数のノードがある場合、設定するプロパティが含まれるノードをクリックします。  
  
6.  必要に応じて **[式]** をクリックし、 **[式]** ページで、タスクまたはコンテナーのプロパティを動的に更新するプロパティ式を作成します。 詳細については、「 [プロパティ式を追加または変更する](expressions/add-or-change-a-property-expression.md)」を参照してください。  
  
7.  プロパティ値を更新します。  
  
8.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services タスク](control-flow/integration-services-tasks.md)   
 [Integration Services コンテナー](control-flow/integration-services-containers.md)  
  
  
