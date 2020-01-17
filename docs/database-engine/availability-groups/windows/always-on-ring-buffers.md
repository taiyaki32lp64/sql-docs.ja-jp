---
title: 可用性グループの正常性情報のリング バッファー
description: SQL Server リング バッファーを使用し、Always On 可用性グループに関する特定の診断情報を取得します。
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 47bb7a1a-c0a5-473c-a7db-d9f4bf3ee650
author: rothja
ms.author: jroth
ms.openlocfilehash: c52e0bcb34c93bb3c973caae53d3983db3660e24
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822115"
---
# <a name="use-ring-buffers-to-obtain-health-information-about-always-on-availability-groups"></a>リング バッファーを使用し、Always On 可用性グループに関する正常性情報を取得する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  いくつかの Always On 可用性グループの診断情報を SQL Server のリング バッファー、または sys.dm_os_ring_buffers 動的管理ビュー (DMV) から入手できます。 リング バッファーは、SQL Server の起動中に作成され、内部診断用に SQL Server システム内のアラートを記録します。 それらはサポートされていませんが、問題のトラブルシューティングを行うときにそれらから貴重な情報を抽出することができます。 これらのリング バッファーは、SQL Server がハングまたはクラッシュしたときに別の診断のソースを提供します。  
  
 次の Transact-SQL (T-SQL) クエリでは、可用性グループのリング バッファーからすべてのイベント レコードを取得します。  
  
```sql  
SELECT * FROM sys.dm_os_ring_buffers WHERE ring_buffer_type LIKE '%HADR%'  
```  
  
 データをより管理しやすくするには、日付とリング バッファーの種類によって、データをフィルター処理します。 次のクエリは、今日発生した指定したリング バッファーからレコードを取得します。  
  
