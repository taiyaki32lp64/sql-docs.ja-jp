---
title: 結合の削除 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- removing joins
- joins [SQL Server], removing
- deleting joins
ms.assetid: ccc212a1-fd13-48d6-85e5-5ff310c34bbd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ac2b8ca912f02aecc5e1b3e76d04d84b501db89b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63253493"
---
# <a name="remove-joins-visual-database-tools"></a>結合の削除 (Visual Database Tools)
  テーブルを内部結合または外部結合によって結合する必要がなくなった場合は、テーブル間の結合を削除できます。 たとえば、 [クエリおよびビュー デザイナー](visual-database-tools.md) が 2 つのテーブル間に自動的に作成した結合を削除できます。  
  
> [!NOTE]  
>  クエリから結合を削除しても、データベースで設定されている基底のリレーションシップは変更されません。  
  
 結合した 2 つのテーブルがクエリの一部であり、テーブル間の結合条件をすべて削除した場合、クエリ結果は両テーブルの積、つまりクロス結合となります。  
  
### <a name="to-remove-a-join"></a>結合を削除するには  
  
-   [ダイアグラム ペイン](diagram-pane-visual-database-tools.md)で、削除する結合線を選択し、Del キーを押します。 同時に複数の結合線を選択して削除することもできます。  
  
 クエリおよびビュー デザイナーが結合線を削除し、 [SQL ペイン](sql-pane-visual-database-tools.md)のステートメントを変更します。  
  
## <a name="see-also"></a>参照  
 [テーブルの自動結合&#40;Visual Database Tools&#41;](join-tables-automatically-visual-database-tools.md)   
 [テーブルを手動で結合&#40;Visual Database Tools&#41;](join-tables-manually-visual-database-tools.md)   
 [結合を使用したクエリ (Visual Database Tools)](query-with-joins-visual-database-tools.md)  
  
  
