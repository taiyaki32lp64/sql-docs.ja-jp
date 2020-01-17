---
title: 統計の更新タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.updatestatisticstask.f1
helpviewer_keywords:
- updating statistics
- Update Statistics task [Integration Services]
ms.assetid: 0247483b-f092-4511-8fa8-3610108bd1bc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: be80af34bc2dc8b5d069406bc13a8f8f9b25c42c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62829454"
---
# <a name="update-statistics-task"></a>統計の更新タスク
  統計の更新タスクは、指定されたテーブルまたはインデックス付きビュー内の 1 つ以上の統計グループ (コレクション) についてキー値の分布に関する情報を更新します。 詳細については、「 [Statistics](../../relational-databases/statistics/statistics.md)」を参照してください。  
  
 統計の更新タスクを使用すると、パッケージは単一データベースまたは複数のデータベース内の統計を更新できます。 このタスクにより単一データベース内の統計のみを更新する場合、タスクによって統計を更新するビューおよびテーブルを選択できます。 更新は、すべての統計、列統計のみ、またはインデックス統計のみを対象とするように構成できます。  
  
 このタスクは、次の引数および句を含めて UPDATE STATISTICS ステートメントをカプセル化します。  
  
-   *table_name* または *view_name* 引数。  
  
-   すべての統計に更新が適用される場合、暗黙的に WITH ALL 句が含められます。  
  
-   列統計にのみ更新が適用される場合、WITH COLUMN 句が含められます。  
  
-   インデックス統計にのみ更新が適用される場合、WITH INDEX 句が含められます。  
  
 統計の更新タスクにより複数データベース内の統計を更新する場合、タスクは複数の UPDATE STATISTICS ステートメントを各テーブルまたはビューに対して 1 つずつ実行します。 UPDATE STATISTICS の全インスタンスで同じ句が使用されますが、*table_name* または *view_name* の値が異なります。 詳細については、「[CREATE STATISTICS (Transact-SQL)](/sql/t-sql/statements/create-statistics-transact-sql)」および「[UPDATE STATISTICS (Transact-SQL)](/sql/t-sql/statements/update-statistics-transact-sql)」を参照してください。  
  
> [!IMPORTANT]  
>  実行する Transact-SQL ステートメントを作成するためにタスクが費やす時間は、タスクが更新する統計数に比例します。 多数のインデックスを含むデータベースのすべてのテーブルおよびビュー内の統計の更新、または複数のデータベース内の統計の更新を実行するようにタスクが構成されている場合、タスクが Transact-SQL ステートメントを生成するには非常に長い時間がかかることがあります。  
  
## <a name="configuration-of-the-update-statistics-task"></a>統計の更新タスクの構成  
 プロパティは、 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから設定できます。 このタスクは、 **デザイナーの** [ツールボックス] **の** [メンテナンス プランのタスク] [!INCLUDE[ssIS](../../../includes/ssis-md.md)] に表示されます。  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[統計の更新タスク] (メンテナンス プラン)](../../relational-databases/maintenance-plans/update-statistics-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](integration-services-tasks.md)   
 [制御フロー](control-flow.md)  
  
  
