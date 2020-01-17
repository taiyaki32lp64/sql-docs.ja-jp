---
title: インデックスの再構築タスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rebuildindextask.f1
helpviewer_keywords:
- rebuilding indexes
- indexes [Integration Services]
- Rebuild Index task
ms.assetid: 021884dd-e72d-47b2-99e8-b741410509c3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9e89c081c1c543c198a827955ab4865709ead391
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62830426"
---
# <a name="rebuild-index-task"></a>インデックスの再構築タスク
  インデックスの再構築タスクでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのテーブルおよびビュー内のインデックスを再構築します。 インデックスの管理の詳細については、「 [インデックスの再編成と再構築](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)」を参照してください。  
  
 インデックスの再構築タスクを使用すると、パッケージは単一データベースまたは複数のデータベース内のインデックスを再構築できます。 このタスクにより単一データベース内のインデックスのみを再構築する場合、タスクによってインデックスを再構築するビューおよびテーブルを選択できます。  
  
 このタスクは、次のインデックス再構築オプションを付けて ALTER INDEX REBUILD ステートメントをカプセル化します。  
  
-   FILLFACTOR のパーセント値を指定するか、または FILLFACTOR の元の値を使用します。  
  
-   PAD_INDEX = ON と設定すると、FILLFACTOR で指定された空き容量がインデックスの中間レベル ページに割り当てられます。  
  
-   SORT_IN_TEMPDB = ON と設定すると、インデックスの作成に使用された並べ替えの途中結果が tempdb に格納されます。 並べ替えの途中結果が OFF に設定されている場合、インデックスと同じデータベースに結果が保存されます。  
  
-   IGNORE_DUP_KEY = ON と設定すると、UNIQUE 制約に違反するレコードを含む複数行の挿入操作を行う場合に、UNIQUE 制約に違反しないレコードを挿入できるようになります。  
  
-   ONLINE = ON と設定すると、テーブルをロックしたままにせず、インデックスの再構築中に基になるテーブルに対するクエリまたは更新を行えるようになります。  
  
> [!NOTE]  
>  オンラインでのインデックス操作は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。  
  
 ALTER INDEX ステートメントおよびインデックスの再構築オプションの詳細については、「[ALTER INDEX (Transact-SQL)](/sql/t-sql/statements/alter-index-transact-sql)」を参照してください。  
  
> [!IMPORTANT]  
>  実行する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを作成するためにタスクが費やす時間は、タスクが再構築するインデックス数に比例します。 多数のインデックスを含むデータベースのすべてのテーブルおよびビュー内のインデックスの再構築、または複数のデータベース内のインデックスの再構築を実行するようにタスクが構成されている場合、タスクが Transact-SQL ステートメントを生成するには非常に長い時間がかかることがあります。  
  
## <a name="configuration-of-the-rebuild-index-task"></a>インデックスの再構築タスクの構成  
 プロパティは、 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから設定できます。 このタスクは、 **デザイナーの** [ツールボックス] **の** [メンテナンス プランのタスク] [!INCLUDE[ssIS](../../../includes/ssis-md.md)] に表示されます。  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
 [[インデックスの再構築タスク] (メンテナンス プラン)](../../relational-databases/maintenance-plans/rebuild-index-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 これらのプロパティを [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーで設定する方法の詳細については、「 [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](integration-services-tasks.md)   
 [制御フロー](control-flow.md)  
  
  
