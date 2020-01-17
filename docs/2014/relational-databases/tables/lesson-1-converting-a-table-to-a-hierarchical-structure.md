---
title: レッスン 1:テーブルの階層構造への変換 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 66e77d0badf14a804cb82249d03ed552e1f8dcfb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205647"
---
# <a name="lesson-1-converting-a-table-to-a-hierarchical-structure"></a>レッスン 1:テーブルの階層構造への変換
  階層リレーションシップを表すために自己結合を使っているテーブルがある場合、このレッスンの説明に従って、それらのテーブルを階層構造に変換できます。 現在の表示から、`hierarchyid` を使用した表示に移行するのは比較的簡単です。 移行後は、コンパクトで理解しやすい階層表示が可能になるため、ユーザーはさまざまな方法でインデックスを作成して効率的なクエリを実現できます。  
  
 このレッスンでは、既存のテーブルを検証した後、`hierarchyid` 列を含む新しいテーブルを作成し、そのテーブルにソース テーブルのデータを取り込みます。さらに、3 とおりのインデックス作成方法を紹介します。 このレッスンの内容は次のとおりです。  
  
-   [Employee テーブルの現在の構造の確認](lesson-1-1-examining-the-current-structure-of-the-employee-table.md)  
  
-   [既存の階層データを使用したテーブルの設定](lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
-   [NewOrg テーブルの最適化](lesson-1-3-optimizing-the-neworg-table.md)  
  
-   [概要:テーブルの階層構造への変換](lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
## <a name="prerequisites"></a>前提条件  
 このレッスンを学習するには、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースが必要です。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [Employee テーブルの現在の構造の確認](lesson-1-1-examining-the-current-structure-of-the-employee-table.md)  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 2:作成して、階層テーブルでデータを管理します。](lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)  
  
  
