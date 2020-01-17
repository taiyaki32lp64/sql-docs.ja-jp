---
title: Excel ソース | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.excelsource.f1
- sql13.dts.designer.excelsourceadapter.connection.f1
- sql13.dts.designer.excelsourceadapter.columns.f1
- sql13.dts.designer.excelsourceadapter.erroroutput.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 38af7d056eab840a5cf83eefa96ec2731e58bc67
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292769"
---
# <a name="excel-source"></a>Excel ソース

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Excel ソースは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel ブック内のワークシートまたは範囲からデータを抽出します。  

> [!IMPORTANT]
> Excel ファイルへの接続、および Excel から、または Excel へのデータの読み込みに関する制限事項と既知の問題については、「[Load data from or to Excel with SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)」 (SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む) を参照してください。

## <a name="access-modes"></a>アクセス モード
 Excel ソースでは、データを抽出するために、次の 4 つの異なるデータ アクセス モードが用意されています。  
  
-   テーブルまたはビュー。  
  
-   変数で指定されたテーブルまたはビュー。  
  
-   SQL ステートメントの結果。 クエリにはパラメーター化クエリを使用できます。  
  
-   変数に格納された SQL ステートメントの結果。  
  
 Excel ソースは、Excel 接続マネージャーを使用してデータ ソースに接続します。Excel 接続マネージャーでは、使用する Excel ブック ファイルを指定します。 詳しくは、「 [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md)」をご覧ください。  
  
 Excel ソースは、1 つの標準出力と 1 つのエラー出力をとります。  
  
## <a name="excel-source-configuration"></a>Excel ソースの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるすべてのプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Excel のカスタム プロパティ](../../integration-services/data-flow/excel-custom-properties.md)  
  
 Excel ファイルのグループによるループ処理については、「 [Foreach ループ コンテナーを使用して Excel のファイルおよびテーブルをループ処理する](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)」をご覧ください。  
  
## <a name="excel-source-editor-connection-manager-page"></a>[Excel ソース エディター] ([接続マネージャー] ページ)
  **[Excel ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ノードを使用すると、変換元として [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] ブックを選択して使用できます。 Excel ソースは、既存のブックのワークシートまたは名前付き範囲からデータを読み取ります。  
  
> [!NOTE]  
>  Excel ソースの **CommandTimeout** プロパティは **[Excel ソース エディター]** ではアクセスできませんが、 **[詳細エディター]** を使用して設定できます。 このプロパティの詳細については、「 [Excel のカスタム プロパティ](../../integration-services/data-flow/excel-custom-properties.md)」 の Excel ソースのセクションを参照してください。  
  
### <a name="static-options"></a>静的オプション  
 **[キャッシュなし]**  
 既存の Excel 接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[Excel 接続マネージャー]** ダイアログ ボックスを使用して、新しい接続マネージャーを作成します。  
  
 **[データ アクセス モード]**  
 ソースからデータを選択する方法を指定します。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|[テーブルまたはビュー]|Excel ファイルのワークシートまたは名前付き範囲からデータを取得します。|  
|[テーブル名またはビュー名の変数]|ワークシートまたは範囲の名前を変数に指定します。<br /><br /> **関連情報**: [パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|[SQL コマンド]|SQL クエリを使用して、Excel ファイルからデータを取得します。 |  
|[変数からの SQL コマンド]|SQL クエリ テキストを変数で指定します。|  
  
 **プレビュー**  
 **[データ ビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 プレビューでは、最大で 200 行を表示できます。  
  
### <a name="data-access-mode-dynamic-options"></a>データ アクセス モードの動的オプション  
  
#### <a name="data-access-mode--table-or-view"></a>[データ アクセス モード] = [テーブルまたはビュー]  
 **[Excel シートの名前]**  
 Excel ブックで使用できるワークシートまたは名前付き範囲の名前を一覧から選択します。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>[データ アクセス モード] = [テーブル名またはビュー名の変数]  
 **[変数名]**  
 ワークシートまたは名前付き範囲の名前が含まれている変数を選択します。  
  
#### <a name="data-access-mode--sql-command"></a>[データ アクセス モード] = [SQL コマンド]  
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
  
#### <a name="data-access-mode--sql-command-from-variable"></a>データ アクセス モードが [変数からの SQL コマンド] の場合  
 **[変数名]**  
 SQL クエリのテキストを含む変数を選択します。  
  
## <a name="excel-source-editor-columns-page"></a>[Excel ソース エディター] ([列] ページ)
  **[Excel ソース エディター]** ダイアログ ボックスの **[列]** ページを使用すると、出力列をそれぞれの外部 (変換元) 列にマップできます。  
  
### <a name="options"></a>オプション  
 **使用できる外部列**  
 データ ソース内の使用できる外部列の一覧を表示します。 このテーブルを使用して列を追加または削除することはできません。  
  
 **[外部列]**  
 タスクで外部 (変換元) 列を読み取る順序を表示します。 この順序を変更するには、最初に上記のテーブル内で選択されている列を選択解除してから、一覧から外部列を別の順で選択します。  
  
 **出力列**  
 各出力列の一意な名前を表示します。 既定では選択された外部 (変換元) 列の名前になりますが、一意でわかりやすい名前を付けることもできます。 指定された名前は、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーに表示されます。  
  
## <a name="excel-source-editor-error-output-page"></a>[Excel ソース エディター] ([エラー出力] ページ)
  **[Excel ソース エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、エラー処理オプションを選択したり、エラー出力列のプロパティを設定したりできます。  
  
### <a name="options"></a>オプション  
 **入力または出力**  
 データ ソースの名前を表示します。  
  
 **列**  
 **[Excel ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ページで選択した外部 (変換元) 列を表示します。  
  
 **Error**  
 エラーが発生した場合に、障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **関連項目:** [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **切り捨て**  
 切り捨てが発生したときの処理方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を指定します。  
  
 **[説明]**  
 エラーの説明を表示します。  
  
 **[選択したセルに設定する値]**  
 エラーまたは切り捨てが発生した場合に、選択したすべてのセルに対して障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **[適用]**  
 選択したセルにエラー処理オプションを適用します。  
  
## <a name="related-content"></a>関連コンテンツ  
[SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む](../load-data-to-from-excel-with-ssis.md)  
[Excel 変換先](excel-destination.md)  
[Excel 接続マネージャー](../connection-manager/excel-connection-manager.md)
