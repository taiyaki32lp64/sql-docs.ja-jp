---
title: Reporting Services レポートの処理のトラブルシューティング | Microsoft Docs
ms.date: 08/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: bb309231-68be-4d68-a44c-c098999c67a2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 85486e929683abaf99216a4d4b03c19a146f230c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65573871"
---
# <a name="troubleshoot-processing-of-reporting-services-reports"></a>Reporting Services レポートの処理のトラブルシューティング
レポート データが取得されると、レポート プロセッサによってデータとレイアウトの情報が結合され、 結合されたデータとレイアウトのコンテキストで、式を持つ各レポート アイテム プロパティが評価されます。 このトピックでは、このような問題のトラブルシューティングについて説明します。   
  
## <a name="my-report-definition-is-not-valid"></a>レポート定義が有効でない  
実行時に、レポート プロセッサはレポート定義のデータ要素とレイアウト要素を結合し、レポート アイテム プロパティの式を評価します。   
  
レポート プロセッサは、レポート定義 (.rdl ファイル) が .rdl ファイルの先頭の名前空間宣言で指定されているスキーマに準拠していることを確認します。 RDL スキーマの詳細については、「 [レポート定義スキーマのバージョンを確認する (SSRS)](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md)」を参照してください。  
  
また、実行時に評価されるレポートの式は、レポートのデータとレイアウトを正しく結合できるようにする一連のルールに従っている必要があります。 レポート プロセッサで問題が検出されると、"レポート `<report name>` の定義が無効です" というメッセージが表示されることがあります。  
  
### <a name="report-item-expressions-can-only-refer-to-fields-within-the-current-dataset-scope-or-if-inside-an-aggregate-the-specified-dataset-scope"></a>レポート アイテムの式は、現在のデータセット スコープ、または集計内の場合は指定されたデータセット スコープ内のフィールドしか参照できない  
  
以下を参考にすると、エラーの原因の特定が容易になります。  
* レポートに複数のデータセットがある場合、レポート本文のテキスト ボックスの集計式でスコープ パラメーターを指定する必要があります。 たとえば、 `=First(Fields!FieldName.Value, "DataSet1")`のようにします。  
  
スコープ パラメーターを指定するには、レポート アイテムのスコープ内にあるデータセット、データ領域、またはグループの名前を指定します。 「 [合計、集計、および組み込みコレクションの式のスコープについて (レポート ビルダー 3.0 および SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) 」および「 [式のリファレンス (レポート ビルダー 3.0 および SSRS)](../../reporting-services/report-design/expression-reference-report-builder-and-ssrs.md)」を参照してください。  
  
### <a name="names-of-objects-must-be-greater-than-0-and-less-than-or-equal-to-256-characters"></a>オブジェクトの名前は、1 文字以上、256 文字以下にする必要がある  
レポート定義では、オブジェクト識別子の長さが 256 文字に制限されます。 識別子は、大文字と小文字を区別し、CLS に準拠する必要があります。 名前は文字で始まる必要があります。また、名前には、文字、数字、またはアンダースコア (_) を使用し、空白は使用しないでください。 たとえば、テキスト ボックスの名前やデータ領域の名前は、これらのガイドラインに準拠している必要があります。   
  
オブジェクトの名前を変更するには、プロパティ ペインのツール バーで、ドロップダウン リストから目的のアイテムを選択し、 **[名前]** までスクロールして、有効なオブジェクト名を入力します。   
  
## <a name="a-text-box-displays-error-how-do-i-fix-it"></a>テキスト ボックスに "#エラー" と表示される  
実行時にレポート プロセッサがレポート アイテム プロパティの式を評価し、データ型の変換エラーやスコープ エラーなどを検出すると、"#エラー" メッセージが表示されます。   
  
データ型エラーは、通常、既定のデータ型または指定されたデータ型がサポートされていないことを意味します。 スコープ エラーは、指定されたスコープが式の評価時に使用できなかったことを意味します。   
  
この "#エラー" メッセージが表示されないようにするには、原因となっている式を書き直す必要があります。 問題の詳細を調べるには、詳細なエラー メッセージを表示してください。   
  
プレビューでは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull.md)]で、出力ウィンドウを表示します。 レポート サーバーでは、呼び出し履歴を表示します。 
  
  
## <a name="see-also"></a>参照  
[エラーとイベント (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

