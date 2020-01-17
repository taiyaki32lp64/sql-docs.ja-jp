---
title: 手順 4:フラット ファイル変換先の追加 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: f4088de3-16d8-419c-96a1-a2cd005d0a5b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ae02b9188ecc9917d26532633e4d5a253d4f326b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295945"
---
# <a name="lesson-4-4-add-a-flat-file-destination"></a>レッスン 4-4:フラット ファイル変換先を追加する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Lookup Currency Key 変換でエラーが出力されると、参照に失敗したデータ行がスクリプト変換操作にリダイレクトされます。 発生したエラーに関する詳細を提供する目的で、スクリプト変換によって各エラーの説明を取得するスクリプトが実行されます。  
  
ここでは、後続の処理のために、失敗した行に関するすべての情報を区切りテキスト ファイルに保存します。 失敗した行を保存するには、フラット ファイル接続マネージャーで、エラー データとフラット ファイル変換先が入るテキスト ファイルを追加し、構成します。 フラット ファイル変換先が使用するフラット ファイル接続マネージャーでプロパティを設定することにより、フラット ファイル変換先がテキスト ファイルをフォーマットする方法と書き込む方法を指定できます。 詳細については、「[フラット ファイル接続マネージャー](../integration-services/connection-manager/flat-file-connection-manager.md)」と「[フラット ファイル変換先](../integration-services/data-flow/flat-file-destination.md)」を参照してください。  
  
## <a name="add-and-configure-a-flat-file-destination"></a>フラット ファイル変換先を追加し、構成する  
  
1.  **[データ フロー]** タブを選択します。  
  
2.  **[SSIS ツールボックス]** で **[その他の変換先]** を展開し、 **[フラット ファイル変換先]** をデータ フロー デザイン画面上にドラッグします。 **[フラット ファイル変換先]** を **[Get Error Description]** 変換のすぐ下にドロップします。  
  
3.  **[Get Error Description]** 変換を選択し、青の矢印を新しい **[フラット ファイル変換先]** までドラッグします。  
  
4.  **[データ フロー]** デザイン画面で、新しい **[フラット ファイル変換先]** 変換の名前 **[フラット ファイル変換先]** を選択し、その名前を「**Failed Rows**」に変更します。  
  
5.  この **Failed Rows** 変換を右クリックし、 **[編集]** を選択します。次に、 **[フラット ファイル変換先エディター]** の **[新規作成]** を選択します。  
  
6.  **[フラット ファイル形式]** ダイアログ ボックスで、 **[区切り記号]** が選択されていることを確認し、 **[OK]** を選択します。  
  
7.  **[フラット ファイル接続マネージャー エディター]** の **[接続マネージャー名]** ボックスに「*Error Data*」と入力します。  
  
8.  **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスで、 **[参照]** を選択し、ファイルの保存先のフォルダーに移動します。  
  
9. **[ファイルを開く]** ダイアログ ボックスで、 **[ファイル名]** に「*ErrorOutput.txt*」と入力し、 **[開く]** を選択します。  
  
10. **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスで、 **[ロケール]** に **[英語 (米国)]** 、 **[コード ページ]** に **[1252 (ANSI - ラテン I)]** が表示されていることを確認します。  
  
11. [オプション] ペインで、 **[列]** を選択します。  
  
    ソース データ ファイルからの列に加え、3 つの新しい列、ErrorCode、ErrorColumn、ErrorDescription があります。 これらの列は、Lookup Currency Key 変換のエラー出力と Get Error Description 変換のスクリプトです。 これらの列は、失敗した行の問題を解決するために使用できます。  
  
12. **[OK]** を選択します。  
  
13. **[フラット ファイル変換先エディター]** で、 **[ファイル内のデータを上書きする]** チェック ボックスをオフにします。  
  
    このチェック ボックスをオフにすると、新しい実行のたびにエラーが出力され、パッケージを何回実行してもエラーが継続します。
  
14. **[フラット ファイル変換先エディター]** の **[マッピング]** を選択し、すべての列が正しいことを確認します。 必要に応じて、変換先の列の名前を変更できます。  
  
15. **[OK]** を選択します。  
  
## <a name="go-to-next-task"></a>次の実習に進む
[手順 5:レッスン 4 で作成したチュートリアル パッケージのテスト](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
  
  
