---
title: SQL トレースのイベント クラスと等価な拡張イベントを確認する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- SQL Trace, extended events equivalents
- extended events [SQL Server], SQL Trace equivalents
- extended events [SQL Server], user configurable events
ms.assetid: 7f24104c-201d-4361-9759-f78a27936011
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0dd90613851184ad7fcff16ecf0a89875433dbfd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62512384"
---
# <a name="view-the-extended-events-equivalents-to-sql-trace-event-classes"></a>SQL トレースのイベント クラスと等価な拡張イベントを確認する
  拡張イベントを使用して、SQL トレース イベントのクラスや列に相当するイベント データを収集する場合、SQL トレース イベントが、拡張イベントのイベントおよびアクションとどのように対応しているかを理解しておくことが大切です。  
  
 SQL トレースのイベントとそれに関連した列について、拡張イベントにおける等価なイベントとアクションを確認するには、次の手順に従います。  
  
## <a name="to-view-the-extended-events-equivalents-to-sql-trace-events-using-query-editor"></a>クエリ エディターを使用して SQL トレース イベントと等価な拡張イベントを確認するには  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のクエリ エディターから、次のクエリを実行します。  
  
    ```  
    USE MASTER;  
    GO  
    SELECT DISTINCT  
       tb.trace_event_id,  
       te.name AS 'Event Class',  
       em.package_name AS 'Package',  
       em.xe_event_name AS 'XEvent Name',  
       tb.trace_column_id,  
       tc.name AS 'SQL Trace Column',  
       am.xe_action_name as 'Extended Events action'  
    FROM (sys.trace_events te LEFT OUTER JOIN sys.trace_xe_event_map em  
       ON te.trace_event_id = em.trace_event_id) LEFT OUTER JOIN sys.trace_event_bindings tb  
       ON em.trace_event_id = tb.trace_event_id LEFT OUTER JOIN sys.trace_columns tc  
       ON tb.trace_column_id = tc.trace_column_id LEFT OUTER JOIN sys.trace_xe_action_map am  
       ON tc.trace_column_id = am.trace_column_id  
    ORDER BY te.name, tc.name  
    ```  
  
 結果を確認する際は、次の点に注意してください。  
  
-   イベント クラス列を除くすべての列で NULL が返された場合、そのイベント クラスは SQL トレースから移行されなかったことを意味します。  
  
-   拡張イベント アクション列の値のみが NULL である場合、次のいずれかの条件に該当します。  
  
    -   SQL トレース列は、拡張イベントのイベントに関連付けられているいずれかのデータ フィールドに対応する。  
  
        > [!NOTE]  
        >  拡張イベントの各イベントは、結果セットに自動的に追加される既定のデータ フィールドのセットを持っています。  
  
    -   アクション列には、意味のある等価な拡張イベントが存在しない。 たとえば、SQL トレースの EventClass 列がこれに該当します。 同じ目的はイベント名によって満たされるため、拡張イベントにこの列は必要ありません。  
  
-   ユーザーが構成できる SQL トレースのイベント クラス (UserConfigurable:1 ～ UserConfigurable:9) は、拡張イベントでは単一のイベントに置き換えられます。 このイベントには、user_event という名前が付けられます。 このイベントは、SQL トレースと同じ sp_trace_generateevent ストアド プロシージャを使用して生成されます。 user_event イベントは、ストアド プロシージャに渡されたイベント ID に関係なく返されます。 ただし、event_id フィールドは、イベント データの一部として返されます。 これによって、イベント ID に基づく述語の作成が可能となります。 たとえば、UserConfigurable:0 (イベント ID = 82) をコード内で使用する場合、user_event イベントをセッションに追加し、'event_id = 82' という述語を指定することができます。 拡張イベントの user_event イベントも SQL トレースにおける等価なイベント クラスも sp_trace_generateevent ストアド プロシージャによって生成されるため、コードを変更する必要はありません。  
  
-   イベント クラス列を除くすべての列で NULL が返された場合、そのイベント クラスは SQL トレースから移行されなかったことを意味します。  
  
-   拡張イベント アクション列の値のみが NULL である場合、次のいずれかの条件に該当します。  
  
    -   SQL トレース列は、拡張イベントのイベントに関連付けられているいずれかのデータ フィールドに対応する。  
  
        > [!NOTE]  
        >  拡張イベントの各イベントは、結果セットに自動的に追加される既定のデータ フィールドのセットを持っています。  
  
    -   アクション列には、意味のある等価な拡張イベントが存在しない。 たとえば、SQL トレースの EventClass 列がこれに該当します。 同じ目的はイベント名によって満たされるため、拡張イベントにこの列は必要ありません。  
  
-   ユーザーが構成できる SQL トレースのイベント クラス (UserConfigurable:1 ～ UserConfigurable:9) は、拡張イベントでは単一のイベントに置き換えられます。 このイベントには、user_event という名前が付けられます。 このイベントは、SQL トレースと同じ sp_trace_generateevent ストアド プロシージャを使用して生成されます。 user_event イベントは、ストアド プロシージャに渡されたイベント ID に関係なく返されます。 ただし、event_id フィールドは、イベント データの一部として返されます。 これによって、イベント ID に基づく述語の作成が可能となります。 たとえば、UserConfigurable:0 (イベント ID = 82) をコード内で使用する場合、user_event イベントをセッションに追加し、'event_id = 82' という述語を指定することができます。 拡張イベントの user_event イベントも SQL トレースにおける等価なイベント クラスも sp_trace_generateevent ストアド プロシージャによって生成されるため、コードを変更する必要はありません。  
  
## <a name="see-also"></a>関連項目  
 [sp_trace_generateevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql)  
  
  
