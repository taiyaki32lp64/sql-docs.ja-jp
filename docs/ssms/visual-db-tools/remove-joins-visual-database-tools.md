---
title: 結合の削除 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- removing joins
- joins [SQL Server], removing
- deleting joins
ms.assetid: ccc212a1-fd13-48d6-85e5-5ff310c34bbd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d36c4abea4cf28e870a74d95c49a56f477a3eb1a
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266268"
---
# <a name="remove-joins-visual-database-tools"></a>結合の削除 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
テーブルを内部結合または外部結合によって結合する必要がなくなった場合は、テーブル間の結合を削除できます。 たとえば、 [クエリおよびビュー デザイナー](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) が 2 つのテーブル間に自動的に作成した結合を削除できます。  
  
> [!NOTE]  
> クエリから結合を削除しても、データベースで設定されている基底のリレーションシップは変更されません。  
  
結合した 2 つのテーブルがクエリの一部であり、テーブル間の結合条件をすべて削除した場合、クエリ結果は両テーブルの積、つまりクロス結合となります。  
  
### <a name="to-remove-a-join"></a>結合を削除するには  
  
-   [ダイアグラム ペイン](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)で、削除する結合線を選択し、Del キーを押します。 同時に複数の結合線を選択して削除することもできます。  
  
クエリおよびビュー デザイナーが結合線を削除し、 [SQL ペイン](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)のステートメントを変更します。  
  
## <a name="see-also"></a>参照  
[テーブルの自動結合 (Visual Database Tools)](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md)  
[手動でのテーブルの結合 (Visual Database Tools)](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md)  
[結合を使用したクエリ (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