```sql  
DECLARE @runtime datetime  
SET @runtime = GETDATE()  
SELECT CONVERT (varchar(30), @runtime, 121) as data_collection_runtime,   
DATEADD (ms, -1 * (inf.ms_ticks - ring.[timestamp]), GETDATE()) AS ring_buffer_record_time,   
ring.[timestamp] AS record_timestamp, inf.ms_ticks AS cur_timestamp, ring.*   
FROM sys.dm_os_ring_buffers ring  
CROSS JOIN sys.dm_os_sys_info inf where ring_buffer_type='<RING_BUFFER_TYPE>'  
```  
  
 各レコードの Record 列には、XML 形式の診断データが含まれています。 XML データは、リング バッファーの種類によって異なります。 各リング バッファーの種類の詳細については、「[可用性グループのリング バッファーの種類](#BKMK_RingBufferTypes)」を参照してください。 XML データを読みやすくするには、目的の XML 要素を抽出するように T-SQL クエリをカスタマイズする必要があります。 たとえば、次のクエリは、RING_BUFFER_HADRDBMGR_API リング バッファーからすべてのイベントを取得し、別のテーブルの列に XML データを書式設定します。  
  
```sql  
WITH hadr(ts, type, record) AS  
(  
  SELECT timestamp AS ts, ring_buffer_type AS type, CAST(record AS XML) AS record   
  FROM sys.dm_os_ring_buffers WHERE ring_buffer_type = 'RING_BUFFER_HADRDBMGR_API'  
)  
SELECT   
  ts,  
  type,  
  record.value('(./Record/@id)[1]','bigint') AS [Record ID],  
  record.value('(./Record/@time)[1]','bigint') AS [Time],  
  record.value('(./Record/HadrDbMgrAPI/dbId)[1]', 'bigint') AS [DBID],  
  record.value('(/Record/HadrDbMgrAPI/API)[1]', 'varchar(50)') AS [API],  
  record.value('(/Record/HadrDbMgrAPI/Action)[1]', 'varchar(50)') AS [Action],  
  record.value('(/Record/HadrDbMgrAPI/role)[1]', 'int') AS [Role],  
  record.value('(/Record/Stack)[1]', 'varchar(100)') AS [Call Stack]  
FROM hadr  
ORDER BY record.value('(./Record/@time)[1]','bigint') DESC  
GO  
```  
  
##  <a name="BKMK_RingBufferTypes"></a> 可用性グループのリング バッファーの種類  
 sys.dm_os_ring_buffers に 4 つの可用性グループ リング バッファーがあります。 次の表は、リング バッファーの種類と、それぞれのリング バッファーの種類の Record 列のコンテンツのサンプルについて説明しています。  
  
 **RING_BUFFER_HADRDBMGR_API**  
  
 発生したまたは発生している状態遷移を記録します。 状態遷移を見るときには、objectType の値に十分注意してください。  
  
```xml  
<Record id="11" type="RING_BUFFER_HADRDBMGR_STATE" time="860243">  
  <HadrDbMgrState>  
    <objectType>HadrUsers</objectType>  
    <currentState>HDbMState_Starting</currentState>  
    <proposedState>HDbMState_Started</proposedState>  
    <targetState>HDbMState_Started</targetState>  
    <legalTransition>Y</legalTransition>  
    <role>1</role>  
  </HadrDbMgrState>  
</Record>  
```  
  
 **RING_BUFFER_HADRDBMGR_STATE**  
  
 Always On アクティビティによって実行された内部メソッドまたは関数呼び出しを記録します。 開始ポイントと終了ポイントの両方を含めて中断、再開、役割の変更などの情報を表示できます。  
  
```xml  
<Record id="45" type="RING_BUFFER_HADRDBMGR_STATE" time="1723487912">  
  <HadrDbMgrState>  
    <dbId>5</dbId>  
    <objectType>HadrDbMgr</objectType>  
    <currentState>HDbMState_Starting</currentState>  
    <proposedState>HDbMState_Started</proposedState>  
    <targetState>HDbMState_Started</targetState>  
    <legalTransition>Y</legalTransition>  
    <role>2</role>  
  </HadrDbMgrState>  
</Record>  
```  
  
 **RING_BUFFER_HADRDBMGR_COMMIT**  
  
```xml  
<Record id="0" type="RING_BUFFER_HADRDBMGR_COMMIT" time="1723475368">  
  <HadrDbMgrCommitPolicy>  
    <dbId>5</dbId>  
    <replicaId>883a18f5-97d5-450f-8f8f-9983a4fa5299</replicaId>  
    <dbHardenPolicy>KillAll</dbHardenPolicy>  
    <dbSyncConfig>0x0</dbSyncConfig>  
    <syncPartnerCount>0</syncPartnerCount>  
    <minSyncPartnerConfig>0</minSyncPartnerConfig>  
    <partnerHardenPolicy>KillAll</partnerHardenPolicy>  
    <partnerSyncConfig>0x0</partnerSyncConfig>  
    <logBlock>0x0000000000000000</logBlock>  
    <leaseExpired>Y</leaseExpired>  
    <partnerChange>N</partnerChange>  
    <role>2</role>  
  </HadrDbMgrCommitPolicy>  
</Record>  
```  
  
 **RING_BUFFER_HADR_TRANSPORT_STATE**  
  
```xml  
<Record id="3" type="RING_BUFFER_HADR_TRANSPORT_STATE" time="1723485399">  
  <HadrTransportState>  
    <agId>08264B79-D10B-412F-B38D-CA07B08E9BD8</agId>  
    <localArId>883A18F5-97D5-450F-8F8F-9983A4FA5299</localArId>  
    <targetArId>628D6349-72DD-4D18-A6E1-1272645660BA</targetArId>  
    <currentState>HadrSession_Configuring</currentState>  
    <targetState>HadrSession_Connected</targetState>  
    <legalTransition>Y</legalTransition>  
  </HadrTransportState>  
</Record>  
```  
  
## <a name="parse-xml-data-from-a-ring-buffer"></a>リング バッファーからの XML データを解析します。  
 クエリで [value&#40;&#41; メソッド &#40;xml データ型 &#41;](~/t-sql/xml/value-method-xml-data-type.md) を使用して、調査しているリング バッファーからの Record フィールドを解析することができます。 このメソッドを使用するには、最初に、リング バッファー内の Record 列を XML に[キャスト](~/t-sql/functions/cast-and-convert-transact-sql.md)する必要があります。 たとえば、次のクエリは、このメソッドを使用して、RING_BUFFER_HADRDBMGR_API を読み取り可能な形式に解析する方法を示しています。  
  
```sql 
WITH hadr(ts, type, record) AS  
   (SELECT timestamp AS ts, ring_buffer_type AS type, CAST(record AS XML) AS record   
FROM sys.dm_os_ring_buffers   
WHERE ring_buffer_type = 'RING_BUFFER_HADRDBMGR_API')  
SELECT ts,  
type,  
record.value('(./Record/@id)[1]','bigint') AS [Record id],  
record.value('(./Record/@time)[1]','bigint') AS [Time],  
record.value('(./Record/HadrDbMgrAPI/dbId)[1]', 'bigint') AS [dbid],  
record.value('(/Record/HadrDbMgrAPI/API)[1]', 'varchar(50)') AS [API],  
record.value('(/Record/HadrDbMgrAPI/Action)[1]', 'varchar(50)') AS [Action],  
record.value('(/Record/HadrDbMgrAPI/role)[1]', 'int') AS [Role],  
record.value('(/Record/Stack)[1]', 'varchar(100)') AS [Call Stack]  
FROM hadr  
ORDER BY record.value('(./Record/@time)[1]','bigint') DESC  
GO  
```  
  
  
