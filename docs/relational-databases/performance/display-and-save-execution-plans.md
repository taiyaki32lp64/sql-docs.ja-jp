---
title: 実行プランの表示と保存 | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2017
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
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 11c33865990bd67e62436de3106282f873e5d0fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946833"
---
# <a name="display-and-save-execution-plans"></a>実行プランの表示と保存
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
ここでは、実行プランを表示する方法、および Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して実行プランを XML 形式でファイルに保存する方法について説明します。  
  
実行プランでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ オプティマイザーによって選択されたデータ取得方法がグラフィカルに表示されます。 実行プランでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の特定のステートメントやクエリの実行コストがアイコンで表されます。この点が、表形式で表す [SET SHOWPLAN_ALL](../../t-sql/statements/set-showplan-all-transact-sql.md) ステートメントまたは [SET SHOWPLAN_TEXT](../../t-sql/statements/set-showplan-text-transact-sql.md) ステートメントとは異なります。 グラフィカルな実行プランの表示は、クエリのパフォーマンスの特徴を理解するうえで役立ちます。  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ オプティマイザーから生成される実行プランは 1 つのみですが、**推定**実行プランと**実際**の実行プランという概念があります。
-  [推定実行プラン](../../relational-databases/performance/display-the-estimated-execution-plan.md)は、コンパイル時にクエリ オプティマイザーが生成する実行プランを返します。 推定実行プランを生成しても、実際にはクエリやバッチが実行されません。そのため、実際のリソース使用状況のメトリックやランタイムの警告など、実行時情報が含まれていません。 
-  [実際の実行プラン](../../relational-databases/performance/display-an-actual-execution-plan.md)は、クエリまたはバッチが実行を完了した後に、クエリ オプティマイザーが生成する実行プランを返します。 実際の実行プランには、リソース使用状況のメトリックやランタイムの警告に関するランタイム情報が含まれます。  

クエリ実行プランの詳細については、「[クエリ処理アーキテクチャ ガイド](../../relational-databases/query-processing-architecture-guide.md)」を参照してください。
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [推定実行プランの表示](../../relational-databases/performance/display-the-estimated-execution-plan.md)  
  
-   [実際の実行プランの表示](../../relational-databases/performance/display-an-actual-execution-plan.md)  
  
-   [XML 形式での実行プランの保存](../../relational-databases/performance/save-an-execution-plan-in-xml-format.md)  
  
  
