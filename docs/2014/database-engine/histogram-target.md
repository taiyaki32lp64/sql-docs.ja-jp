---
title: ヒストグラム ターゲット |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- bucketing target [SQL Server extended events]
- event bucketing target
- targets [SQL Server extended events], bucketing
ms.assetid: 2ea39141-7eb0-4c74-abf8-114c2c106a19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a584311061a24d674eed114f37d9cbbbda43909
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66064700"
---
# <a name="histogram-target"></a>ヒストグラムのターゲット
  ヒストグラム ターゲットは、イベント データに基づいて、特定の種類のイベントの発生をグループ化します。 イベントのグループは、指定されたイベント列またはアクションに基づいてカウントされます。 ヒストグラム ターゲットを使用して、パフォーマンス上の問題のトラブルシューティングを行うことができます。 どのイベントが最もよく発生するかを識別することで、パフォーマンス上の問題を引き起こす可能性を示す "ホットスポット" を見つけることができます。  
  
 次の表では、ヒストグラム ターゲットの構成に使用できるオプションについて説明します。  
  
|オプション|指定できる値|説明|  
|------------|--------------------|-----------------|  
|slots|任意の整数値。 この値は省略可能です。|保持するグループの最大数を示すユーザー指定の値。 この値に達した場合、既存のグループに属していない新しいイベントは無視されます。<br /><br /> パフォーマンス向上のために、スロット数は 2 の次の累乗に切り上げられます。|  
|filtering_event_name|拡張イベント セッション内に存在するすべてのイベント。 この値は省略可能です。|イベントのクラスを識別するためのユーザー指定の値。 指定されたイベントのインスタンスだけがバケット化されます。 それ以外のすべてのイベントは無視されます。<br /><br /> この値は、 *package_name*.*event_name*形式で指定する必要があります &#40;例: `'sqlserver.checkpoint_end'`&#41;。 次のクエリを使用すると、パッケージ名を特定できます。<br /><br /> SELECT p.name, se.event_name<br />FROM sys.dm_xe_session_events se<br />Sys.dm_xe_packages p を参加させる<br />ON se_event_package_guid = p.guid<br />ORDER BY p.name, se.event_name<br /><br /> <br /><br /> filtering_event_name 値を指定しない場合は、source_type を 1 (既定値) に設定する必要があります。|  
|source_type|バケットの基になっているオブジェクトの種類。 この値は省略可能で、指定しない場合は既定値 1 が使用されます。|次のいずれかの値になります。<br /><br /> 0 (イベントの場合)<br /><br /> 1 (アクションの場合)|  
|source|イベント列またはアクション名。|データ ソースとして使用されるイベント列またはアクション名です。<br /><br /> source に対してイベント列を指定する場合は、filtering_event_name 値に使用されているイベントの列を指定する必要があります。 次のクエリを使用すると、使用できる列を特定できます。<br /><br /> SELECT name FROM sys.dm_xe_object_columns<br />WHERE object_name = '\<eventname >'<br />AND column_type != 'readonly'<br /><br /> source に対してイベント列を指定する場合は、パッケージ名を source 値に含める必要はありません。<br /><br /> source に対してアクション名を指定する場合は、このターゲットが使用されているイベント セッションのコレクションに対して構成されているいずれかのアクションを使用する必要があります。 アクション名に使用できる値を調べるには、sys.dm_xe_sesssion_event_actions ビューの action_name 列に対するクエリを実行します。<br /><br /> アクション名をデータ ソースとして使用している場合は、 *package_name*.*action_name*形式で source 値を指定する必要があります。|  
  
 次の例では、ヒストグラム ターゲットによるデータ収集のしくみの概要を示します。 この例では、ヒストグラム ターゲットを使用して、待機が何回発生したかを待機の種類別にカウントします。 この場合、ヒストグラム ターゲットを定義するときに次のオプションを指定します。  
  
-   filtering_event_name = 'wait_info'  
  
-   source = 'wait_type'  
  
-   source_type = 0 (wait_type がイベント列のため)  
  
 この例のシナリオでは、wait_type ソースに対して次のデータが記録されます。  
  
|フィルター イベント名|ソース列値|  
|--------------------------|-------------------------|  
|wait_info|file_io|  
|wait_info|file_io|  
|wait_info|ネットワーク|  
|wait_info|ネットワーク|  
|wait_info|スリープ (sleep)|  
  
 待機の種類値は、次の値とスロット数を持つ 3 つのスロットに分類されます。  
  
|値|スロット数|  
|-----------|----------------|  
|file_io|2|  
|ネットワーク|2|  
|スリープ (sleep)|1|  
  
 ヒストグラム ターゲットによって保持されるのは、指定されたソースのイベント データだけです。 イベント データが大きすぎて全体を保持することができない場合もあります。その場合は、データが切り捨てられます。 イベント データが切り捨てられた場合、バイト数が記録されて、XML 出力として表示されます。  
  
## <a name="adding-the-target-to-a-session"></a>セッションへのターゲットの追加  
 ヒストグラム ターゲットを拡張イベント セッションに追加するには、目的のターゲットの種類に応じて、イベント セッションの作成時または変更時に次のいずれかのステートメントを含める必要があります。  
  
```  
ADD TARGET package0.histogram  
```  
  
 SET ステートメントを使用して、さまざまなオプションを設定できます。 次の例では、sqlserver.checkpoint_end イベントのデータを収集するヒストグラム ターゲットの追加方法を示しています。  
  
```  
ADD TARGET package0.histogram  
(SET slots = 32, filtering_event_name = 'sqlserver.checkpoint_end', source_type = 0, source = 'database_id')  
```  
  
 詳細については、「[ロックの大半を取得しているオブジェクトを見つける](../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)」と「[拡張イベントを使用したシステムの使用状況の監視](../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)」を参照してください。  
  
## <a name="reviewing-the-target-output"></a>ターゲット出力の確認  
 ヒストグラム ターゲットは、呼び出し元のプログラムまたはプロシージャに対するデータを XML 形式でシリアル化します。 ターゲット出力は、いずれのスキーマにも準拠しません。  
  
 ヒストグラム ターゲットの出力を確認するには、次のクエリを使用します。 *session_name* をイベント セッションの名前に置き換えてください。  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 次の例は、ヒストグラム ターゲットの出力形式を示しています。  
  
```  
<Slots truncated = "0" buckets=[count]>  
    <Slot count=[count] trunc=[truncated bytes]>  
        <value>  
        </value>  
    </Slot>  
</Slots>  
```  
  
## <a name="see-also"></a>関連項目  
 [SQL Server 拡張イベント ターゲット](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
