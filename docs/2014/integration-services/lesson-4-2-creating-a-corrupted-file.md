---
title: 手順 2:破損ファイルの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cd0b18dc-66c3-4d88-86ef-8e40cb660fae
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fa1bb23843447cc77276a34d5466d417f2a87a05
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767384"
---
# <a name="step-2-creating-a-corrupted-file"></a>手順 2:破損ファイルの作成
  変換エラーの構成と処理を体験するために、コンポーネントの処理が失敗するサンプル フラット ファイルを作成します。  
  
 この実習では、既存のサンプル フラット ファイルのコピーを作成します。 その後、このファイルをメモ帳などで開き、 **CurrencyID** 列を編集して、参照変換中に照合が失敗するようにします。 新しいファイルの処理時、参照が失敗すると Lookup Currency Key 変換は失敗し、それ以降のパッケージも失敗します。 破損しているサンプル ファイルを作成したら、パッケージを実行して、パッケージのエラーを確認します。  
  
### <a name="to-create-a-corrupted-sample-flat-file"></a>破損しているサンプル フラット ファイルを作成するには  
  
1.  メモ帳などのテキスト エディターで Currency_VEB.txt ファイルを開きます。  
  
     このサンプル データは、SSIS のレッスン パッケージに含まれています。 サンプル データとレッスン パッケージをダウンロードするには、次の手順を実行します。  
  
    1.  「 [Integration Services 製品サンプル](https://go.microsoft.com/fwlink/?LinkID=267527)」に移動します。  
  
    2.  **[ダウンロード]** タブをクリックします。  
  
    3.  SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip ファイルをクリックします。  
  
2.  使用して、テキスト エディターの検索と置換機能のすべてのインスタンスを`VEB`に置き換えます`BAD`します。  
  
3.  他のサンプル データ ファイルと同じフォルダーで、変更されたファイルとして保存`Currency_BAD.txt`します。  
  
    > [!IMPORTANT]  
    >  必ず`Currency_BAD.txt`他のサンプル データ ファイルと同じフォルダーに保存されます。  
  
4.  テキスト エディターを閉じます。  
  
### <a name="to-verify-that-an-error-will-occur-during-run-time"></a>実行時にエラーが発生することを確認するには  
  
1.  **[デバッグ]** メニューの **[デバッグの開始]** をクリックします。  
  
     データ フローの 3 つ目の反復処理で、Lookup Currency Key 変換が Currency_BAD.txt ファイルを処理しようとし、変換が失敗します。 この変換エラーにより、パッケージ全体が失敗します。  
  
2.  **[デバッグ]** メニューの **[デバッグの停止]** をクリックします。  
  
3.  デザイン画面で、 **[実行結果]** タブをクリックします。  
  
4.  ログの内容を参照し、次の処理不能エラーが発生していることを確認します。  
  
     `[Lookup Currency Key[27]] Error: Row yielded no match during lookup.`  
  
    > [!NOTE]  
    >  数値 27 はコンポーネントの ID です。 この値はデータ フローを構築したときに割り当てられるもので、パッケージの値とは異なることがあります。  
  
## <a name="next-steps"></a>次の手順  
 [ステップ 3:エラー フロー リダイレクションの追加](lesson-4-3-adding-error-flow-redirection.md)  
  
  
