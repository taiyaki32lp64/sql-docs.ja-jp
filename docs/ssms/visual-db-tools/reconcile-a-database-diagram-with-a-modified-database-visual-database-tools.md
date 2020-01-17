---
title: データベース ダイアグラムへのデータベースの変更の反映 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- updating diagram to match database
- reconciling database diagrams
- diagrams [SQL Server], reconciling changes
- updating database to match diagram
- database diagrams [SQL Server], reconciling changes
ms.assetid: eda8dea2-eedd-43a7-85aa-92bd97783b5f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 37801a47dc7ee4df7253f554adc522798b964891
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266248"
---
# <a name="reconcile-a-database-diagram-with-a-modified-database-visual-database-tools"></a>データベース ダイアグラムへのデータベースの変更の反映 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
データベース ダイアグラムは、ダイアグラムと一致するようにデータベースを更新する準備ができた段階で保存します。 ただし、ダイアグラムを開いた後で別のユーザーがデータベースを更新した場合は、変更内容によって自分のダイアグラムが影響を受けることがあります。また、別のユーザーがデータベースを開いた後で自分がデータベースを更新した場合は、相手のダイアグラムが影響を受けることもあります。  
  
ダイアグラムを保存すると、他のユーザーの変更が上書きされ、データベースにダイアグラムの内容が反映されます。そのため、データベースはダイアグラムと一致します。  
  
### <a name="to-update-a-database-to-match-your-diagram"></a>ダイアグラムに一致するようにデータベースを更新するには  
  
1.  データベース ダイアグラムを保存します。  
  
    ダイアグラムを初めて保存する場合は、 **[新しいデータベース ダイアグラムの保存]** ダイアログ ボックスにダイアグラム名を入力し、 **[OK]** をクリックします。  
  
2.  ダイアグラムを保存するときに影響を受けるテーブルが **[上書き保存]** ダイアログ ボックスに一覧表示されます。 **[はい]** をクリックして次の手順に進みます。  
  
3.  他のユーザーによって変更されたオブジェクトのうち、ダイアグラムの内容に合うように再度変更されるオブジェクトが、 **[データベースの変更を確認]** ダイアログ ボックスに一覧表示されます。 **[はい]** をクリックしてダイアグラムを保存し、変更一覧を受け入れます。  
  
    > [!NOTE]  
    > データベースで削除されたテーブルや列がダイアグラムに含まれている場合は、ダイアグラムを保存すると、テーブルや列の定義だけがデータベースに再度作成されます。 削除前にオブジェクトに存在していたデータは復元されません。  
  
### <a name="to-update-your-diagram-to-match-a-modified-database"></a>変更されたデータベースに一致するようにダイアグラムを更新するには  
  
1.  変更を保存せずにダイアグラムを閉じます。  
  
2.  オブジェクト エクスプローラーでダイアグラムを右クリックします。  
  
3.  ショートカット メニューの **[最新の情報に更新]** をクリックします。  
  
4.  ダイアグラムを再度開きます。  
  
## <a name="see-also"></a>参照  
[データベース ダイアグラムの使用 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  
