---
title: 検索基準の指定 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], Criteria pane
- queries [Visual Database Tools]
- criteria for search conditions
- search conditions [SQL Server], search criteria
- View Designer, Criteria pane
- row return limitations [SQL Server]
- Criteria pane
- restricting rows returned
- search criteria [SQL Server]
- Visual Database Tools [SQL Server], queries
- limiting rows returned
ms.assetid: 25fb4e31-6dbf-4cf6-8e47-0dd0998c836c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f3cef20ba9e4d841e74a8deaed47fab2f8b6b193
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263537"
---
# <a name="specify-search-criteria-visual-database-tools"></a>検索基準の指定 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
検索基準を使用すると、クエリによって返される行数を制限できます。  
  
検索基準の作成手順の詳細については、次の表の各トピックを参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
[検索値を入力するときの規則 (Visual Database Tools)](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
テキスト、数値、日付、または論理値の入力方法を説明します。  
  
[抽出条件ペインで検索条件を組み合わせる場合の規則 (Visual Database Tools)](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
AND 演算子および OR 演算子の使用の背景にある概念を説明します。  
  
[検索条件の指定 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-conditions-visual-database-tools.md)  
必要なデータが得られるように検索基準を選択するための基礎知識を説明します。  
  
[1 つの列に対して複数の検索条件を指定する (Visual Database Tools)](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-one-column-visual-database-tools.md)  
同じデータ列に対して複数の検索条件を作成する方法を説明します。  
  
[複数の列に対して複数の検索条件を指定する (Visual Database Tools)](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-multiple-columns-visual-database-tools.md)  
クエリの検索条件の一部として複数のデータ列を指定する方法を説明します。  
  
[クエリでの TOP 句の指定 (Visual Database Tools)](../../ssms/visual-db-tools/specify-the-top-clause-in-queries-visual-database-tools.md)  
指定した数または割合の行だけを返す方法を説明します。  
  
[同一クエリ内で HAVING 句および WHERE 句を使用する (Visual Database Tools)](../../ssms/visual-db-tools/use-having-and-where-clauses-in-the-same-query-visual-database-tools.md)  
この 2 つの句を 1 つのクエリで両方使用する方法と理由を説明します。  
  
[値の一致しない行を選択する方法 (Visual Database Tools)](../../ssms/visual-db-tools/select-rows-that-do-not-match-a-value-visual-database-tools.md)  
指定した列の値が、クエリ ステートメントで指定した値と一致しない行をすべて返す方法を説明します。  
  
[行を含めるまたは除外する (Visual Database Tools)](../../ssms/visual-db-tools/include-or-exclude-rows-visual-database-tools.md)  
クエリで使用される句と演算子の背景にある概念を説明します。  
  
[重複する行の除外 (Visual Database Tools)](../../ssms/visual-db-tools/exclude-duplicate-rows-visual-database-tools.md)  
選択クエリの結果で重複している行をフィルター処理する方法を説明します。  
  
[AND が優先する場合の条件を結合する (Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-and-has-precedence-visual-database-tools.md)  
クエリ結果をフィルター処理するために AND 演算子を使用する理由と方法を説明します。  
  
[OR が優先する場合の条件を結合する (Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
クエリ結果をフィルター処理するために OR 演算子を使用する理由と方法を説明します。  
  
[サブクエリの作成 (Visual Database Tools)](../../ssms/visual-db-tools/create-subqueries-visual-database-tools.md)  
サブクエリまたは入れ子になったクエリを作成する方法を説明します。  
  
## <a name="related-sections"></a>関連項目  
[クエリに関する基本操作の実行 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
リンクが掲載されており、リンク先には最も一般的な問い合わせタスクの手順についてのトピックが掲載されています。  
  
[クエリの種類 (Visual Database Tools)](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
リンクが掲載されており、リンク先にはサポートされているクエリの種類を解説するトピックが掲載されています。  
  
[クエリ結果の並べ替えおよびグループ化 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
リンクが掲載されており、リンク先にはクエリの結果を並べ替えおよびグループ化する手順に関するトピックが掲載されています。  
  
[クエリ結果の要約 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
リンクが掲載されており、リンク先には NULL 列および数値以外の列を含む、結果の集計の手順に関するトピックが掲載されています。  
  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
クエリおよびビュー デザイナーを使用してクエリとビューで実行できる作業に関する、トピックとセクションへのリンクが掲載されています。  
  
