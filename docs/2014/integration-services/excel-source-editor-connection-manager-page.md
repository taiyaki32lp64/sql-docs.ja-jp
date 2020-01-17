---
title: Excel ソース エディター (接続マネージャー ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.excelsourceadapter.connection.f1
helpviewer_keywords:
- Excel Source Editor
ms.assetid: 428e04e0-ad98-45d0-8345-12ec1b67b2eb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c3132bd65bb6f3092cc950758d4f346b5c4cd8fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059166"
---
# <a name="excel-source-editor-connection-manager-page"></a>[Excel ソース エディター] ([接続マネージャー] ページ)
  **[Excel ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ノードを使用すると、変換元として [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] ブックを選択して使用できます。 Excel ソースは、既存のブックのワークシートまたは名前付き範囲からデータを読み取ります。  
  
> [!NOTE]  
>  `CommandTimeout`の Excel ソースのプロパティでは使用できません、 **Excel ソース エディター**を使用して設定できますが、**高度なエディター**します。 このプロパティの詳細については、「 [Excel のカスタム プロパティ](data-flow/excel-custom-properties.md)」 の Excel ソースのセクションを参照してください。  
  
 Excel ソースの詳細については、「 [Excel Source](data-flow/excel-source.md)」を参照してください。  
  
## <a name="static-options"></a>静的オプション  
 **[キャッシュなし]**  
 既存の Excel 接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[Excel 接続マネージャー]** ダイアログ ボックスを使用して、新しい接続マネージャーを作成します。  
  
 **[データ アクセス モード]**  
 ソースからデータを選択する方法を指定します。  
  
|値|説明|  
|-----------|-----------------|  
|[テーブルまたはビュー]|Excel ファイルのワークシートまたは名前付き範囲からデータを取得します。|  
|[テーブル名またはビュー名の変数]|ワークシートまたは範囲の名前を変数に指定します。<br /><br /> **関連情報**: [パッケージで変数を使用する](../../2014/integration-services/use-variables-in-packages.md)|  
|[SQL コマンド]|SQL クエリを使用して、Excel ファイルからデータを取得します。 クエリ構文の詳細については、「 [Excel ソース](data-flow/excel-source.md)」を参照してください。|  
|[変数からの SQL コマンド]|SQL クエリ テキストを変数で指定します。|  
  
 **プレビュー**  
 **[データ ビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 プレビューでは、最大で 200 行を表示できます。  
  
## <a name="data-access-mode-dynamic-options"></a>データ アクセス モードの動的オプション  
  
### <a name="data-access-mode--table-or-view"></a>[データ アクセス モード] = [テーブルまたはビュー]  
 **[Excel シートの名前]**  
 Excel ブックで使用できるワークシートまたは名前付き範囲の名前を一覧から選択します。  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>[データ アクセス モード] = [テーブル名またはビュー名の変数]  
 **[変数名]**  
 ワークシートまたは名前付き範囲の名前が含まれている変数を選択します。  
  
### <a name="data-access-mode--sql-command"></a>[データ アクセス モード] = [SQL コマンド]  
 **[SQL コマンド テキスト]**  
 SQL クエリのテキストを入力し、 **[クエリの作成]** をクリックしてクエリを作成します。または、 **[参照]** をクリックし、クエリ テキストが含まれているファイルを参照します。  
  
 **パラメーター**  
 クエリ テキスト内でパラメーターのプレースホルダーとして "?" を使用することにより、 パラメーター化クエリを入力した場合は、 **[クエリ パラメーターの設定]** ダイアログ ボックスを使用して、クエリ入力パラメーターをパッケージ変数にマップします。  
  
 **Build query**  
 SQL クエリを視覚的に作成するには、 **[クエリ ビルダー]** ダイアログ ボックスを使用します。  
  
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、SQL クエリのテキストが含まれているファイルを指定します。  
  
 **[クエリの解析]**  
 クエリ テキストの構文を検査します。  
  
### <a name="data-access-mode--sql-command-from-variable"></a>データ アクセス モードが [変数からの SQL コマンド] の場合  
 **[変数名]**  
 SQL クエリのテキストを含む変数を選択します。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [[Excel ソース エディター] ([列] ページ)](../../2014/integration-services/excel-source-editor-columns-page.md)   
 [[Excel ソース エディター] ([エラー出力] ページ)](../../2014/integration-services/excel-source-editor-error-output-page.md)   
 [Excel 接続マネージャー](connection-manager/excel-connection-manager.md)   
 [Foreach ループ コンテナーを使用して Excel のファイルおよびテーブルをループ処理する](control-flow/foreach-loop-container.md)  
  
  
