---
title: 方法:スクリプト間を移動する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.editor.howto.navigate
ms.assetid: 8664bde5-86ff-4e8b-b5a6-af003316f6ad
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b5ff9e02b15c70d08151384bb46332e8b4ea550a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035158"
---
# <a name="how-to-navigate-between-scripts"></a>方法:スクリプト間を移動する
Transact\-SQL エディターでは、オフライン開発用に 2 つの便利なナビゲーション ツールが用意されています。[定義へ移動] と [すべての参照の検索] です。 たとえば、テーブル名を右クリックし、[すべての参照の検索] を使用すると、プロジェクト内のそのテーブルへの参照をすべて一覧表示できます。 検索結果をダブルクリックすると、特定のコード ファイルに移動できます。 このファイル内でテーブル名を再度右クリックし、[定義へ移動] をクリックすると、テーブル定義に戻ります。  
  
> [!WARNING]  
> 以下に示す手順では、「[接続されているデータベース開発](../ssdt/connected-database-development.md)」および「[プロジェクト指向のオフライン データベース開発](../ssdt/project-oriented-offline-database-development.md)」に示されているこれまでの手順で作成したエンティティを使用します。  
  
### <a name="to-navigate-between-scripts"></a>スクリプト間を移動するには  
  
1.  **ソリューション エクスプローラー**で **[関数]** フォルダーを展開し、**GetProductsBySupplier.sql** をダブルクリックします。  
  
2.  コード内の以下の行で `Products` を右クリックし、 **[定義へ移動]** をクリックします  
  
    ```  
    SELECT * from Products p  
    ```  
  
3.  Products.sql が自動的に開き、`Products` 型が定義されている場所が示されます。  
  
4.  GetProductsBySupplier.sql に戻ります。 今度は、`Products` のコンテキスト メニューの **[すべての参照の検索]** をクリックします。 **シンボルの検索結果**ペインに、`Products` テーブルが参照されている場所の一覧が表示されます。 任意の検索結果をダブルクリックすると、参照の場所に移動できます。  
  
