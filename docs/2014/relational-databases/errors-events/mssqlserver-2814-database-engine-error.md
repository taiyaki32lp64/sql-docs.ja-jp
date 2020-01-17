---
title: MSSQLSERVER_2814 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2814 (Database Engine error)
ms.assetid: 22800748-9be9-4511-9428-6b8b40e5bef9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4c8def0fad1ae7eddb9de2e7206923b872c41ed2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "67046771"
---
# <a name="mssqlserver2814"></a>MSSQLSERVER_2814
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|2814|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PR_POSSIBLE_INFINITE_RECOMPILE|  
|メッセージ テキスト|SQLHANDLE %hs、PlanHandle %hs、開始オフセット %d、終了オフセット %d の再コンパイルが無限に行われる可能性があることが検出されました。 前回の再コンパイルの理由は、%d でした。|  
  
## <a name="explanation"></a>説明  
 1 つ以上のステートメントにより、クエリ バッチが少なくとも 50 回再コンパイルされました。 指定したステートメントを修正し、これ以上再コンパイルされるのを回避する必要があります。  
  
 次の表に、再コンパイルの理由を示します。  
  
|理由コード|説明|  
|-----------------|-----------------|  
|1|スキーマの変更|  
|2|統計の変更|  
|3|コンパイルの遅延|  
|4|Set オプションの変更|  
|5|Temp テーブルの変更|  
|6|リモート行セットの変更|  
|7|参照権限の変更|  
|8|クエリ通知環境の変更|  
|9|パーティション ビューの変更|  
|10|カーソル オプションの変更|  
|11|オプション (再コンパイル) の要求|  
  
## <a name="user-action"></a>ユーザーの操作  
  
1.  次のクエリを実行して、再コンパイルの原因になっているステートメントを確認します。 *sql_handle*、*starting_offset*、*ending_offset*、*plan_handle* の各プレースホルダーを、エラー メッセージで指定された値に置き換えます。 **database_name** 列と **object_name** 列は、アドホックおよび準備された [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは NULL になることに注意してください。  
  
     SELECT DB_NAME(st.dbid) AS database_name  
  
     , OBJECT_NAME(st.objectid) AS object_name  
  
     , st.text  
  
     FROM sys.dm_exec_query_stats AS qs  
  
     CROSS APPLY sys.dm_exec_sql_text (*sql_handle*) AS st  
  
     WHERE qs.statement_start_offset = *starting_offset*  
  
     AND qs.statement_end_offset = *ending_offset*  
  
     AND qs.plan_handle = *plan_handle*;  
  
2.  理由コードの説明に基づいて、再コンパイルを回避するようにステートメント、バッチ、またはプロシージャを修正します。 たとえば、ストアド プロシージャに 1 つ以上の SET ステートメントが含まれていることがあります。 これらのステートメントはプロシージャから削除する必要があります。 再コンパイルの理由と解決策のその他の例については、「[SQL Server 2005 のバッチのコンパイル、再コンパイル、およびプランのキャッシュに関する問題](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/administrator/cc966425(v=technet.10))」を参照してください。  
  
3.  問題が継続して発生する場合は、マイクロソフト カスタマー サポート サービスに問い合わせてください。  
  
## <a name="see-also"></a>関連項目  
 [SQL:StmtRecompile イベント クラス](../event-classes/sql-stmtrecompile-event-class.md)  
  
  
