---
title: 複数のユーザーによる変更の調整 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- table modifications [SQL Server], multiple users
- reconciling changes made by multiple users
- modifications made by multiple users
ms.assetid: fc7ed4f2-ad3d-47fc-a3ef-51e5bb069ef0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f13b7f6a2e34d7819b930d919e9fd773e2c993d7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63010673"
---
# <a name="reconcile-changes-made-by-multiple-users-visual-database-tools"></a>複数のユーザーによる変更の調整 (Visual Database Tools)
  マルチユーザー環境では、同一のオブジェクトに複数のユーザーが同時に変更を加える場合があります。 この現象は、テーブル デザイナーまたはデータベース ダイアグラム デザイナーでオブジェクトの構造を操作しているときに発生する可能性があります。また、クエリおよびビュー デザイナーの結果ペインに返された結果の値に、他のユーザーが変更を加えている場合もあります。 こうした現象により、解決を必要とする競合が発生する可能性があります。  
  
## <a name="conflicts-in-the-table-or-database-diagram-designers"></a>テーブル デザイナーまたはデータベース ダイアグラム デザイナーでの競合  
 たとえば、テーブル デザイナーでテーブルを操作しているときに、他のユーザーが同じテーブルまたは関連するテーブルを削除したり、名前を変更したりする可能性があります。 テーブルを保存しようとすると、 [[データベースの変更を確認] ダイアログ ボックス (Visual Database Tools)](visual-database-tools.md) によって、テーブルを前回開いた後でデータベースが更新されたことが通知されます。  
  
 このダイアログ ボックスには、テーブルを保存する結果として影響を受けるデータベース オブジェクトの一覧も表示されます。 この時点で、次のいずれかの処理を実行できます。  
  
-   **[はい]** をクリックして、一覧内のすべての変更内容をデータベースに反映させます。  
  
     このアクションを実行すると、同じデータベース オブジェクトを共有しているテーブルが影響を受けます。 たとえば、 `au`テーブルの`id` _ `titleauthors` 列を編集しているときに、他のユーザーが、 `authors` 列によって `titleauthors` テーブルと関連付けられている `au`\_`id` テーブルを操作しているとします。 このテーブルを保存すると、他のユーザーのテーブルが影響を受けます。 同様に、あるユーザーが `qty` テーブルの `sales` 列に CHECK 制約を定義したとします。 別のユーザーが `qty` 列を削除して `sales` テーブルを保存すると、最初のユーザーの CHECK 制約が影響を受けます。  
  
-   保存を取り消すには、 **[いいえ]** をクリックします。  
  
     その後、保存せずにテーブルを閉じます。 テーブルを再度開くと、そのテーブルにはデータベースの現在の内容が反映されています。  
  
-   変更内容の一覧を保存するには、 **[テキスト ファイルを保存]** をクリックします。  
  
     **[データベースの変更を確認]** ダイアログ ボックスに表示されているデータベースの変更内容の一覧をテキスト ファイルに保存すると、他のユーザーによる変更の原因を調査できます。 たとえば、削除することにしたテーブルを他のユーザーが編集していた場合、データベースを更新する前にテーブルを削除する必要があるかどうかを調べることができます。  
  
## <a name="conflicts-in-the-query-and-view-designer"></a>クエリおよびビュー デザイナーでの競合  
 クエリを実行するか、ビューの結果を返すと、 [結果ペイン](results-pane-visual-database-tools.md)にデータが表示されます。 複数のユーザーが同じデータセットを同時に操作すると、競合が発生する場合があります。  
  
 たとえば、他のユーザーと同時に `titleauthors` テーブルの全データを表示するクエリを実行するとします。 他のユーザーが、最初に返されるレコードの名前を Barb から Barbara に変更するとします。 この時点で、データベースの該当するフィールドの値は Barbara ですが、こちら側に表示されている結果セットは Barb のままです。 ここで、Barbara と入力して、その行から移動するとします。 すると、競合の解決方法をたずねるメッセージが表示されます。  
  
-   データベースに変更内容を反映させるには、 **[はい]** をクリックします。  
  
     他のユーザーの変更をオーバーライドします。  
  
-   データベースの現在の内容に結果セットを更新するには、 **[いいえ]** をクリックします。  
  
     こちら側の変更が他のユーザーの変更によってオーバーライドされます。  
  
-   競合を解決せずに編集を続行するには、 **[キャンセル]** をクリックします。  
  
     この場合、変更を加えてもデータベースにコミットできなくなります。  
  
## <a name="see-also"></a>参照  
 [[データベースの変更を確認] ダイアログ ボックス (Visual Database Tools)](visual-database-tools.md)  
  
  
