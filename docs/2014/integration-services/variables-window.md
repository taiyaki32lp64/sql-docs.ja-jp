---
title: '[変数] ウィンドウ | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.variables.f1
helpviewer_keywords:
- Variables Window dialog box
ms.assetid: f405e5ce-ef69-4c58-8c7d-a3d44dfe9ab0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 62dd9af9ea66678c2cc69a016b83e907025a4294
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62877877"
---
# <a name="variables-window"></a>[変数] ウィンドウ
  **[変数]** ウィンドウを使用すると、ユーザー定義変数を作成、変更し、システム変数を表示できます。  
  
 既定では、 **[変数]** ウィンドウは **の SSIS デザイナーの** [接続マネージャー] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]領域の下にあります。 **[変数]** ウィンドウが表示されない場合は、 **[SSIS]** メニューの **[変数]** をクリックして、ウィンドウを表示します。  
  
 必要に応じて、View.Variables コマンドを **[オプション]** ダイアログ ボックスの **[キーボード]** ページで選択したキーの組み合わせにマップすることによって、 **[変数]** ウィンドウを表示することもできます。  
  
> [!NOTE]
>  `Name` プロパティと `Namespace` プロパティの値の最初の文字は、Unicode Standard 2.0 に定義されているアルファベット文字か、アンダースコア (_) にする必要があります。 2 番目以降の文字では、Unicode Standard 2.0 に定義されている文字または数字と、アンダースコア (\_) を使用できます。  
  
## <a name="options"></a>および  
 **[変数の追加]**  
 ユーザー定義変数を追加します。  
  
 **変数の移動**  
 一覧で変数をクリックし、 **[変数の移動]** をクリックして変数のスコープを変更します。 **[新しいスコープの選択]** ダイアログ ボックスで、パッケージまたはパッケージ内のコンテナー、タスク、またはイベント ハンドラーを選択して、変数のスコープを変更します。  
  
 変数のスコープの詳細については、「 [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)領域の下にあります。  
  
 **変数の削除**  
 変数を一覧から選択し、 **[変数の削除]** をクリックします。  
  
 **グリッドのオプション**  
 クリックすると **[可変グリッドのオプション]** ダイアログ ボックスが開きます。このダイアログ ボックスで、列の選択を変更したり、 **[変数]** ウィンドウにフィルターを適用したりできます。 詳細については、「 [可変グリッドのオプション](../../2014/integration-services/variable-grid-options.md)」を参照してください。  
  
 `Name`  
 変数名を表示します。 ユーザー定義変数の名前を更新できます。  
  
 **Scope**  
 変数のスコープを表示します。 変数には、パッケージ全体のスコープまたはコンテナーやタスクのスコープがあります。 変数のスコープは、変数の値の読み取りや設定を必要とする他のタスクやコンポーネントからアクセスできるように十分な範囲を指定する必要があります。  
  
 スコープを変更するには、変数をクリックして **[変数]** ウィンドウの **[変数の移動]** をクリックします。  
  
 **[データ型]**  
 変数のデータ型が表示されます。 一覧からユーザー定義変数のデータ型を選択できます。  
  
> [!NOTE]  
>  変数に式を割り当てる場合は、データ型を変更できません。  
  
 **[値]**  
 変数の値を表示します。 ユーザー定義変数の値を更新できます。 この値は、リテラルまたは式にすることができます。また、複数行の文字列にすることもできます。 変数に式を割り当てるには、 **[変数]** ウィンドウの **[式]** 列の横にある参照ボタンをクリックします。  
  
 `Namespace`  
 名前空間名を表示します。 ユーザー定義変数は最初に作成、**ユーザー**で名前空間の名前を変更できますが名前空間、`Namespace`フィールド。 この列を表示するには、 **[グリッドのオプション]** をクリックします。  
  
 **[Raise Change Event]**  
 値を変更した場合に `OnVariableValueChanged` イベントを発生させるかどうかを示します。 ユーザー定義変数およびシステム変数の値を更新できます。 既定では、 **[変数]** ウィンドウにこの列は表示されません。 この列を表示するには、 **[グリッドのオプション]** をクリックします。  
  
 **[説明]**  
 変数の説明を表示します。 ユーザー定義変数の説明を変更できます。 既定では、 **[変数]** ウィンドウにこの列は表示されません。 この列を表示するには、 **[グリッドのオプション]** をクリックします。  
  
 **[変数]**  
 変数に割り当てられた式を表示します。 式を割り当てるには、参照ボタンをクリックします。  
  
 変数に式を割り当てると、変数の横に特別なアイコン マーカーが表示されます。 この特別なアイコン マーカーは、式が設定されている接続マネージャーおよびタスクの横にも表示されます。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)   
 [パッケージで変数を使用する](../../2014/integration-services/use-variables-in-packages.md)   
 [Integration Services &#40;SSIS&#41; の式](expressions/integration-services-ssis-expressions.md)   
 [パッケージ実行用のダンプ ファイルを生成する](troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
