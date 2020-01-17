---
title: クエリに対する変更の破棄 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- reverting queries
- queries [SQL Server], discarding changes
- discarding query changes
ms.assetid: 7bb17ece-1222-4622-b476-5789d7641c64
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cb5db1e50e23772219bd7cd822d8e04615b13a29
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263756"
---
# <a name="discard-changes-made-to-queries-visual-database-tools"></a>クエリに対する変更の破棄 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
変更を保存する前であれば、クエリ定義に対して行った変更を破棄できます。 いったん変更を保存すると、変更前の状態に戻すことはできなくなります。  
  
> [!NOTE]  
> 結果ペインで値に行った変更を元に戻すには、レコードから移動する前に Esc キーを押します。 レコードから移動して、変更がデータベースにコミットされないという通知を受け取った場合も、Esc キーを押すことで前の値に戻ることができます。  
  
### <a name="to-discard-changes-made-to-a-query-definition"></a>クエリ定義に行った変更を破棄するには  
  
1.  クエリを開いているクエリおよびビュー デザイナーで、 **[ファイル]** メニューの **[閉じる]** をクリックします。  
  
2.  **[Microsoft SQL Server Management Studio]** ダイアログ ボックスで **[いいえ]** を選択します。  
  
    クエリの定義が前回保存した状態に戻ります。  
  
## <a name="see-also"></a>参照  
[クエリの保存 (Visual Database Tools)](../../ssms/visual-db-tools/save-queries-visual-database-tools.md)  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[クエリに関する基本操作の実行 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[結果ペインのデータの操作 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-data-in-the-results-pane-visual-database-tools.md)  
  
