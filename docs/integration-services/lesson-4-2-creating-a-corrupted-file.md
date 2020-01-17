---
title: 手順 2:破損ファイルの作成 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: cd0b18dc-66c3-4d88-86ef-8e40cb660fae
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cd9266512675c4127a99903e6de0d1da5ccaec70
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295960"
---
# <a name="lesson-4-2-create-a-corrupted-file"></a>レッスン 4-2:破損したファイルを作成する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



変換エラーの構成と処理を体験するには、コンポーネントの処理が失敗するサンプル フラット ファイルが必要です。  
  
この実習では、既存のサンプル フラット ファイルのコピーを作成します。 メモ帳でファイルを開き、**CurrencyID** 列を編集し、参照に失敗する正しくない値を入力します。 破損ファイルの処理時、参照が失敗すると Lookup Currency Key 変換は失敗し、それ以降のパッケージも失敗します。 破損しているサンプル ファイルを作成したら、パッケージを実行して、パッケージのエラーを確認します。  
  
## <a name="create-a-corrupted-sample-flat-file"></a>破損しているサンプル フラット ファイルを作成する  
  
1.  メモ帳などのテキスト エディターで **Currency_VEB.txt** ファイルを開きます。  
  
2.  テキスト エディターの検索置換機能を使用し、 **VEB** と表示されているすべての箇所を **BAD**に置換します。  
  
3.  他のサンプル データ ファイルと同じフォルダーに、修正したファイルを保存します。このファイルには「 **Currency_BAD.txt**」という名前を付けてください。  
  
    > [!NOTE]  
    > **Currency_BAD.txt** が他のサンプル データ ファイルと同じフォルダーに保存されていることを確認してください。  
  
4.  テキスト エディターを閉じます。  
  
## <a name="verify-that-an-error-occurs-during-run-time"></a>実行時にエラーが発生することを確認する  
  
1.  **[デバッグ]** メニューの **[デバッグの開始]** を選択します。  
  
    データ フローの 3 つ目の反復処理で、Lookup Currency Key 変換が **Currency_BAD.txt** ファイルを処理しようとし、変換が失敗します。 この変換エラーにより、パッケージ全体が失敗します。  
  
2.  **[デバッグ]** メニューの **[デバッグの停止]** を選択します。  
  
3.  デザイン画面で、 **[実行結果]** タブを選択します。  
  
4.  ログの内容を参照し、次の処理不能エラーが発生していることを確認します。  
  
    ```
    [Lookup Currency Key[27]] Error: Row yielded no match during lookup.
    ```
  
    > [!NOTE]  
    > 数値 27 はコンポーネントの ID です。 この値はデータ フローを構築したときに割り当てられるもので、パッケージの値とは異なることがあります。  
  
## <a name="go-to-next-task"></a>次の実習に進む  
[手順 3:エラー フロー リダイレクションを追加する](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
  
  
