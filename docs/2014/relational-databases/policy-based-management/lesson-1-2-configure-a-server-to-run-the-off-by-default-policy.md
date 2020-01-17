---
title: "\"既定でオフ\" ポリシーを実行するためのサーバーの構成 | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 41c3022d-ab13-443e-ac64-ba1d64584f79
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8beb6998d78ad9a113ce18323133de7ed39ead56
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090638"
---
# <a name="configure-a-server-to-run-the-off-by-default-policy"></a>"既定でオフ" ポリシーを実行するためのサーバーの構成
  "既定でオフ" という名前のポリシーがあります。 この実習では、このポリシーの要件にサーバーが準拠しているかどうかを確認します。  
  
### <a name="to-run-the-off-by-default-policy"></a>"既定でオフ" ポリシーを実行するには  
  
1.  オブジェクト エクスプローラーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス名を右クリックし、 **[ポリシー]** をポイントして、 **[評価]** をクリックします。  
  
2.  **[ポリシーの評価]** ダイアログ ボックスで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の別のインスタンスから、またはファイルからポリシーを選択できます。 この手順では、 **[ソース]** を [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに設定したままにしてください。  
  
3.  **[ポリシー]** セクションで、 **[既定でオフ]** ポリシーを選択します。  
  
4.  サーバーがポリシーに準拠しているかどうかを確認するには、 **[評価]** をクリックします。  
  
5.  **[結果]** 領域では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] がポリシーに準拠している場合にチェック マークの付いた緑の円が表示されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] がポリシーに準拠していない場合は、X の付いた赤い円が表示されます。  
  
6.  **[対象の詳細]** 領域では、エラーが発生すると、 **[メッセージ]** 列に詳細情報が表示されます。 **[メッセージ]** 列では、 **[表示]** をクリックすると、確認された各ファセット プロパティの確認結果を示すレポートが表示されます。  
  
7.  ページの下部にポリシーの説明が表示され、 **[追加のヘルプ]** セクションにポリシーに対して構成したハイパーリンクが表示されます。 メッセージ ハイパーリンクをクリックすると、ポリシー作成時に指定した Web ページが開きます。  
  
8.  ブラウザーを閉じ、 **[結果の詳細ビュー]** ダイアログ ボックスを閉じます。  
  
9. サーバーが準拠していない場合に、データベース メールを無効にするには、 **[評価の結果]** ページで **[適用]** をクリックします。  
  
10. **[結果の詳細ビュー]** と **[ポリシーの評価]** の両方のダイアログ ボックスを閉じます。  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 2:名前付け基準ポリシーの作成と適用](lesson-2-create-and-apply-a-naming-standards-policy.md)  
  
  
