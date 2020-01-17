---
title: テーブルのスクリプト作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: ea88d736-849e-4368-b55d-06aeee097bf3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 22fae65a5e62be579f751dd3d6d3d0c9a73e7409
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63316394"
---
# <a name="script-a-table"></a>テーブルのスクリプト作成
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、テーブルを選択、挿入、更新、削除するスクリプト、およびストアド プロシージャを作成、変更、削除、または実行するスクリプトを作成できます。  
  
 プロシージャを削除した後でプロシージャを作成したり、テーブルを作成した後でテーブルを変更するなど、1 つのスクリプトで複数のオプションを実行させたい場合もあります。 複合的なスクリプトを作成するには、1 番目のスクリプトをクエリ エディター ウィンドウに保存し、2 番目のスクリプトをクリップボードに保存します。次に、クエリ エディター ウィンドウで、1 番目のスクリプトの後ろに 2 番目のスクリプトを貼り付けます。  
  
## <a name="creating-an-update-script"></a>更新スクリプトの作成  
  
#### <a name="to-create-the-insert-script-for-a-table"></a>テーブルの挿入スクリプトを作成するには  
  
1.  オブジェクト エクスプローラーでサーバーを展開し、 **[データベース]** 、[ [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]]、 **[テーブル]** の順に展開します。次に、 **[HumanResources.Employee]** を右クリックし、 **[テーブルをスクリプト化]** をポイントします。  
  
2.  ショートカット メニューには、7 つの使用可能なスクリプト作成オプションがあります。**作成**、**ドロップして、** 、 **DROP および CREATE**、**を**、**に挿入**、 **への更新**、および**削除**します。 **[データ更新]** をポイントし、 **[新しいクエリ エディター ウィンドウ]** をクリックします。  
  
3.  新しいクエリ エディター ウィンドウが開き、接続が確立され、更新ステートメント全体が表示されます。  
  
     この実習では、テーブルやストアド プロシージャを作成する以外にスクリプト機能でどのようなことを実行できるのかを学習します。 この新機能により、データ操作スクリプトをプロジェクトにすばやく追加し、スクリプトによるストアド プロシージャの実行を簡単に行うことができます。 多数のフィールドを持つテーブルやプロシージャでは、時間を大幅に節約できます。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [概要:書き込み TRANSACT-SQL](../../tutorials/summary-writing-transact-sql.md)  
  
  
