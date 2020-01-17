---
title: 実行プランの比較と分析 | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Showplan results
- execution plans [SQL Server]
- queries [SQL Server], tuning
- execution plans [SQL Server], how-to topics
- SQL Server Management Studio [SQL Server], execution plans
- tuning queries [SQL Server]
ms.assetid: bcd6f094-c613-4835-ae19-4caaadb4bb17
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 4b300d1fbc144f25b3f725f34e49d961953c434c
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72289333"
---
# <a name="compare-and-analyze-execution-plans"></a>実行プランの比較と分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
このセクションでは、Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して実行プランを比較し、分析する方法について説明します。 この機能は [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v17.4 以降で使用できます。  
  
実行プランでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ オプティマイザーによって選択されたデータ取得方法がグラフィカルに表示されます。 実行プランでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の特定のステートメントやクエリの実行コストがアイコンで表されます。この点が、表形式で表す [SET SHOWPLAN_ALL](../../t-sql/statements/set-showplan-all-transact-sql.md) ステートメントまたは [SET SHOWPLAN_TEXT](../../t-sql/statements/set-showplan-text-transact-sql.md) ステートメントとは異なります。 グラフィカルな実行プランの表示は、クエリのパフォーマンスの特徴を理解するうえで非常に役立ちます。 

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] には、ユーザーが 2 つの実行プランを比較し (同じクエリに対して良く受け止められたプランと悪く受け止められたプランの比較など)、根本原因を分析するための機能が含まれています。 また、シングル クエリ プラン分析を実行する機能が含まれています。その実行プランを分析することで、クエリのパフォーマンスに影響を与えうるシナリオを理解できます。

クエリ実行プランの詳細については、[推定実行プラン](../../relational-databases/performance/display-the-estimated-execution-plan.md)、[実際の実行プラン](../../relational-databases/performance/display-an-actual-execution-plan.md)に関するページ、「[クエリ処理アーキテクチャ ガイド](../../relational-databases/query-processing-architecture-guide.md)」を参照してください。
  
## <a name="in-this-section"></a>このセクションの内容  
[実行プランの比較](../../relational-databases/performance/display-the-estimated-execution-plan.md)     
[実際の実行プランの分析](../../relational-databases/performance/display-an-actual-execution-plan.md)      
  
