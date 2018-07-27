---
title: CDC ソース エディター (接続マネージャー ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.connection.f1
ms.assetid: 304e6717-e160-4a7b-a06f-32182449fef8
caps.latest.revision: 9
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1e78f64882c002e8bb9f7ae2a2f424ac7367fd89
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37300558"
---
# <a name="cdc-source-editor-connection-manager-page"></a>[CDC ソース エディター] ([接続マネージャー] ページ)
  **[CDC ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、CDC ソースが変更行を読み取る [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] データベース (CDC データベース) の ADO.NET 接続マネージャーを選択できます。 CDC データベースを選択した後で、キャプチャされたテーブルをデータベースで選択する必要があります。  
  
 CDC ソースの詳細については、「 [CDC ソース](data-flow/cdc-source.md)」を参照してください。  
  
## <a name="task-list"></a>タスク一覧  
 **[CDC ソース エディター] の [接続マネージャー] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]で、CDC ソースを含む [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、CDC ソースをダブルクリックします。  
  
3.  **[CDC ソース エディター]** で、 **[接続マネージャー]** をクリックします。  
  
## <a name="options"></a>および  
 **ADO.NET 接続マネージャー**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。 選択した変更テーブルが存在する、CDC に対応した [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースへの接続である必要があります。  
  
 **[新規作成]**  
 **[新規]** をクリックします。 新しい接続マネージャーを作成できる **[ADO.NET 接続マネージャーの構成エディター]** ダイアログ ボックスが開きます。  
  
 **[CDC テーブル]**  
 読み取って、処理のために下流の SSIS コンポーネントに渡す、キャプチャされた変更の含まれる CDC ソース テーブルを選択します。  
  
 **[キャプチャ インスタンス]**  
 読み取る CDC テーブルの CDC キャプチャ インスタンスの名前を選択または入力します。  
  
 キャプチャされたソース テーブルには、スキーマの変更によりテーブル定義のシームレスな遷移を処理するためのキャプチャされたインスタンスが 1 ～ 2 個含まれることがあります。 キャプチャ対象のソース テーブルに複数のキャプチャ インスタンスが定義されている場合は、ここで使用するキャプチャ インスタンスを選択してください。 [スキーマ].[テーブル] という形式のテーブルの既定のキャプチャ インスタンス名は \<スキーマ>_\<テーブル> ですが、使用される実際のキャプチャ インスタンス名は異なる可能性があります。 読み取り元の実際のテーブルは、**cdc .\<キャプチャ インスタンス>_CT** という形式の CDC テーブルです。  
  
 **[CDC 処理モード]**  
 処理上のニーズに最も適した処理モードを選択します。 オプションは次のとおりです。  
  
-   **[すべて]**: **[更新前]** の値なしで、現在の CDC 範囲内の変更を返します。  
  
-   **[古い値を含むすべて]**: 古い値 (**[更新前]**) を含め、現在の CDC 処理範囲内の変更を返します。 更新操作ごとに、2 つの行 (更新前の値の行と更新後の値の行) が存在することになります。  
  
-   **[差分]**: 現在の CDC 処理範囲内で変更された、ソース行あたり 1 つの変更行のみを返します。 ソース行が複数回更新された場合は、変更が結合されたうえで生成されます (たとえば、挿入と更新が 1 回の更新として、または更新と削除が 1 回の削除として、結合されたうえで生成されることがあります)。 [差分] 変更処理モードで作業する場合は、1 つのソース行が複数の出力に出現するため、変更を削除、挿入、および更新の各出力に分割し、並行処理することができます。  
  
-   **[更新マスクを含む差分]**: このモードは通常の [差分] モードと似ていますが、**__$\<column-name>\__Changed** という名前のパターンを持つブール型の列も追加されます。これは、現在の変更行の変更された列を示します。  
  
-   **[結合を含む差分]**: このモードは通常の [結合] モードと似ていますが、挿入操作と更新操作が 1 つの結合操作 (UPSERT) に結合されます。  
  
> [!NOTE]  
>  どの差分変更オプションを使用する場合も、ソース テーブルに主キーまたは一意のインデックスが必要です。 主キーまたは一意のインデックスがないテーブルに対しては、 **[すべて]** オプションを使用する必要があります。  
  
 **[CDC 状態を含む変数]**  
 現在の CDC コンテキストの CDC 状態を保持する SSIS 文字列パッケージ変数を選択します。 CDC 状態変数の詳細については、「 [状態変数の定義](data-flow/define-a-state-variable.md)」を参照してください。  
  
 **[再処理インジケーター列を含める]**  
 **__$reprocessing**という特別な出力列を作成する場合は、このチェック ボックスをオンにします。  
  
 CDC 処理範囲が初期処理範囲 (初期読み込みの期間に対応する LSN の範囲) と重なる場合か、CDC 処理範囲が前の実行でのエラーの後に再処理される場合、この列の値は **true** になります。 このインジケーター列を使用すると、SSIS 開発者は変更を再処理するときに、エラーを別々に処理できます (たとえば、非既存行の削除やキーの重複により失敗した挿入などの操作を無視できます)。  
  
 詳細については、「 [CDC ソースのカスタム プロパティ](data-flow/cdc-source-custom-properties.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [[CDC ソース エディター&#40;列] ページ&#41;](../../2014/integration-services/cdc-source-editor-columns-page.md)   
 [[CDC ソース エディター&#40;エラー出力] ページ&#41;](../../2014/integration-services/cdc-source-editor-error-output-page.md)  
  
  