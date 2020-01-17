---
title: Broker:Message Classify イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Broker:Message Classify event class
ms.assetid: e51f3351-1239-4c41-b87c-1dd86968e027
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f0d3219271483ffbd4d5c51d1f382b3277086521
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67999650"
---
# <a name="brokermessage-classify-event-class"></a>Broker:Message Classify イベント クラス

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、Service Broker によりメッセージのルーティングが決定されると、 **Broker:Message Classify** イベントを生成します。  
  
## <a name="brokermessage-classify-event-class-data-columns"></a>Broker:Message Classify イベント クラスのデータ列  
  
|データ列|データ型|[説明]|列番号|フィルターの適用|  
|-----------------|---------------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|**ClientProcessID**|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターによって割り当てられた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|はい|  
|**DatabaseID**|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|**EventClass**|**int**|キャプチャされたイベント クラスの種類。 **Broker:Message Classify** の場合は、常に **141**です。|27|いいえ|  
|**EventSequence**|**int**|このイベントのシーケンス番号。|51|いいえ|  
|**EventSubClass**|**nvarchar**|イベント サブクラスの種類です。各イベント クラスについての詳細な情報を提供します。 この列は次の値を含むことができます。<br /><br /> **Local**: 選択されるルートには LOCAL アドレスが含まれます。<br /><br /> **Remote**:                選択されるルートには、LOCAL 以外のアドレスが含まれます。<br /><br /> **Delayed**:                転送が無効か、一致するルートが存在しないため、メッセージが遅延されます。|21|はい|  
|**FileName**|**nvarchar**|メッセージ送信先のサービス名。|36|いいえ|  
|**GUID**|**uniqueidentifier**|ダイアログのメッセージ交換 ID。 この ID はメッセージの一部として転送され、メッセージ交換の両側で共有されます。|54|いいえ|  
|**HostName**|**nvarchar**|クライアントが実行しているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|いいえ|  
|**LoginSid**|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|**NTDomainName**|**nvarchar**|ユーザーが属している Windows ドメイン。|7|はい|  
|**NTUserName**|**nvarchar**|このイベントが生成された接続を所有するユーザーの名前。|6|はい|  
|**OwnerName**|**nvarchar**|メッセージ送信先のブローカー ID。|37|いいえ|  
|**RoleName**|**nvarchar**|メッセージをネットワークから受信したか、またはこの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスから発信したかを示します。|38|いいえ|  
|**ServerName**|**nvarchar**|トレースされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|**SPID**|**int**|クライアントに関連付けられているプロセスに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって割り当てられているサーバー プロセス ID。|12|はい|  
|**Start Time**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**TargetUserName**|**nvarchar**|次のホップ ブローカーのネットワーク アドレス。|39|いいえ|  
|**TransactionID**|**bigint**|トランザクションに対してシステムが割り当てた ID。|4|いいえ|  
  
## <a name="see-also"></a>参照  
 [SQL Server Service Broker (SQL Server Service Broker)](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
