---
title: 手順 8:レッスン 1 のパッケージをわかりやすく |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 390fb10287ff88ec5f7a0220dea6dd677e8e36cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767594"
---
# <a name="step-8-making-the-lesson-1-package-easier-to-understand"></a>手順 8:レッスン 1 のパッケージをわかりやすくする作業
  ここまでの作業で、レッスン 1 のパッケージの構成が完了しました。次は、パッケージのレイアウトを整理することをお勧めします。 制御フローやデータ フローのレイアウトの図形サイズがまちまちであったり、図形の整列やグループ化が行われていないと、パッケージの機能がわかりにくくなることがあります。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools には、パッケージのレイアウトをすばやく簡単に書式設定できるツールが用意されています。 この書式設定機能を使用すると、複数の図形を同じサイズにしたり、整列したり、図形間の上下左右の間隔を操作することができます。  
  
 パッケージの機能をわかりやすくするには、パッケージ機能について説明した注釈を追加するという方法もあります。  
  
 この実習では、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools の書式設定機能を使用してデータ フローのレイアウトを改善し、さらにデータ フローに注釈を追加します。  
  
### <a name="to-format-the-layout-of-the-data-flow"></a>データ フローのレイアウトを書式設定するには  
  
1.  レッスン 1 のパッケージを開いていない場合は、ソリューション エクスプローラーで Lesson 1.dtsx をダブルクリックします。  
  
2.  **[データ フロー]** タブをクリックします。  
  
3.  Extract Sample Currency 変換の右上隅にカーソルを合わせ、クリックしてすべてのデータ フロー コンポーネントを囲むようにドラッグします。  
  
4.  **[書式]** メニューの **[同じサイズに揃える]** をポイントし、 **[両方]** をクリックします。  
  
5.  データ フロー オブジェクトが選択されている状態で、 **[書式]** メニューの **[整列]** をポイントし、 **[左]** をクリックします。  
  
### <a name="to-add-an-annotation-to-the-data-flow"></a>データ フローに注釈を追加するには  
  
1.  データ フローのデザイン画面の背景で任意の場所を右クリックし、 **[注釈の追加]** をクリックします。  
  
2.  注釈ボックスに、次のテキストを入力するか、コピーして貼り付けます。  
  
     **このデータ フローは、ファイルからデータを抽出し、DimCurrency テーブルの CurrencyKey 列の値と DimDate テーブルの DateKey 列の値を参照して、データを NewFactCurrencyRate テーブルに書き込みます。**  
  
     注釈ボックスのテキストを折り返すには、改行する場所にカーソルを置いて、Enter キーを押します。  
  
     注釈ボックスにテキストを追加しない場合は、注釈ボックスの外側をクリックするとボックスは表示されなくなります。  
  
## <a name="next-steps"></a>次の手順  
 [手順 9:レッスン 1 のチュートリアル パッケージのテスト](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  
