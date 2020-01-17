---
title: 手順 5:レッスン 4 のチュートリアル パッケージのテスト |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5f18df92-0248-4858-836b-c8b02f0e0439
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fab91a2df7d0401e8301589b1dd0d21027e579c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62891292"
---
# <a name="step-5-testing-the-lesson-4-tutorial-package"></a>手順 5:レッスン 4 のチュートリアル パッケージのテスト
  壊れているファイル Currency_BAD.txt を実行すると、CurrencyKey 参照変換の照合結果の生成に失敗します。 ただし、CurrencyKey 参照変換のエラー出力は、失敗した行を新しい [Failed Rows] 変換先へリダイレクトするように構成されています。したがって、コンポーネント自体は失敗せず、パッケージは正常に実行されます。 エラーがある行はすべて、ErrorOutput.txt に書き込まれます。  
  
 この実習では、パッケージを実行して、変更したエラー出力構成をテストします。 パッケージが正常に実行されたら、ErrorOutput.txt ファイルの内容を確認します。  
  
> [!NOTE]  
>  ErrorOutput.txt ファイルにエラー行が蓄積されないようにする場合は、パッケージ実行の間に手動でファイルの内容を削除してください。  
  
## <a name="checking-the-package-layout"></a>パッケージ レイアウトの確認  
 パッケージをテストする前に、次の図に示すオブジェクトがレッスン 4 のパッケージの制御フローとデータ フローに含まれていることを確認します。 制御フローはレッスン 2 ～ 4 の制御フローと同じである必要があります。  
  
 **制御フロー**  
  
 ![パッケージ内の制御フロー](../../2014/tutorials/media/task4lesson2control.gif "パッケージ内の制御フロー")  
  
 **データ フロー**  
  
 ![パッケージ内のデータ フロー](../../2014/tutorials/media/task5lesson5data.gif "パッケージ内のデータ フロー")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>レッスン 4 のチュートリアル パッケージを実行するには  
  
1.  **[デバッグ]** メニューの **[デバッグの開始]** をクリックします。  
  
2.  パッケージの実行が完了したら、 **[デバッグ]** メニューの **[デバッグの停止]** をクリックします。  
  
### <a name="to-verify-the-contents-of-the-erroroutputtxt-file"></a>ErrorOutput.txt ファイルの内容を確認するには  
  
-   メモ帳などのテキスト エディターで ErrorOutput.txt ファイルを開きます。 既定の列の順序は次のとおりです。AverageRate、CurrencyID、CurrencyDate、EndOfDateRate、ErrorCode、ErrorColumn、ErrorDescription です。  
  
     ファイルのすべての行には、一致しない CurrencyID 値 BAD、ErrorCode 値 -1071607778、ErrorColumn 値 0、ErrorDescription 値 "参照中に一致する行が見つかりませんでした" が含まれています。 エラーは列固有ではなく、ErrorColumn の値は 0 になっています。 これは失敗した参照操作を表します。 .  
  
  
