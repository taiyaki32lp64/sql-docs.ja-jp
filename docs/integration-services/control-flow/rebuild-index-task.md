---
title: インデックスの再構築タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rebuildindextask.f1
helpviewer_keywords:
- rebuilding indexes
- indexes [Integration Services]
- Rebuild Index task
ms.assetid: 021884dd-e72d-47b2-99e8-b741410509c3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: af10da0db8cff17e6cf06c155a85713a3fae50eb
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294017"
---
# <a name="rebuild-index-task"></a>インデックスの再構築タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  インデックスの再構築タスクでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのテーブルおよびビュー内のインデックスを再構築します。 インデックスの管理の詳細については、「 [インデックスの再編成と再構築](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)」を参照してください。  
  
 インデックスの再構築タスクを使用すると、パッケージは単一データベースまたは複数のデータベース内のインデックスを再構築できます。 このタスクにより単一データベース内のインデックスのみを再構築する場合、タスクによってインデックスを再構築するビューおよびテーブルを選択できます。  
  
 このタスクは、次のインデックス再構築オプションを付けて ALTER INDEX REBUILD ステートメントをカプセル化します。  
  
-   FILLFACTOR のパーセント値を指定するか、または FILLFACTOR の元の値を使用します。  
  
-   SORT_IN_TEMPDB = ON と設定すると、インデックスの作成に使用された並べ替えの途中結果が tempdb に格納されます。 並べ替えの途中結果が OFF に設定されている場合、インデックスと同じデータベースに結果が保存されます。  
  
-   PAD_INDEX = ON と設定すると、FILLFACTOR で指定された空き容量がインデックスの中間レベル ページに割り当てられます。  
  
-   IGNORE_DUP_KEY = ON と設定すると、UNIQUE 制約に違反するレコードを含む複数行の挿入操作を行う場合に、UNIQUE 制約に違反しないレコードを挿入できるようになります。  
  
-   ONLINE = ON と設定すると、テーブルをロックしたままにせず、インデックスの再構築中に基になるテーブルに対するクエリまたは更新を行えるようになります。  
  
    > [!NOTE]  
    >  オンラインでのインデックス操作は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
-   並列プランの実行で使用されるプロセッサ数を制限するには、MAXDOP の値を指定します。  
  
-   優先度の低いロックをインデックス操作が待機する時間を制御するには、WAIT_AT_LOW_PRIORITY、MAX_DURATION、および ABORT_AFTER_WAIT を指定します。  
  
 ALTER INDEX ステートメントおよびインデックスの再構築オプションの詳細については、「[ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)」を参照してください。  
  
> [!IMPORTANT]  
>  実行する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを作成するためにタスクが費やす時間は、タスクが再構築するインデックス数に比例します。 多数のインデックスを含むデータベースのすべてのテーブルおよびビュー内のインデックスの再構築、または複数のデータベース内のインデックスの再構築を実行するようにタスクが構成されている場合、タスクが Transact-SQL ステートメントを生成するには非常に長い時間がかかることがあります。  
  
## <a name="configuration-of-the-rebuild-index-task"></a>インデックスの再構築タスクの構成  
 プロパティは、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから設定できます。 このタスクは、 **デザイナーの** [ツールボックス] **の** [メンテナンス プランのタスク] [!INCLUDE[ssIS](../../includes/ssis-md.md)] に表示されます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
 [[インデックスの再構築タスク] (メンテナンス プラン)](../../relational-databases/maintenance-plans/rebuild-index-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 これらのプロパティを [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定する方法の詳細については、「 [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)   
 [制御フロー](../../integration-services/control-flow/control-flow.md)  
  
  
