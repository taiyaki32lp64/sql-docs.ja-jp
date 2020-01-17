---
title: Excel 変換先エディター ([接続マネージャー] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.exceldestadapter.connection.f1
helpviewer_keywords:
- Excel Destination Editor
ms.assetid: fc13f725-963c-488e-91e2-20627133e842
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c55b9daba7e8e1823e1ced43fc9958d4fe5892ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059237"
---
# <a name="excel-destination-editor-connection-manager-page"></a>[Excel 変換先エディター] ([接続マネージャー] ページ)
  **[Excel 変換先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、データ ソース情報を指定したり、結果をプレビューしたりできます。 Excel 変換先では、 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] ブックのワークシートまたは名前付き範囲にデータが読み込まれます。  
  
> [!NOTE]  
>  `CommandTimeout` Excel 変換先のプロパティでは使用できません、 **Excel 変換先エディター**を使用して設定できますが、**高度なエディター**します。 また、一部の高速読み込みオプションは **[詳細エディター]** でしか使用できません。 これらのプロパティの詳細については、「 [Excel Custom Properties](data-flow/excel-custom-properties.md)」の「Excel 変換先」を参照してください。  
  
 Excel 変換先の詳細については、「 [Excel Destination](data-flow/excel-destination.md)」を参照してください。  
  
## <a name="static-options"></a>静的オプション  
 **Excel 接続マネージャー**  
 既存の Excel 接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[Excel 接続マネージャー]** ダイアログ ボックスを使用して、新しい接続マネージャーを作成します。  
  
 **[データ アクセス モード]**  
 ソースからデータを選択する方法を指定します。  
  
|オプション|説明|  
|------------|-----------------|  
|[テーブルまたはビュー]|Excel データ ソースのワークシートまたは名前付き範囲にデータを読み込みます。|  
|[テーブル名またはビュー名の変数]|ワークシートまたは範囲の名前を変数に指定します。<br /><br /> **関連情報**: [パッケージで変数を使用する](../../2014/integration-services/use-variables-in-packages.md)|  
|[SQL コマンド]|SQL クエリを使用して、Excel 変換先にデータを読み込みます。|  
  
 **[Excel シートの名前]**  
 ドロップダウン リストから Excel 変換先を選択します。 一覧が空の場合は **[新規]** をクリックします。  
  
 **[新規作成]**  
 **[新規]** をクリックすると、 **[テーブルの作成]** ダイアログ ボックスが表示されます。 **[OK]** をクリックすると、 **Excel 接続マネージャー** の参照先の Excel ファイルが作成されます。  
  
 **[既存のデータを表示]**  
 **[クエリ結果のプレビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 プレビューでは、最大で 200 行を表示できます。  
  
> [!WARNING]  
>  選択した **Excel 接続マネージャー** が存在しない Excel ファイルを参照している場合、このボタンをクリックするとエラー メッセージが表示されます。  
  
## <a name="data-access-mode-dynamic-options"></a>データ アクセス モードの動的オプション  
  
### <a name="data-access-mode--table-or-view"></a>[データ アクセス モード] = [テーブルまたはビュー]  
 **[Excel シートの名前]**  
 データ ソースで使用できるワークシートまたは名前付き範囲の名前を一覧から選択します。  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>[データ アクセス モード] = [テーブル名またはビュー名の変数]  
 **[変数名]**  
 ワークシートまたは名前付き範囲の名前が含まれている変数を選択します。  
  
### <a name="data-access-mode--sql-command"></a>[データ アクセス モード] = [SQL コマンド]  
 **[SQL コマンド テキスト]**  
 SQL クエリのテキストを入力し、 **[クエリの作成]** をクリックしてクエリを作成します。または、 **[参照]** をクリックし、クエリ テキストが含まれているファイルを指定します。  
  
 **[クエリの作成]**  
 SQL クエリを視覚的に作成するには、 **[クエリ ビルダー]** ダイアログ ボックスを使用します。  
  
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、SQL クエリのテキストが含まれているファイルを指定します。  
  
 **[クエリの解析]**  
 クエリ テキストの構文を検査します。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [[Excel 変換先エディター] &#40;[マッピング] ページ&#41;](../../2014/integration-services/excel-destination-editor-mappings-page.md)   
 [[Excel 変換先エディター] &#40;[エラー出力] ページ&#41;](../../2014/integration-services/excel-destination-editor-error-output-page.md)   
 [Foreach ループ コンテナーを使用して Excel のファイルおよびテーブルをループ処理する](control-flow/foreach-loop-container.md)  
  
  
