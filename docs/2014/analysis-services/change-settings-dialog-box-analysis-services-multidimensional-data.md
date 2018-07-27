---
title: 変更の設定 ダイアログ ボックス (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.process.batchsettingsdialog.f1
ms.assetid: 0041e042-d7ce-48f9-a690-a6dc65471ff3
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5c9a70f95f552ee5a614f8f44e1f8436c0aa35e8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151743"
---
# <a name="change-settings-dialog-box-analysis-services---multidimensional-data"></a>[設定の変更] ダイアログ ボックス (Analysis Services - 多次元データ)
  **および** の [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] [設定の変更] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ダイアログ ボックスを使用すると、 **[処理]** ダイアログ ボックスに示されているオブジェクトの処理を制御する設定を変更できます。 **[設定の変更]** ダイアログ ボックスを表示するには、 **[処理]** ダイアログ ボックスの **[設定の変更]** をクリックします。  
  
> [!NOTE]  
>  このダイアログ ボックスで指定された設定は、**[処理]** ダイアログ ボックスに一覧表示されたオブジェクトの、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースから継承された既定の設定をオーバーライドします。  
  
## <a name="options"></a>および  
 **処理オプション**  
 このタブを使用して、処理中の操作の処理順序、書き戻しテーブル、および影響を受けたオブジェクトに関連する設定を修正します。 このタブには次のオプションがあります。  
  
 **Parallel**  
 オブジェクトを並列に処理します。  
  
 **最大並列タスク**  
 処理中の操作で並列に実行されるタスクの最大数を選択するか、 **[サーバーの決定]** を選択し、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] が並列タスクの最適数を選択します。  
  
 **シーケンシャル**  
 オブジェクトを順番に処理します。  
  
 **[トランザクション モード]**  
 オブジェクトが順番に処理される際に使用するトランザクション モードを次から選択します。  
  
-   **[1 つのトランザクション]** は、同じトランザクションのすべてのオブジェクトを処理します。  
  
-   **[個別のトランザクション]** は、依存オブジェクトを含む、個別のトランザクションのすべてのオブジェクトを処理します。  
  
> [!NOTE]  
>  このオプションは、 **[シーケンシャル]** が選択されている場合にのみ有効です。  
  
 **書き戻しテーブル オプション**  
 書き戻しテーブルの管理に使用するオプションを選択します。  
  
-   **[作成]** は、書き戻しテーブルが存在しない場合に作成します。 書き戻しテーブルが既に存在する場合はエラーが発生します。  
  
-   **[常に作成]** は、書き戻しテーブルが存在しない場合に作成するか、既存の書き戻しテーブルを上書きします。  
  
-   **[既存のデータを使用する]** は、書き戻しテーブルが存在する場合にそれを使用します。 書き戻しテーブルが存在しない場合はエラーが発生します。  
  
 **[影響を受けたオブジェクトの処理]**  
 処理中の操作に含まれているオブジェクトに依存するオブジェクトを、処理対象に含めて処理します。  
  
 **ディメンション キーのエラー**  
 このタブを使用して、処理中の操作のエラー構成に関連する設定を修正します。 このタブには次のオプションがあります。  
  
 **既定のエラー構成を使用して、**  
 処理操作でオブジェクトに対して既定のエラー構成を使用します。  
  
 **カスタム エラー構成を使用**  
 処理操作でオブジェクトに対してエラー構成を定義します。  
  
 **[キー エラー アクション]**  
 参照できない処理の間に新しいキーが検出されたとき、発生するアクションを次の中から 1 つ選択します。  
  
-   **[不明な種類に変換]** は、レコードの情報を不明なメンバーに集計します。  
  
-   **[レコードの破棄]** は、レコードの情報をオブジェクトでの処理から除外します。  
  
 **エラーの数を無視します。**  
 処理中に発生するエラーは、すべて無視します。  
  
 **[エラー時に停止する]**  
 エラーが発生した場合、処理を停止します。 このオプションによって、 **[エラー数]** オプションおよび **[エラー時のアクション]** オプションが有効になります。  
  
 **[エラー数]**  
 処理が停止される前に無視できるエラーの数を入力します。  
  
 **[エラー時のアクション]**  
 エラー数が **[エラー数]** の値を超えたときに行うアクションを次の中から 1 つ選択します。  
  
-   **[処理の停止]** は、処理中の操作を終了します。  
  
-   **[ログ記録の停止]** は、エラーのログ記録を停止しますが、処理中の操作は続行します。  
  
 **[見つからないキー]**  
 オブジェクトの処理の際にキーが見つからなかった場合に行うアクションを次の中から 1 つ指定します。  
  
-   **[エラーを無視する]** は、エラーを無視します。  
  
-   **[報告して続行する]** は、エラーを報告して、処理中の操作を続行します。  
  
-   **[報告して停止する]** は、エラーを報告して、処理中の操作を停止します。  
  
 **[重複キー]**  
 オブジェクトの処理の際に重複キーが見つかった場合に行うアクションを次の中から 1 つ指定します。  
  
-   **[エラーを無視する]** は、エラーを無視します。  
  
-   **[報告して続行する]** は、エラーを報告して、処理中の操作を続行します。  
  
-   **[報告して停止する]** は、エラーを報告して、処理中の操作を停止します。  
  
 **[不明な種類に変換された NULL キー]**  
 オブジェクトの処理の際に NULL メンバー キーが不明なメンバーに追加された場合に行うアクションを次の中から 1 つ指定します。  
  
-   **[エラーを無視する]** は、エラーを無視します。  
  
-   **[報告して続行する]** は、エラーを報告して、処理中の操作を続行します。  
  
-   **[報告して停止する]** は、エラーを報告して、処理中の操作を停止します。  
  
 **[許可されていない NULL キー]**  
 オブジェクトの処理の際に NULL キーが見つかったが許可されていない場合に行うアクションを次の中から 1 つ指定します。  
  
-   **[エラーを無視する]** は、エラーを無視します。  
  
-   **[報告して続行する]** は、エラーを報告して、処理中の操作を続行します。  
  
-   **[報告して停止する]** は、エラーを報告して、処理中の操作を停止します。  
  
 **[エラー ログのパス]**  
 エラー ログ ファイルの完全なパスとファイル名を入力します。  
  
 **[参照]**  
 **[開く]** ダイアログ ボックスを表示し、エラー ログ ファイルの完全なパスおよびファイル名を選択します。  
  
 **[影響を受けたオブジェクトの処理]**  
 **[処理]** ダイアログ ボックスで選択されたオブジェクトに依存するオブジェクトを処理します。  
  
## <a name="see-also"></a>参照  
 [Analysis Services のデザイナーおよびダイアログ ボックス&#40;多次元データ&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [[プロセス] ダイアログ ボックス&#40;Analysis Services - 多次元データ&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  