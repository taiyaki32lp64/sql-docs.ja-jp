---
title: '手順 5: レッスン 4 のチュートリアル パッケージのテスト | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5f18df92-0248-4858-836b-c8b02f0e0439
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ba5766483def3dc357bc8f1bf65dd1048fa94b48
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295916"
---
# <a name="lesson-4-5-test-the-lesson-4-package"></a>レッスン 4-5: レッスン 4 のパッケージをテストする

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



壊れているファイル **Currency_BAD.txt** を実行すると、CurrencyKey 参照変換の照合結果の生成に失敗します。 CurrencyKey 参照変換のエラー出力は、失敗した行を新しい Failed Rows 変換先へリダイレクトするように構成されているので、コンポーネント自体は失敗せず、パッケージは正常に実行されます。 エラーがある行はすべて、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] によって **ErrorOutput.txt** に書き込まれます。  
  
この実習では、パッケージを実行して、変更したエラー出力構成をテストします。 パッケージが正常に実行されたら、**ErrorOutput.txt** ファイルの内容を確認します。  
  
> [!NOTE]  
> **ErrorOutput.txt** ファイルにエラー行が蓄積されないようにする場合は、パッケージ実行の合間に手動でファイルの内容を削除してください。  
  
## <a name="check-the-package-layout"></a>パッケージ レイアウトを確認する  
パッケージをテストする前に、レッスン 4 のパッケージ内の制御フローとデータ フローが次の図のようになっていることを確認します。 
  
**制御フロー**  
  
![パッケージ内の制御フロー](../integration-services/media/task4lesson2control.gif "パッケージ内の制御フロー")  
  
**データ フロー**  
  
![パッケージ内のデータ フロー](../integration-services/media/task5lesson5data.gif "パッケージ内のデータ フロー")  
  
## <a name="run-the-lesson-4-tutorial-package"></a>レッスン 4 のチュートリアル パッケージを実行する  
  
1.  **[デバッグ]** メニューの **[デバッグの開始]** を選択します。  
  
2.  パッケージの実行が完了したら、 **[デバッグ]** メニューの **[デバッグの停止]** を選択します。  
  
## <a name="view-the-contents-of-the-erroroutputtxt-file"></a>ErrorOutput.txt ファイルの内容を確認する  
  
メモ帳などのテキスト エディターで、**ErrorOutput.txt** ファイルを開きます。 既定の列の順序は次のとおりです。AverageRate、CurrencyID、CurrencyDate、EndOfDateRate、ErrorCode、ErrorColumn、ErrorDescription です。  
 
ファイルのすべての行には、一致しない CurrencyID 値 ("BAD")、ErrorCode 値 (-1071607778)、ErrorColumn 値 (0)、ErrorDescription 値 ("参照中に一致する行が見つかりませんでした") が含まれています。 エラーは列固有のものではなく、参照操作の失敗によるものであるため、ErrorColumn の値は 0 となります。
  
  
## <a name="next-lesson"></a>次のレッスン
[レッスン 5: パッケージ配置モデルの SSIS パッケージ構成を追加する](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
