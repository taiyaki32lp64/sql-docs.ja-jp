---
title: ヒント (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- query optimizer [SQL Server], hints
- hints [SQL Server], about hints
- SELECT statement [SQL Server], hints
- hints [SQL Server]
- INSERT statement [SQL Server], hints
- UPDATE statement [SQL Server], hints
- DELETE statement [SQL Server], hints
ms.assetid: 99412475-b0df-4264-9938-33a0b302b41a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3f7bc162244e30b2ac48f9b49a6c596268b595c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901976"
---
# <a name="hints-transact-sql"></a>ヒント (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  ヒントは、SELECT、INSERT、UPDATE、または DELETE の各ステートメントについて、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ プロセッサが実施するように指定したオプションまたは方法です。 ヒントは、クエリ オプティマイザーがクエリのために選択するどの実行プランよりも優先されます。  
  
> [!CAUTION]  
>  通常、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ オプティマイザーでは、クエリにとって最適な実行プランが選択されるため、\<join_hint>、\<query_hint> および \<table_hint> は、経験を積んだ開発者やデータベース管理者が最後の手段としてのみ使用することをお勧めします。
  
 ここでは、次のヒントについて説明します。  
  
-   [結合ヒント](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [テーブル ヒント](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
