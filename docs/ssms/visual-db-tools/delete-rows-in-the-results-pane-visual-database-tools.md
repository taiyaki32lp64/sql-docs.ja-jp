---
title: 結果ペイン内の行の削除 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- removing rows
- row removal [SQL Server], Visual Database Tools Results pane
- row deletions [SQL Server], Visual Database Tools Results pane
- Query Designer [SQL Server], Results pane
- deleting rows
- Results pane
ms.assetid: a1147905-fe4a-4fac-b576-a17622477e66
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a07da8ed6f57a8ebcc693391bc69a0ba88175b87
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263836"
---
# <a name="delete-rows-in-the-results-pane-visual-database-tools"></a>結果ペイン内の行の削除 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
データベース内のレコードを削除するには、結果ペイン内の行を削除します。 すべての行を削除する場合、削除クエリを使用できます。 詳細については、「 [削除クエリの作成 (Visual Database Tools)](../../ssms/visual-db-tools/create-delete-queries-visual-database-tools.md)」を参照してください。 結果ペインからの行の削除だけを行う場合は、クエリの条件を変更します。 詳細については、「 [検索基準の指定 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)」を参照してください。  
  
### <a name="to-delete-a-row-or-rows"></a>1 行または複数の行を削除するには  
  
1.  結果ペイン内で、削除する行の左側にあるボックスを選択します。  
  
2.  Del キーを押します。  
  
3.  確認を要求するメッセージ ボックスで、 **[はい]** をクリックします。  
  
> [!CAUTION]  
> この方法で削除した行は、データベースから完全に削除され、再度呼び出すことはできません。  
  
> [!NOTE]  
> 選択した行をデータベースから削除できない場合、行の削除は行われず、削除できない行を通知するメッセージが表示されます。  
  
## <a name="see-also"></a>参照  
[削除クエリの作成 (Visual Database Tools)](../../ssms/visual-db-tools/create-delete-queries-visual-database-tools.md)  
[検索基準の指定 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
