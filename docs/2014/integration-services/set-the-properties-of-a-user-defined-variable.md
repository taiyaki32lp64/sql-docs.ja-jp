---
title: ユーザー定義変数のプロパティを設定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- modifying variables
- variables [Integration Services], properties
ms.assetid: f98ddbec-f668-4dba-a768-44ac3ae0536f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: aadfb7b53d22a00bf14699f611f20ce508a7ab5e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055652"
---
# <a name="set-the-properties-of-a-user-defined-variable"></a>ユーザー定義変数のプロパティを設定する
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] でユーザー定義変数のプロパティを設定するには、次の機能のいずれかを使用します。  
  
-   [変数] ウィンドウ。  
  
-   [プロパティ] ウィンドウ。 **[プロパティ]** ウィンドウには、 **[変数]** ウィンドウでは使用できない変数を構成するための次のプロパティが一覧表示されています: Description、EvaluateAsExpression、Expression、ReadOnly、ValueType、IncludeInDebugDump。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、RaiseChangedEvent プロパティを除き、更新できないプロパティを持つ一連のシステム変数もあります。  
  
 **変数に式を設定します。**  
  
 **[プロパティ]** ウィンドウを使用してユーザー定義変数に式を設定する場合:  
  
-   変数の値は、Value プロパティまたは Expression プロパティによって設定できます。 既定では、EvaluateAsExpression プロパティに設定が`False`値プロパティによって変数の値が設定されます。 値を設定する式を使用する必要がありますまず EvaluateAsExpression に設定する`True`、Expression プロパティで式を指定します。 Value プロパティには、自動的に式の評価結果が設定されます。  
  
-   ValueType プロパティには、Value プロパティの値のデータ型が含まれます。 Value が式によって設定される場合、ValueType は、式の評価結果と互換性があるデータ型に自動的に更新されます。 たとえば、値には、0 と ValueType プロパティが含まれている場合に**Int32** 、GETDATE() に式を設定して、値には、現在の日付と時刻が含まれます。 および、ValueType がに設定されている`DateTime`します。  
  
-   変数の **[プロパティ]** ウィンドウからは **[式ビルダー]** ダイアログ ボックスを開くことができます。 このツールを使用すると、式の作成、検証、および評価を行うことができます。 詳しくは、「[式ビルダー](expressions/expression-builder.md)」と「[Integration Services &#40;SSIS&#41; の式](expressions/integration-services-ssis-expressions.md)」をご覧ください。  
  
 **[変数]** ウィンドウを使用してユーザー定義変数に式を設定する場合:  
  
-   変数の値を設定する式を使用して、まず変数のデータ型が、式の評価結果と互換性があることを確認しで式を指定し、`Expression`の列、**変数**ウィンドウ。 EvaluateAsExpression プロパティ、**プロパティ**ウィンドウは自動的に設定`True`します。  
  
-   変数に式を割り当てると、変数の横に特別なアイコン マーカーが表示されます。 この特別なアイコン マーカーは、式が設定されている接続マネージャーおよびタスクの横にも表示されます。  
  
-   変数の **[変数]** ウィンドウからは **[式ビルダー]** ダイアログ ボックスを開くことができます。 このツールを使用すると、式の作成、検証、および評価を行うことができます。 詳しくは、「[式ビルダー](expressions/expression-builder.md)」と「[Integration Services &#40;SSIS&#41; の式](expressions/integration-services-ssis-expressions.md)」をご覧ください。  
  
 両方で、**変数**と**プロパティ**ウィンドウで、変数に式を割り当てる場合および`EvaluateAsExpression`に設定されている`True`、変数のデータ型を変更することはできません。  
  
 **Namespace と名のプロパティの設定**  
  
 `Name` プロパティと `Namespace` プロパティの値の最初の文字は、Unicode Standard 2.0 に定義されているアルファベット文字か、アンダースコア (_) にする必要があります。 2 番目以降の文字では、Unicode Standard 2.0 に定義されている文字または数字と、アンダースコア (\_) を使用できます。  
  
## <a name="using-the-variables-window-to-set-properties"></a>[変数] ウィンドウを使用したプロパティの設定  
  
#### <a name="to-set-the-properties-of-a-variable-by-using-the-variables-window"></a>[変数] ウィンドウを使用して変数のプロパティを設定するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージを右クリックして開きます。  
  
3.  **SSIS** メニューの **[変数]** をクリックします。  
  
     必要に応じて、View.Variables コマンドを **[オプション]** ダイアログ ボックスの **[キーボード]** ページで選択したキーの組み合わせにマップすることによって、 **[変数]** ウィンドウを表示することもできます。  
  
4.  必要に応じて、 **[変数]** ウィンドウで **[グリッドのオプション]** をクリックして、 **[変数]** ウィンドウに表示する列を選択したり、変数の一覧に適用するフィルターを選択したりします。  
  
5.  一覧で、変数を選択し、値を更新し、 `Name`、**データ型**、 `Value`、 `Namespace`、 **Raise Change Event**、**説明、** と`Expression`列。  
  
6.  一覧で変数を選択し、 **[変数の移動]** をクリックしてスコープを変更します。  
  
7.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="using-the-properties-window-to-set-properties"></a>[プロパティ] ウィンドウを使用したプロパティの設定  
  
#### <a name="to-set-the-properties-of-a-variable-by-using-the-properties-window"></a>[プロパティ] ウィンドウを使用して変数のプロパティを設定するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージを右クリックして開きます。  
  
3.  **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックします。  
  
4.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、 **[パッケージ エクスプローラー]** タブをクリックし、[パッケージ] ノードを展開します。  
  
5.  パッケージの適用範囲の変数を変更するには、[変数] ノードを展開します。それ以外の場合は、変更する変数が含まれている [変数] ノードが表示されるまで、[イベント ハンドラー] または [実行可能ファイル] ノードを展開します。  
  
6.  変更するプロパティの変数をクリックします。  
  
7.  **[プロパティ]** ウィンドウで、読み取り/書き込みの変数プロパティを更新します。 ユーザー定義変数の場合は読み取り/読み取りのみのプロパティもあります。  
  
     プロパティの詳細については、「[Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)」を参照してください。  
  
8.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)   
 [パッケージで変数を使用する](../../2014/integration-services/use-variables-in-packages.md)   
 [パッケージ内のユーザー定義変数のスコープの追加、削除、変更](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
  
