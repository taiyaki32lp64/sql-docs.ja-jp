---
title: DBCC (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC
- DBCC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transactional consistency
- Database Console Command statements
- status information [SQL Server], DBCC statements
- snapshots [SQL Server database snapshots], DBCC statements
- emergency database state [SQL Server]
- TABLOCK
- internal database snapshots [SQL Server]
- reporting DBCC statement progress
- logical consistency of data [SQL Server]
- DBCC statements
- validation statements [SQL Server]
- miscellaneous statements [SQL Server]
- statements [SQL Server], DBCC statements
- DBCC commands [SQL Server]
- result sets [SQL Server], DBCC statements
- maintenance statements [SQL Server]
- physical consistency of data [SQL Server]
- current DBCC statement status
- progress reporting [DBCC statements]
- informational statements [SQL Server]
ms.assetid: c6da8c04-5b6b-459a-9f76-110c92ca8b29
author: pmasl
ms.author: umajay
ms.openlocfilehash: 7f0d3d07f6f4a0ef3a35991c4805c478ed702bdf
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982441"
---
# <a name="dbcc-transact-sql"></a>DBCC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

[!INCLUDE[tsql](../../includes/tsql-md.md)] プログラミング言語には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベース コンソール コマンドとして機能する DBCC ステートメントが用意されています。
  
データベース コンソール コマンドは、次のように分類されます。
  
|コマンドのカテゴリ|実行内容|  
|---|---|
|メンテナンス|データベース、インデックスまたはファイル グループを対象とするメンテナンス タスク。|  
|その他|トレース フラグの有効化やメモリからの DLL の削除など、その他のタスク。|  
|情報提供|さまざまな種類の情報を収集および表示するタスク。|  
|検証|データベース、テーブル、インデックス、カタログ、ファイル グループ、またはデータベース ページの割り当ての検証操作。|  
  
DBCC コマンドは入力パラメーターをと受け取り、値を返します。 すべての DBCC コマンド パラメーターには、Unicode と DBCS の両方のリテラルを使用できます。
  
## <a name="dbcc-internal-database-snapshot-usage"></a>DBCC 内部データベース スナップショットの使用  
次の DBCC コマンドは、[!INCLUDE[ssDE](../../includes/ssde-md.md)]で作成される内部の読み取り専用データベース スナップショットに対して実行でき、 これにより、コマンド実行時のブロックやコンカレンシーの問題を回避できます。 詳細については、「[データベース スナップショット &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)」を参照してください。
- DBCC CHECKALLOC
- DBCC CHECKCATALOG
- DBCC CHECKDB
- DBCC CHECKFILEGROUP
- DBCC CHECKTABLE

DBCC コマンドの 1 つを実行すると、[!INCLUDE[ssDE](../../includes/ssde-md.md)] ではデータベース スナップショットが作成され、スナップショットはトランザクション全体で一貫性のある状態になります。 その後、DBCC コマンドではこのスナップショットに対するチェックが行われます。 DBCC コマンドの完了後、このスナップショットは削除されます。
  
内部データベース スナップショットが必要ではない場合や、内部データベース スナップショットを作成できない場合、 DBCC コマンドは実際のデータベースに対して実行されます。 データベースがオンラインの場合、DBCC コマンドではテーブルロックを使用して、チェックするオブジェクトの一貫性を確保します。 この動作は、WITH TABLOCK オプションが指定される場合と同じです。
  
次の条件で DBCC コマンドを実行する場合、内部データベース スナップショットは作成されません。
-   **master** に対して実行する場合で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスがシングル ユーザー モードで実行されている場合。  
-   **master** 以外のデータベースに対して実行する場合で、データベースが ALTER DATABASE ステートメントによってシングル ユーザー モードに設定されている場合。  
-   読み取り専用データベースに対して実行する場合。  
-   ALTER DATABASE ステートメントによって緊急モードに設定されたデータベースに対して実行する場合。  
-   **tempdb** に対して実行する場合。 この場合、内部的な制約のため、データベース スナップショットは作成できません。  
-   WITH TABLOCK オプションを使用する場合。 この場合、DBCC ではデータベース スナップショットは作成されず、要求が受け入れられます。  
  
DBCC コマンドを次の対象に実行する場合は、内部データベース スナップショットの代わりにテーブル ロックが使用されます。
-   読み取り専用のファイル グループ  
-   FAT ファイル システム  
-   "名前付きストリーム" がサポートされないボリューム  
-   "代替ストリーム" がサポートされないボリューム  
  
> [!NOTE]  
>  WITH TABLOCK オプションを使用して、DBCC CHECKALLOC を実行する場合、または DBCC CHECKDB の同様な機能を実行する場合は、データベースの排他 (X) ロックが必要です。 このデータベース ロックは **tempdb** または **master** に対しては設定できず、他のすべてのデータベースでも失敗する可能性があります。  
  
> [!NOTE]  
>  DBCC CHECKDB を **master** に対して実行した場合、内部データベース スナップショットが作成できないと DBCC CHECKDB は失敗します。  
  
## <a name="progress-reporting-for-dbcc-commands"></a>DBCC コマンドの進行状況レポート  
**sys.dm_exec_requests** カタログ ビューには、DBCC CHECKDB、DBCC CHECKFILEGROUP、DBCC CHECKTABLE コマンドの実行の進行状況と現在のフェーズについての情報が格納されます。 **percent_complete** 列にはコマンドの完了率が示され、**command** 列にはコマンド実行の現在のフェーズがレポートされます。
  
レポートされる進行状況のレベルは、DBCC コマンド実行の現在のフェーズによって異なります。 たとえば、フェーズによって、進行状況がデータベース ページ レベルでレポートされる場合と、データベース レベルまたはアロケーション修復レベルでレポートされる場合があります。 次の表は、実行の各フェーズと、コマンドでレポートされる進行状況のレベルです。
  
|実行フェーズ|[説明]|進行状況レポートの単位|  
|---------------------|-----------------|------------------------------------|  
|DBCC TABLE CHECK|このフェーズでは、データベースのオブジェクトの論理的および物理的な一貫性がチェックされます。|進行状況はデータベース ページ レベルでレポートされます。<br /><br /> 進行状況レポートの値は、1,000 データベース ページがチェックされるたびに更新されます。|  
|DBCC TABLE REPAIR|このフェーズでは、REPAIR_FAST、REPAIR_REBUILD、または REPAIR_ALLOW_DATA_LOSS が指定され、修復が必要なオブジェクト エラーがある場合に、データベース修復が実行されます。|進行状況は個々の修復レベルでレポートされます。<br /><br /> カウンターは修復が完了するたびに更新されます。|  
|DBCC ALLOC CHECK|このフェーズでは、データベースの割り当て構造がチェックされます。<br /><br /> 注:DBCC CHECKALLOC でも同じチェックが実行されます。|進行状況はレポートされません。|  
|DBCC ALLOC REPAIR|このフェーズでは、REPAIR_FAST、REPAIR_REBUILD、または REPAIR_ALLOW_DATA_LOSS が指定され、修復が必要なアロケーション エラーがある場合に、データベース修復が実行されます。|進行状況はレポートされません。|  
|DBCC SYS CHECK|このフェーズでは、データベース システム テーブルがチェックされます。|進行状況はデータベース ページ レベルでレポートされます。<br /><br /> 進行状況レポートの値は、1,000 データベース ページがチェックされるたびに更新されます。|  
|DBCC SYS REPAIR|このフェーズでは、REPAIR_FAST、REPAIR_REBUILD、または REPAIR_ALLOW_DATA_LOSS が指定され、修復が必要なシステム テーブル エラーがある場合に、データベース修復が実行されます。|進行状況は個々の修復レベルでレポートされます。<br /><br /> カウンターは修復が完了するたびに更新されます。|  
|DBCC SSB CHECK|このフェーズでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Broker オブジェクトがチェックされます。<br /><br /> 注:このフェーズは、DBCC CHECKTABLE を実行した場合は実行されません。|進行状況はレポートされません。|  
|DBCC CHECKCATALOG|このフェーズでは、データベース カタログの一貫性がチェックされます。<br /><br /> 注:このフェーズは、DBCC CHECKTABLE を実行した場合は実行されません。|進行状況はレポートされません。|  
|DBCC IVIEW CHECK|このフェーズでは、データベースに存在するインデックス付きビューの論理的な一貫性がチェックされます。|進行状況は、チェックされたデータベース ビュー レベルでレポートされます。|  
  
## <a name="informational-statements"></a>情報ステートメント  
  
|||  
|-|-|  
|[DBCC INPUTBUFFER](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)|[DBCC SHOWCONTIG](../../t-sql/database-console-commands/dbcc-showcontig-transact-sql.md)|  
|[DBCC OPENTRAN](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)|[DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)|  
|[DBCC OUTPUTBUFFER](../../t-sql/database-console-commands/dbcc-outputbuffer-transact-sql.md)|[DBCC TRACESTATUS](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)|  
|[DBCC PROCCACHE](../../t-sql/database-console-commands/dbcc-proccache-transact-sql.md)|[DBCC USEROPTIONS](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)|  
|[DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)||  
  
## <a name="validation-statements"></a>検証ステートメント  
  
|||  
|-|-|  
|[DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)|[DBCC CHECKFILEGROUP](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)|  
|[DBCC CHECKCATALOG](../../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md)|[DBCC CHECKIDENT](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)|  
|[DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md)|[DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)|  
|[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)||  
  
## <a name="maintenance-statements"></a>メンテナンス ステートメント  
  
|||  
|-|-|  
|[DBCC CLEANTABLE](../../t-sql/database-console-commands/dbcc-cleantable-transact-sql.md)|[DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md)|  
|[DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)|[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)|  
|[DBCC DROPCLEANBUFFERS](../../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)|[DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)|  
|[DBCC FREEPROCCACHE](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)|[DBCC UPDATEUSAGE](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)|  
  
## <a name="miscellaneous-statements"></a>その他のステートメント  
  
|||  
|-|-|  
|[DBCC dllname (FREE)](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)|[DBCC HELP](../../t-sql/database-console-commands/dbcc-help-transact-sql.md)|  
|[DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)|[DBCC TRACEOFF](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)|  
|[DBCC FREESESSIONCACHE](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)|[DBCC TRACEON](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)|  
|[DBCC FREESYSTEMCACHE](../../t-sql/database-console-commands/dbcc-freesystemcache-transact-sql.md)|[DBCC CLONEDATABASE](../../t-sql/database-console-commands/dbcc-clonedatabase-transact-sql.md) <br /><br /> **適用対象**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 以降。|  
  
  
