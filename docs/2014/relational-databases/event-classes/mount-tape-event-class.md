---
title: Mount Tape イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Mount Tape event class
ms.assetid: 4c595e0a-d968-47d3-a84f-9b6857342671
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 513792c12833a14b8d1d3fc78f4b3bb6be173627
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63023450"
---
# <a name="mount-tape-event-class"></a>Mount Tape イベント クラス
  Mount Tape イベント クラスは、テープのマウント要求を受け取ったときに発生します。 テープのマウント要求およびその要求の成功と失敗を監視するには、このイベント クラスを使用します。  
  
## <a name="mount-tape-event-class-data-columns"></a>Mount Tape イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、アプリケーションによって渡された値が格納されます。|10|はい|  
|ClientProcessID|`int`|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによりクライアント プロセス ID が指定されると、このデータ列に値が格納されます。|9|はい|  
|DatabaseID|`int`|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|`nvarchar`|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|Duration|`bigint`|イベントにかかった時間 (マイクロ秒)。|13|はい|  
|EndTime|`datetime`|マウント要求イベントでは、タイムアウトが発生した場合はマウント タイムアウトの時刻、それ以外の場合はイベント自体の発生時刻です (この場合、StartTime が対応するマウント要求の時刻を示します)。|15|はい|  
|EventClass|`int`|イベントの種類 = 195。|27|いいえ|  
|EventSequence|`int`|要求内の特定のイベントのシーケンス。|51|いいえ|  
|EventSubClass|`int`|イベント サブクラスの種類。<br /><br /> 1 = テープのマウント要求<br /><br /> 2 = テープのマウント完了<br /><br /> 3 = テープのマウント取り消し|21|はい|  
|GroupID|`int`|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|HostName|`nvarchar`|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|IsSystem|`int`|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|[はい]|  
|LoginName|`nvarchar`|ユーザーのログイン名 (DOMAIN [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] username [!INCLUDE[msCoName](../../includes/msconame-md.md)] の形式で表された\\*セキュリティ ログインまたは*Windows ログイン資格情報)。|11|はい|  
|NTDomainName|`nvarchar`|ユーザーが所属する Windows ドメイン。|7|はい|  
|NTUserName|`nvarchar`|Windows のユーザー名。|6|はい|  
|ServerName|`nvarchar`|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|SessionLoginName|`nvarchar`|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|SPID|`int`|イベントが発生したセッションの ID。|12|はい|  
|StartTime|`datetime`|イベントの開始時刻 (取得できた場合)。|14|はい|  
|TextData|`ntext`|*physical device name* [ ( *logical device name* ) ]. 論理デバイス名は、sys.backup_devices カタログ ビューで定義されている場合のみ表示されます。|1|はい|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [SQL Server データベースのバックアップと復元](../backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
