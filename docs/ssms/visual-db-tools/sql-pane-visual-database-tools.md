---
title: SQL ペイン (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], SQL pane
- View Designer, SQL pane
- SQL pane [Visual Database Tools]
ms.assetid: dbabab18-0614-415b-a2ef-9bcd0d320d5c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ab19242401fb962152fcd9fbeef590922d104498
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265623"
---
# <a name="sql-pane-visual-database-tools"></a>SQL ペイン (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
SQL ペインでは、任意の SQL ステートメントを作成できます。抽出条件ペインおよびダイアグラム ペインでも SQL ステートメントを作成できますが、どちらの場合も SQL ステートメントは SQL ペインに作成されます。 クエリを作成すると、SQL ペインは自動的に更新され、読みやすいように書式が変更されます。  
  
SQL ペインを開くには、まずクエリおよびビュー デザイナーを開きます。これには、サーバー エクスプローラーでデータベース オブジェクトを選択し、 **[データベース]** メニューの **[新しいクエリ]** をクリックします。 次に、 **[クエリ デザイナー]** メニューの **[ペイン]** をポイントし、 **[SQL]** をクリックします。  
  
SQL ペインでは、次の作業を行うことができます。  
  
-   SQL ステートメントを入力し、新しいクエリを作成する。  
  
-   ダイアグラム ペインおよび抽出条件ペインで行った設定に基づいてクエリおよびビュー デザイナーが作成した SQL ステートメントを変更する。  
  
-   使用しているデータベース固有の機能を利用するステートメントを入力する。  
  
> [!NOTE]  
> 使用しているデータベースでデータベース オブジェクトを識別する規則を確認してください。 詳細については、使用しているデータベース管理システムのマニュアルを参照してください。  
  
## <a name="statements-in-the-sql-pane"></a>SQL ペインにステートメントを入力する  
SQL ペインでは、現在のクエリを直接編集できます。 他のペインに移動すると、クエリおよびビュー デザイナーによってステートメントの書式が自動的に設定され、ステートメントに合わせてダイアグラム ペインと抽出条件ペインが変更されます。  
  
ダイアグラム ペインおよび抽出条件ペインが表示されていて、これらのペインでステートメントを表示できない場合、クエリおよびビュー デザイナーはエラーを表示します。この場合、次のいずれかを選択できます。  
  
-   ダイアグラム ペインおよび抽出条件ペインでステートメントを表示できなくても無視して作業を続ける。  
  
-   表示できない変更を元に戻して、その前に変更を加えた後の SQL ステートメントに戻す。  
  
ダイアグラム ペインおよび抽出条件ペインでステートメントを表示できなくても無視して作業を続けることを選択した場合、これらのペインは、SQL ペインの内容を反映できないことを示すため、淡色表示されます。  
  
ステートメントの編集と実行は、他の SQL ステートメントと同じように実行できます。  
  
> [!NOTE]  
> SQL ステートメントを入力した後に、ダイアグラム ペインと抽出条件ペインでクエリを変更した場合、クエリおよびビュー デザイナーでは SQL ステートメントのリビルドおよび再表示が行われます。 この処理の結果、最初に入力した SQL ステートメントとは異なるステートメントが作成されることがあります。ただし、ステートメントの実行結果は常に同じになります。 この現象は、AND または OR で連結された複数の句を含む検索条件がある場合によく発生します。  
  
## <a name="see-also"></a>参照  
[クエリの作成 (Visual Database Tools)](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[クエリの実行 (Visual Database Tools)](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[ダイアグラム ペイン (Visual Database Tools)](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[抽出条件ペイン (Visual Database Tools)](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[結果ペイン (Visual Database Tools)](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)  
  
