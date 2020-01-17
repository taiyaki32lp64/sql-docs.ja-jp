---
title: クエリの検査 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:100644
helpviewer_keywords:
- verifying queries
- queries [SQL Server], verifying
- checking queries
ms.assetid: 1382c0c0-46dc-45f9-ab38-9bba1d347eea
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e19fbe26a7f3382885a8a1cd2bcbeaed71108708
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68261583"
---
# <a name="verify-queries-visual-database-tools"></a>クエリの検査 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
問題を回避するために、作成したクエリを検証して、構文が正しいことを確認できます。 このオプションは、 [SQL ペイン](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)にステートメントを入力する場合に特に便利です。  
  
次に、クエリの検査について注意が必要な点を挙げます。  
  
-   **ダイアグラム ペイン** および **抽出条件ペイン**に表示できない場合でも、有効なステートメントは正しく検査されます。  
  
-   SQL 検査では SQL エラーのすべてが検出されるわけではありません。 SQL 検査で検出されないエラーがクエリにある場合は、クエリを実行するときに、データベースによってエラーが検出されます。  
  
-   パラメーターを含むクエリは検査できません。  
  
### <a name="to-verify-an-sql-statement"></a>SQL ステートメントを検査するには  
  
-   **SQL ペイン**を右クリックし、ショートカット メニューの **[SQL 構文の確認]** を選択します。  
  
## <a name="see-also"></a>参照  
[クエリの実行 (Visual Database Tools)](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[クエリに関する基本操作の実行 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
