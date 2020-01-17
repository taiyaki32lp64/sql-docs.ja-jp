---
title: Excel 変換先 | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.exceldest.f1
- sql13.dts.designer.exceldestadapter.connection.f1
- sql13.dts.designer.exceldestadapter.mappings.f1
- sql13.dts.designer.exceldestadapter.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 418d3c214f667807df997902f97bfa271c8c4742
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292817"
---
# <a name="excel-destination"></a>Excel 変換先

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Excel 変換先は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel ブックのワークシートまたは範囲にデータを読み込みます。  

> [!IMPORTANT]
> Excel ファイルへの接続、および Excel から、または Excel へのデータの読み込みに関する制限事項と既知の問題については、「[Load data from or to Excel with SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)」 (SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む) を参照してください。
  
## <a name="access-modes"></a>アクセス モード  
 Excel 変換先には、データを読み込むために、次の 3 つの異なるデータ アクセス モードが用意されています。  
  
-   テーブルまたはビュー。  
  
-   変数で指定されたテーブルまたはビュー。  
  
-   SQL ステートメントの結果。 クエリにはパラメーター化クエリを使用できます。  
  
## <a name="configure-the-excel-destination"></a>Excel 変換先の構成  
 Excel 変換先は、Excel 接続マネージャーを使用してデータ ソースに接続します。Excel 接続マネージャーでは、使用する Excel ブック ファイルを指定します。 詳しくは、「 [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md)」をご覧ください。  
  
 Excel 変換先は、1 つの標準入力と 1 つのエラー出力をとります。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるすべてのプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Excel のカスタム プロパティ](../../integration-services/data-flow/excel-custom-properties.md)  
  
 プロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="excel-destination-editor-connection-manager-page"></a>[Excel 変換先エディター] ([接続マネージャー] ページ)
  **[Excel 変換先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、データ ソース情報を指定したり、結果をプレビューしたりできます。 Excel 変換先では、 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] ブックのワークシートまたは名前付き範囲にデータが読み込まれます。  
  
> [!NOTE]  
>  Excel 変換先の **CommandTimeout** プロパティは、 **[Excel 変換先エディター]** ではアクセスできませんが、 **[詳細エディター]** を使用して設定できます。 また、一部の高速読み込みオプションは **[詳細エディター]** でしか使用できません。 これらのプロパティの詳細については、「 [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md)」の「Excel 変換先」を参照してください。  
  
### <a name="static-options"></a>静的オプション  
 **Excel 接続マネージャー**  
 既存の Excel 接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[Excel 接続マネージャー]** ダイアログ ボックスを使用して、新しい接続マネージャーを作成します。  
  
 **[データ アクセス モード]**  
 ソースからデータを選択する方法を指定します。  
  
|オプション|[説明]|  
|------------|-----------------|  
|[テーブルまたはビュー]|Excel データ ソースのワークシートまたは名前付き範囲にデータを読み込みます。|  
|[テーブル名またはビュー名の変数]|ワークシートまたは範囲の名前を変数に指定します。<br /><br /> **関連情報**: [パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|[SQL コマンド]|SQL クエリを使用して、Excel 変換先にデータを読み込みます。|  
  
 **[Excel シートの名前]**  
 ドロップダウン リストから Excel 変換先を選択します。 一覧が空の場合は **[新規]** をクリックします。  
  
 **[新規作成]**  
 **[新規]** をクリックすると、 **[テーブルの作成]** ダイアログ ボックスが表示されます。 **[OK]** をクリックすると、 **Excel 接続マネージャー** の参照先の Excel ファイルが作成されます。  
  
 **[既存のデータを表示]**  
 **[クエリ結果のプレビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 プレビューでは、最大で 200 行を表示できます。  
  
### <a name="data-access-mode-dynamic-options"></a>データ アクセス モードの動的オプション  
  
#### <a name="data-access-mode--table-or-view"></a>[データ アクセス モード] = [テーブルまたはビュー]  
 **[Excel シートの名前]**  
 データ ソースで使用できるワークシートまたは名前付き範囲の名前を一覧から選択します。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>[データ アクセス モード] = [テーブル名またはビュー名の変数]  
 **[変数名]**  
 ワークシートまたは名前付き範囲の名前が含まれている変数を選択します。  
  
#### <a name="data-access-mode--sql-command"></a>[データ アクセス モード] = [SQL コマンド]  
 **[SQL コマンド テキスト]**  
 SQL クエリのテキストを入力し、 **[クエリの作成]** をクリックしてクエリを作成します。または、 **[参照]** をクリックし、クエリ テキストが含まれているファイルを指定します。  
  
 **[クエリの作成]**  
 SQL クエリを視覚的に作成するには、 **[クエリ ビルダー]** ダイアログ ボックスを使用します。  
  
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、SQL クエリのテキストが含まれているファイルを指定します。  
  
 **[クエリの解析]**  
 クエリ テキストの構文を検査します。  
  
## <a name="excel-destination-editor-mappings-page"></a>[Excel 変換先エディター] ([マッピング] ページ)
  **[Excel 変換先エディター]** ダイアログ ボックスの **[マッピング]** ページを使用すると、入力列を変換先列にマップできます。  
  
### <a name="options"></a>オプション  
 **使用できる入力列**  
 使用できる入力列の一覧を表示します。 ドラッグ アンド ドロップ操作により、テーブル内の使用できる入力列を変換先列にマップします。  
  
 **使用できる変換先列**  
 使用できる変換先列の一覧を表示します。 ドラッグ アンド ドロップ操作により、テーブル内の使用できる変換先列を入力列にマップします。  
  
 **入力列**  
 上の表で選択された入力列が表示されます。 **[使用できる入力列]** ボックスの一覧を使用して、マッピングを変更できます。  
  
 **変換先列**  
 マップされているかどうかに関係なく、使用できる変換先列を表示します。  
  
## <a name="excel-destination-editor-error-output-page"></a>[Excel 変換先エディター] ([エラー出力] ページ)
  **[Excel 変換先エディター]** ダイアログ ボックスの **[詳細設定]** ページを使用すると、エラー処理オプションを指定できます。  
  
### <a name="options"></a>オプション  
 **入力または出力**  
 データ ソースの名前を表示します。  
  
 **列**  
 **[Excel ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ノードで選択されている外部 (ソース) 列を表示します。  
  
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
  
## <a name="see-also"></a>参照  
 [SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む](../load-data-to-from-excel-with-ssis.md)  
 [Excel ソース](../../integration-services/data-flow/excel-source.md)   
[Excel 接続マネージャー](../connection-manager/excel-connection-manager.md)
