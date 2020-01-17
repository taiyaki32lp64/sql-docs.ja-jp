---
title: '[変数] ウィンドウ | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.variables.f1
- sql13.dts.designer.variableoptionswindow.f1
helpviewer_keywords:
- Variables Window dialog box
ms.assetid: f405e5ce-ef69-4c58-8c7d-a3d44dfe9ab0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ef2e4b408dabf7b054465149b2489e07fbdefef8
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295026"
---
# <a name="variables-window"></a>[変数] ウィンドウ

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **[変数]** ウィンドウを使用すると、ユーザー定義変数を作成、変更し、システム変数を表示できます。  
  
 既定では、 **[変数]** ウィンドウは **の SSIS デザイナーの** [接続マネージャー] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]領域の下にあります。 **[変数]** ウィンドウが表示されない場合は、 **[SSIS]** メニューの **[変数]** をクリックして、ウィンドウを表示します。  
  
 必要に応じて、View.Variables コマンドを **[オプション]** ダイアログ ボックスの **[キーボード]** ページで選択したキーの組み合わせにマップすることによって、 **[変数]** ウィンドウを表示することもできます。  
  
> [!NOTE]
>  **Name** プロパティと **Namespace** プロパティの値の最初の文字は、Unicode Standard 2.0 に定義されているアルファベット文字か、アンダースコア (_) にする必要があります。 2 番目以降の文字では、Unicode Standard 2.0 に定義されている文字または数字と、アンダースコア (\_) を使用できます。  
  
## <a name="options"></a>オプション  
 **[変数の追加]**  
 ユーザー定義変数を追加します。  
  
 **変数の移動**  
 一覧で変数をクリックし、 **[変数の移動]** をクリックして変数のスコープを変更します。 **[新しいスコープの選択]** ダイアログ ボックスで、パッケージまたはパッケージ内のコンテナー、タスク、またはイベント ハンドラーを選択して、変数のスコープを変更します。  
  
 変数のスコープの詳細については、「 [Integration Services &#40;SSIS&#41; の変数](../integration-services/integration-services-ssis-variables.md)領域の下にあります。  
  
 **変数の削除**  
 変数を一覧から選択し、 **[変数の削除]** をクリックします。  
  
 **グリッドのオプション**  
 クリックすると **[可変グリッドのオプション]** ダイアログ ボックスが開きます。このダイアログ ボックスで、列の選択を変更したり、 **[変数]** ウィンドウにフィルターを適用したりできます。 詳細については、「 [可変グリッドのオプション](../integration-services/variable-grid-options.md)」を参照してください。  
  
 **Name**  
 変数名を表示します。 ユーザー定義変数の名前を更新できます。  
  
 **スコープ**  
 変数のスコープを表示します。 変数には、パッケージ全体のスコープまたはコンテナーやタスクのスコープがあります。 変数のスコープは、変数の値の読み取りや設定を必要とする他のタスクやコンポーネントからアクセスできるように十分な範囲を指定する必要があります。  
  
 スコープを変更するには、変数をクリックして **[変数]** ウィンドウの **[変数の移動]** をクリックします。  
  
 **[データ型]**  
 変数のデータ型が表示されます。 一覧からユーザー定義変数のデータ型を選択できます。  
  
> [!NOTE]  
>  変数に式を割り当てる場合は、データ型を変更できません。  
  
 **Value**  
 変数の値を表示します。 ユーザー定義変数の値を更新できます。 この値は、リテラルまたは式にすることができます。また、複数行の文字列にすることもできます。 変数に式を割り当てるには、 **[変数]** ウィンドウの **[式]** 列の横にある参照ボタンをクリックします。  
  
 **Namespace**  
 名前空間名を表示します。 ユーザー定義変数は、最初に **ユーザー** 名前空間で作成されますが、 **[名前空間]** フィールドで名前空間名を変更できます。 この列を表示するには、 **[グリッドのオプション]** をクリックします。  
  
 **[Raise Change Event]**  
 値を変更した場合に **OnVariableValueChanged** イベントを発生させるかどうかを示します。 ユーザー定義変数およびシステム変数の値を更新できます。 既定では、 **[変数]** ウィンドウにこの列は表示されません。 この列を表示するには、 **[グリッドのオプション]** をクリックします。  
  
 **[説明]**  
 変数の説明を表示します。 ユーザー定義変数の説明を変更できます。 既定では、 **[変数]** ウィンドウにこの列は表示されません。 この列を表示するには、 **[グリッドのオプション]** をクリックします。  
  
 **[変数]**  
 変数に割り当てられた式を表示します。 式を割り当てるには、参照ボタンをクリックします。  
  
 変数に式を割り当てると、変数の横に特別なアイコン マーカーが表示されます。 この特別なアイコン マーカーは、式が設定されている接続マネージャーおよびタスクの横にも表示されます。  

## <a name="variable-grid-options-dialog-box"></a>[可変グリッドのオプション] ダイアログ ボックス
 **[可変グリッドのオプション]** ダイアログ ボックスを使用して、 **[変数]** ウィンドウに表示される列を選択したり、変数の一覧に適用するフィルターを選択したりします。 対応する変数のプロパティの詳細については、「 [Integration Services (SSIS) の変数](../integration-services/integration-services-ssis-variables.md)」を参照してください。  
  
### <a name="options-for-filter"></a>フィルターのオプション  
 **システム変数を表示する**  
 選択すると、 **[変数]** ウィンドウにシステム変数が一覧表示されます。 システム変数は定義済みです。 システム変数は追加も削除もできません。 **RaiseChangedEvent** プロパティ設定を変更できます。  
  
 この一覧は色分け表示されています。 システム変数は灰色で、ユーザー定義変数は黒です。  
  
 **すべてのスコープの変数を表示する**  
 選択すると、パッケージのスコープ内の変数、および、パッケージにあるコンテナー、タスク、およびイベント ハンドラーのスコープ内の変数が表示されます。 このオプションをオフにすると、パッケージのスコープ内の変数、および、選択されたコンテナー、タスク、またはイベント ハンドラーのスコープ内の変数のみが表示されます。  
  
 変数のスコープの詳細については、「 [Integration Services (SSIS) の変数](../integration-services/integration-services-ssis-variables.md)」を参照してください。  
  
### <a name="options-for-columns"></a>列のオプション  
 **[変数]** ウィンドウに表示する列を選択します。  
  
-   **スコープ**  
  
-   **Data type**  
  
-   **Value**  
  
-   **Namespace**  
  
-   **[変数値の変化時にイベントを発生]**  
  
-   **[説明]**  
  
-   **[式]**  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; の変数](../integration-services/integration-services-ssis-variables.md)   
 [パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)   
 [Integration Services &#40;SSIS&#41; の式](../integration-services/expressions/integration-services-ssis-expressions.md)   
 [パッケージ実行用のダンプ ファイルを生成する](../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
