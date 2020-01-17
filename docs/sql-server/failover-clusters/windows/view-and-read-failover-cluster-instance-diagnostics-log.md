---
title: フェールオーバー クラスター インスタンスの診断ログを表示して読む方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 68074bd5-be9d-4487-a320-5b51ef8e2b2d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0932181110c5c4ec34e3d4bdf6b1395bffc65cca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904990"
---
# <a name="view-and-read-failover-cluster-instance-diagnostics-log"></a>フェールオーバー クラスター インスタンスの診断ログを表示して読む方法
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server Resource DLL のすべての重大なエラーと警告イベントが、Windows イベント ログに書き込まれます。 [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) システム ストアド プロシージャによってキャプチャされる SQL Server に固有の診断情報の実行ログは、SQL Server フェールオーバー クラスター診断ログ ファイル (*SQLDIAG* ログとも呼ばれます) に書き込まれます。  
  
-   **作業を開始する準備:** [推奨事項](#Recommendations)、[セキュリティ](#Security)  
  
-   **診断ログを表示するには、次を使用:** [SQL Server Management Studio](#SSMSProcedure)、[Transact-SQL](#TsqlProcedure)  
  
-   **診断ログ設定を構成するには、次を使用:** [Transact-SQL](#TsqlConfigure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Recommendations"></a> 推奨事項  
 既定では、SQLDIAG は、SQL Server インスタンス ディレクトリのローカル ログ フォルダーに保存されます。たとえば、AlwaysOn フェールオーバー クラスター インスタンス (FCI) の所有元ノードの "C\Program Files\Microsoft SQL Server\MSSQL13.\<InstanceName>\MSSQL\LOG" です。 各 SQLDIAG ログ ファイルのサイズは 100 MB に固定されています。 10 個のログ ファイルがコンピューターに格納された後、新しいログとして再利用されます。  
  
 ログには、拡張イベント ファイル形式が使用されます。 **sys.fn_xe_file_target_read_file** システム関数は、拡張イベントによって作成されるファイルの読み取りに使用することができます。 行ごとに、XML 形式の 1 つのイベントが返されます。 XML データを結果セットとして解析するには、システム ビューに対してクエリを実行します。 詳細については、「[sys.fn_xe_file_target_read_file &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 **fn_xe_file_target_read_file**を実行するには、VIEW SERVER STATE 権限が必要です。  
  
 SQL Server Management Studio を管理者として開きます。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **診断ログ ファイルを表示するには**  
  
1.  **[ファイル]** メニューから、 **[開く]** 、 **[ファイル]** を選択し、表示する診断ログ ファイルを選択します。  
  
2.  イベントは、右ペインに行として表示されます。既定では、 **名前**と **タイムスタンプ** の 2 つの列だけが表示されます。  
  
     また、 **[ExtendedEvents]** メニューがアクティブ化されます。  
  
3.  他の列を表示するには、 **[ExtendedEvents]** メニューにアクセスし、 **[列の選択]** を選択します。  
  
     ダイアログ ボックスが開き、表示対象として選択できる列が表示されます。  
  
4.  **[ExtendedEvents]** メニューを使用し、 **[フィルター]** オプションを選択することによって、イベント データをフィルター選択したり並べ替えたりすることができます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **診断ログ ファイルを表示するには**  
  
 SQLDIAG ログ ファイル内のすべてのログ アイテムを表示するには、次のクエリを使用します。  
  
```  
SELECT  
xml_data.value('(event/@name)[1]','varchar(max)') AS 'Name'  
,xml_data.value('(event/@package)[1]','varchar(max)') AS 'Package'  
,xml_data.value('(event/@timestamp)[1]','datetime') AS 'Time'  
,xml_data.value('(event/data[@name=''state'']/value)[1]','int') AS 'State'  
,xml_data.value('(event/data[@name=''state_desc'']/text)[1]','varchar(max)') AS 'State Description'  
,xml_data.value('(event/data[@name=''failure_condition_level'']/value)[1]','int') AS 'Failure Conditions'  
,xml_data.value('(event/data[@name=''node_name'']/value)[1]','varchar(max)') AS 'Node_Name'  
,xml_data.value('(event/data[@name=''instancename'']/value)[1]','varchar(max)') AS 'Instance Name'  
,xml_data.value('(event/data[@name=''creation time'']/value)[1]','datetime') AS 'Creation Time'  
,xml_data.value('(event/data[@name=''component'']/value)[1]','varchar(max)') AS 'Component'  
,xml_data.value('(event/data[@name=''data'']/value)[1]','varchar(max)') AS 'Data'  
,xml_data.value('(event/data[@name=''info'']/value)[1]','varchar(max)') AS 'Info'  
FROM  
 ( SELECT object_name AS 'event'  
  ,CONVERT(xml,event_data) AS 'xml_data'  
  FROM sys.fn_xe_file_target_read_file('C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log\SQLNODE1_MSSQLSERVER_SQLDIAG_0_129936003752530000.xel',NULL,NULL,NULL)   
)   
AS XEventData  
ORDER BY Time;  
  
```  
  
> [!NOTE]  
>  WHERE 句を使用して、特定のコンポーネントまたは状態の結果にフィルターを適用することができます。  
  
##  <a name="TsqlConfigure"></a> Transact-SQL の使用  
 **診断ログのプロパティを構成するには**  
  
> [!NOTE]  
>  この手順の例については、このセクションの後半の「 [例 (Transact-SQL)](#TsqlExample)」を参照してください。  
  
 データ定義言語 (DDL) ステートメント **ALTER SERVER CONFIGURATION** を使用すると、[sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) プロシージャによってキャプチャされた診断データのログ記録を開始または停止し、SQLDIAG ログの構成パラメーター (ログ ファイルのロールオーバー回数、ログ ファイルのサイズ、ファイルの場所など) を設定できます。 構文の詳細については、「 [Setting diagnostic log options](../../../t-sql/statements/alter-server-configuration-transact-sql.md#Diagnostic)」を参照してください。  
  
###  <a name="ConfigTsqlExample"></a> 例 (Transact-SQL)  
  
####  <a name="TsqlExample"></a> Setting diagnostic log options  
 このセクションの例では、診断ログ オプションの値を設定する方法を示します。  
  
##### <a name="a-starting-diagnostic-logging"></a>A. 診断ログの記録を開始する  
 次の例では、診断データのログ記録を開始します。  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG ON;  
```  
  
##### <a name="b-stopping-diagnostic-logging"></a>B. 診断ログの記録を停止する  
 次の例では、診断データのログ記録を停止します。  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG OFF;  
```  
  
##### <a name="c-specifying-the-location-of-the-diagnostic-logs"></a>C. 診断ログの場所を指定する  
 次の例では、診断ログの場所を、指定されたファイル パスに設定します。  
  
```  
ALTER SERVER CONFIGURATION  
SET DIAGNOSTICS LOG PATH = 'C:\logs';  
```  
  
##### <a name="d-specifying-the-maximum-size-of-each-diagnostic-log"></a>D. 各診断ログの最大サイズを指定する  
 次の例では、各診断ログの最大サイズを 10 MB に設定します。  
  
```  
ALTER SERVER CONFIGURATION   
SET DIAGNOSTICS LOG MAX_SIZE = 10 MB;  
```  
  
## <a name="see-also"></a>参照  
 [フェールオーバー クラスター インスタンスのフェールオーバー ポリシー](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)  
  
  
