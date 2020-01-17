---
title: クエリおよびビュー デザイナーを開く (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- opening View Designer
- View Designer, opening
- Query Designer [SQL Server], opening
- opening Query Designer
ms.assetid: b473f258-d53c-41c0-9ad9-528a2ff141f4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6dc9d87aafadabee059c674423dfbcfd9f1ab63b
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263278"
---
# <a name="open-the-query-and-view-designer-visual-database-tools"></a>クエリおよびビュー デザイナーを開く (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
ビューの定義を開いたり、クエリまたはビューの結果を表示したり、クエリを作成したり開いたりすると、クエリおよびビュー デザイナーが開きます。 クエリおよびビュー デザイナーは、4 つの個別のペインで構成されています。  
  
-   ダイアグラム ペインには、データ接続で選択したテーブルまたはテーブル値オブジェクトが、グラフィカルに表示されます。 また、テーブル間の結合リレーションシップも示されます。  
  
-   抽出条件ペインでは、表示するデータ列、結果の順序、選択する行などのクエリ オプションを選択してスプレッドシート形式のグリッドに入力することにより、クエリ オプションを指定できます。  
  
-   SQL ペインでは、任意の SQL ステートメントを作成できます。抽出条件ペインおよびダイアグラム ペインでも SQL ステートメントを作成できますが、どちらの場合も SQL ステートメントは SQL ペインに作成されます。 クエリを作成すると、SQL ペインは自動的に更新され、読みやすいように書式が変更されます。  
  
-   結果ペインには、最後に実行された選択クエリの結果が表示されます。 他の種類のクエリ結果は、メッセージ ボックスに表示されます。  
  
-   これらのペインはクエリおよびビューを操作する場合に便利です。  
  
-   ビューまたはクエリを開くと、いくつかのペインまたはすべてのペインがビューまたはクエリと共に開きます。 どのペインが開くかは、 **[オプション]** ダイアログ ボックスの設定、および接続しているデータベース管理システムの種類によって異なります。 既定の設定では、4 つすべてが開きます。  
  
### <a name="to-open-the-query-and-view-designer-for-a-view"></a>クエリおよびビュー デザイナーでビューを開くには  
  
1.  オブジェクト エクスプローラーで、開くビューを右クリックし、 **[デザイン]** または **[ビューを開く]** をクリックします。  
  
    **[デザイン]** を選択すると、 **[オプション]** ダイアログ ボックスで選択したオプションに従い、クエリおよびビュー デザイナーのペインが開きます。 **[ビューを開く]** を選択すると、既定で結果ペインのみが開きます。  
  
### <a name="to-open-the-query-and-view-designer-for-an-existing-query"></a>クエリおよびビュー デザイナーで既存のクエリを開くには  
  
1.  ソリューション エクスプローラーで、 **[クエリ]** フォルダーを展開します。  
  
2.  開くクエリをダブルクリックします。  
  
3.  クエリ ステートメントを強調表示し、強調表示された領域を右クリックして、 **[エディターでクエリをデザイン]** をクリックします。  
  
## <a name="see-also"></a>参照  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[クエリおよびビュー デザイナー ツール (Visual Database Tools)](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)  
  
