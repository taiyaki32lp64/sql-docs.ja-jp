---
title: イベント ファイル ターゲット |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- event file target
- file target [SQL Server extended events]
- targets [SQL Server extended events], file target
ms.assetid: 4f0ee6ec-a0a8-4c38-aa61-8293ab6ac7fd
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 53cf3aa4b23484bb22f4237fbf61874990381067
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66064860"
---
# <a name="event-file-target"></a>Event File Target
  イベント ファイル ターゲットは、完全なバッファーをディスクに書き込むターゲットです。  
  
 次の表では、イベント ファイル ターゲットの構成に使用できるオプションについて説明します。  
  
|オプション|指定できる値|説明|  
|------------|--------------------|-----------------|  
|filename|260 文字までの任意の文字列。 この値は必須です。|ファイルの場所とファイル名。<br /><br /> 任意のファイル名拡張子を使用できます。|  
|max_file_size|任意の 64 ビット整数。 この値は省略可能です。|ファイルの最大サイズ (MB)。 max_file_size を指定しない場合、ファイルはディスクがいっぱいになるまで拡張されます。 既定のファイル サイズは 1 GB です。<br /><br /> max_file_size は、セッション バッファーの現在のサイズを超えるサイズである必要があります。 そうでないと、ファイル ターゲットの初期化が失敗し、max_file_size が無効であるとレポートされます。 バッファーの現在のサイズを表示するには、 [sys.dm_xe_sessions](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql) 動的管理ビューで buffer_size 列に対するクエリを発行します。<br /><br /> 既定のファイル サイズがセッション バッファー サイズ未満の場合は、max_file_size を、 [sys.server_event_sessions](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql) カタログ ビューの max_memory 列に指定された値に設定することをお勧めします。<br /><br /> max_file_size をセッション バッファーのサイズを超えて設定した場合、セッション バッファーのサイズの最も近い倍数に丸められたサイズが使用されます。 その結果、max_file_size に指定した値に満たないターゲット ファイルが作成されることがあります。 たとえば、バッファー サイズが 100 MB のときに max_file_size を 150 MB に設定した場合、2 番目のバッファーが残りの 50 MB のスペースに収まらないため、結果のファイル サイズは 100 MB に丸められます。<br /><br /> 既定のファイル サイズがセッション バッファー サイズ未満の場合は、max_file_size を、 [sys.server_event_sessions](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql) カタログ ビューの max_memory 列の値に設定することをお勧めします。|  
|max_rollover_files|任意の 32 ビット整数。 この値は省略可能です。|ファイル システム内に保持するファイルの最大数。 既定値は 5 です。|  
|increment|任意の 32 ビット整数。 この値は省略可能です。|ファイルの拡張増分値 (MB)。 指定しない場合、増分の既定値はセッション バッファー サイズの 2 倍になります。|  
  
 イベント ファイル ターゲットが初めて作成されるとき、指定したファイル名に _0\_ と長整数値が付加されます。 整数値は 1601 年 1 月 1 日の間のミリ秒数として計算され、ファイルが作成された日付と時刻。 後続のロールオーバー ファイルでもこの形式が使用されます。 長整数値を調べることで、最新のファイルを判別できます。 次の例は、filename オプションに C:\OutputFiles\MyOutput.xel と指定した場合のファイルの名前の決定方法を示しています。  
  
-   最初に作成されるファイル: C:\OutputFiles\MyOutput_0_128500310259380000.xel  
  
-   最初のロールオーバー ファイル : C:\OutputFiles\MyOutput_0_128505831770890000.xel  
  
-   2 番目のロールオーバー ファイル: C:\OutputFiles\MyOutput_0_132410772966237000.xel  
  
## <a name="adding-the-target-to-a-session"></a>セッションへのターゲットの追加  
 イベント ファイル ターゲットを拡張イベント セッションに追加するには、イベント セッションの作成時または変更時に次のいずれかのステートメントを含めます。 *file_name* を目的のファイル名とパスに置き換えてください。  
  
```  
ADD TARGET package0.event_file(  
   SET filename='file_name.xel')  
```  
  
## <a name="reviewing-the-target-output"></a>ターゲット出力の確認  
 ターゲット ファイルからの出力を確認するには、sys.fn_xe_file_target_read_file 関数を使用する必要があります。 データを XML としてキャストすることをお勧めします。 次の構文を使用できます。 *file_name* を、ターゲットの追加時に指定したファイル名とパスに置き換えてください。  
  
```  
SELECT *, CAST(event_data AS XML) AS 'event_data_XML'  
FROM sys.fn_xe_file_target_read_file('file_name*.xel', NULL, NULL, NULL)  
```  
  
## <a name="see-also"></a>関連項目  
 [SQL Server 拡張イベント ターゲット](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.fn_xe_file_target_read_file &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql)   
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
