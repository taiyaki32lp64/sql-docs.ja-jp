---
title: 手順 8:レッスン 1 パッケージに注釈を付け、書式を設定する | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3a67d7593ca63a2271fc94fc7203e9bb55d6efcc
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71680975"
---
# <a name="lesson-1-8-annotate-and-format-the-lesson-1-package"></a>レッスン 1-8:レッスン 1 パッケージに注釈を付け、書式を設定する 

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



ここまでの作業で、レッスン 1 のパッケージの構成が完了しました。次は、パッケージのレイアウトを整理することをお勧めします。 コントロールやデータ フロー レイアウトで図形のサイズが異なっていたり、均等にレイアウトされていなかったりする場合、パッケージがわかりにくくなることがあります。  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools には、パッケージ レイアウトを簡単に書式設定するためのツールがあります。 この書式設定機能を使用すると、複数の図形を同じサイズにしたり、整列したり、図形間の上下左右の間隔を変更したりできます。  
  
パッケージの機能をわかりやすくするには、パッケージ機能について説明した注釈を追加するという方法もあります。  
  
この実習では、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools の書式設定機能を使用してデータ フローのレイアウトを改善し、注釈を追加します。  
  
## <a name="format-the-layout-of-the-data-flow"></a>データ フローのレイアウトを書式設定する  
  
1.  レッスン 1 のパッケージを開いていない場合は、**ソリューション エクスプローラー**で **Lesson 1.dtsx** をダブルクリックします。  
  
2.  **[データ フロー]** タブを選択します。  
  
3.  データ フロー コンポーネントを一度に全部選択するには、 **[編集]** の **[すべて選択]** を使用します。
  
4.  **[書式]** メニューの **[同じサイズに揃える]** を選択し、 **[両方]** を選択します。  
  
5.  データ フロー オブジェクトが選択されている状態で、 **[書式]** メニューの **[整列]** を選択し、 **[中央]** をクリックします。  

6.  データ フロー オブジェクトが選択されている状態で、 **[書式]** メニューの **[上下の間隔]** をポイントし、 **[間隔を均等にする]** をクリックします。  
  
## <a name="add-an-annotation-to-the-data-flow"></a>データ フローに注釈を追加する  
  
1.  データ フローのデザイン画面の背景で任意の場所を右クリックし、 **[注釈の追加]** を選択します。  
  
2.  注釈ボックスに、次のテキストを入力するか、コピーして貼り付けます。  
  
        The data flow extracts data from a file, looks up values in the CurrencyKey column in the DimCurrency table and the DateKey column in the DimDate table, and writes the data to the NewFactCurrencyRate table.
  
    注釈ボックスのテキストを折り返すには、改行する場所にカーソルを置いて、**Enter** を押します。  
  
    注釈ボックスにテキストを追加しない場合、注釈ボックスの外側をクリックするとボックスの表示が消えます。  この動作により、注釈ボックスにテキストを貼り付けたい場合は、[注釈の追加] を選択する前にテキストをクリップボードにコピーします。 
  
## <a name="go-to-next-task"></a>次のタスクに進む
[手順 9:レッスン 1 パッケージをテストする](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  
  
