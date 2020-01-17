---
title: 優先順位制約のプロパティを設定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Precedence Constraint Editor dialog box
- precedence constraints [Integration Services], properties
ms.assetid: d990f600-5c09-4cd5-8528-0a58d79dc9f2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bc83e1b636aa03e37717ac62de1a44e9c6f1cfd2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055736"
---
# <a name="set-the-properties-of-a-precedence-constraint"></a>優先順位制約のプロパティを設定する
  優先順位制約のプロパティを設定するには、次のいずれかのツールを使用します。  
  
-   **[優先順位制約エディター]** ダイアログ ボックスを使用します。  
  
-   [プロパティ] ウィンドウを使用します。 [プロパティ] ウィンドウには、 **[優先順位制約エディター]** ダイアログ ボックスでは使用できない優先順位制約を構成するためのプロパティが一覧表示されます。 [プロパティ] ウィンドウでは、優先順位制約の説明と名前を指定し、デザイン画面に表示する優先順位制約の注釈を構成することができます。  
  
 次の手順では、これらの各ツールを使用して優先順位制約のプロパティを設定する方法について説明します。  
  
### <a name="to-set-the-properties-of-a-precedence-constraint-by-using-the-precedence-constraint-editor"></a>[優先順位制約エディター] を使用して優先順位制約のプロパティを設定するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。  
  
4.  優先順位制約をダブルクリックします。  
  
     **[優先順位制約エディター]** が開きます。  
  
5.  **[評価操作]** ドロップダウン リストで、評価操作を選択します。  
  
6.  `Value`ドロップダウン リストで、優先実行可能オブジェクトの実行結果を選択します。  
  
7.  評価操作で式を使用する場合、`Expression`ボックスで、式を入力し、をクリックして**テスト**式を評価します。  
  
    > [!NOTE]  
    >  変数名の大文字と小文字は区別されます。  
  
8.  複数のタスクまたはコンテナーが制約付き実行可能ファイルに接続されている場合は、選択**論理的かつ**に上記すべての実行可能ファイルの実行結果を評価する必要がありますを指定する`true`します。 選択**論理和**に 1 つだけの実行結果を評価する必要がありますを指定する`true`します。  
  
9. **[OK]** をクリックし、 **[優先順位制約エディター]** を閉じます。  
  
10. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="to-set-the-properties-of-a-precedence-constraint-by-using-the-properties-window"></a>[プロパティ] ウィンドウを使用して優先順位制約のプロパティを設定するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、変更するパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。 **[制御フロー]** タブのデザイン画面で優先順位制約を右クリックし、 **[プロパティ]** をクリックします。 [プロパティ] ウィンドウで、プロパティの値を変更します。  
  
4.  **[プロパティ]** ウィンドウで、優先順位制約の次の読み取り/書き込みプロパティを設定します。  
  
    |読み取り/書き込みプロパティ|構成アクション|  
    |--------------------------|--------------------------|  
    |説明|説明を指定します。|  
    |EvalOp|評価操作を選択します。 場合、 `Expression`、 **ExpressionAndConstant**、または**ExpressionOrConstant**操作が選択した場合、式を指定することができます。|  
    |式|評価操作に and 式が含まれる場合は、式を指定します。 式はブール値に評価される必要があります。 式言語の詳細については、「[Integration Services &#40;SSIS&#41; 式](expressions/integration-services-ssis-expressions.md)」をご覧ください。|  
    |LogicalAnd|設定`LogicalAnd`複数実行可能ファイルの直前および制約付き実行可能ファイルにリンクしているときに、その他の優先順位制約と組み合わせて、優先順位制約を評価するかどうかを指定するには|  
    |名前|優先順位制約の名前を更新します。|  
    |ShowAnnotation|使用する注釈の種類を指定します。 注釈を無効にするには **[Never]** 、要求時に注釈を有効にするには **[AsNeeded]** 、Name プロパティの値を使用して注釈を自動的に設定するには **[ConstraintName]** 、Description プロパティの値を使用して注釈を自動的に設定するには **[ConstraintDescription]** 、Value プロパティと Expression プロパティの値を使用して注釈を自動的に設定するには **[ConstraintOptions]** をそれぞれ選択します。|  
    |値|EvalOP プロパティで指定された評価操作に制約が含まれる場合は、制約付き実行可能ファイルの実行結果を選択します。|  
  
5.  [プロパティ] ウィンドウを閉じます。  
  
6.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [優先順位制約](control-flow/precedence-constraints.md)   
 [既定の優先順位制約を使用してタスクとコンテナーを連結する](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [ショートカット メニューを使用して、優先順位制約の値を設定します。](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [優先順位制約で式を使用する](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
  
