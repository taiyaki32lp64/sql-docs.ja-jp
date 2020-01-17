---
title: 方法:データの差異を表示する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.datacompare.f1
ms.assetid: f88d3350-2eaf-44cc-96a8-84008b6cd071
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ec641fc027bae18a09e81d5cf14eee1bd8ab3ee3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930340"
---
# <a name="how-to-view-data-differences"></a>方法:データの差異を表示する
2 つのデータベースのデータを比較すると、比較した各*データベース オブジェクト*とその状態が一覧表示されます。 各オブジェクト内のレコードの結果を状態別にグループ化して表示することもできます。  
  
差異を表示した後、異なる、欠落している、または新しいオブジェクトまたはレコードの一部またはすべてについて、*ソース*と一致するように*ターゲット*を更新できます。  
  
### <a name="to-view-data-differences"></a>データの差異を表示するには  
  
1.  ソースとターゲットのデータを比較します。  
  
2.  (省略可能) 次のいずれかまたは両方の操作を行います。  
  
    -   既定では、状態に関係なく、すべてのオブジェクトの結果が表示されます。 特定の状態のオブジェクトのみを表示するには、 **[フィルター]** ボックスの一覧でオプションをクリックします。  
  
    -   特定のオブジェクト内のレコードの結果を表示するには、メインの結果ペインでオブジェクトをクリックし、レコード ビュー ペインでタブをクリックします。 各タブには、そのオブジェクト内で特定の状態 (不一致、ソースのみに存在、ターゲットのみに存在、または一致) にあるすべてのレコードが表示されます。 データは、レコードおよび列ごとに表示されます。  
  
## <a name="see-also"></a>参照  
[方法:スキーマ比較を使用して各種のデータベース定義を比較する](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)  
  
