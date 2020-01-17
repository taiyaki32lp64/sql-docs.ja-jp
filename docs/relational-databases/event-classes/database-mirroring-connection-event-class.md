---
title: Database Mirroring Connection イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: b59dccc9-f40d-4c82-aa35-ac40acea86ff
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b10bdc5786d87dedb2d4247dbffc6f7f9eda43fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68009565"
---
# <a name="database-mirroring-connection-event-class"></a>Database Mirroring Connection イベント クラス
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、 **Database Mirroring Connection** イベントを生成し、データベース ミラーリングによって管理されているトランスポート接続のステータスを報告します。  
  
## <a name="database-mirroringconnection-event-class-data-columns"></a>Database Mirroring:Connection イベント クラスのデータ列  
  
|データ列|型|[説明]|列番号|フィルターの適用|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|**ClientProcessID**|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターによって割り当てられた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|はい|  
|**DatabaseID**|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database*ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、 **DB_ID** 関数を使用して特定します。|3|はい|  
|**Error**|**int**|イベント内のテキストの、 **sys.messages** 内でのメッセージ ID 番号。 このイベントがエラーを報告する場合、この ID が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー番号となります。|31|いいえ|  
|**EventClass**|**int**|キャプチャされたイベント クラスの種類。 **Database Mirroring Connection** の場合は常に **151**。|27|いいえ|  
|**EventSequence**|**int**|このイベントのシーケンス番号。|51|いいえ|  
|**EventSubClass**|**nvarchar**|この接続の接続状態。 このイベントでは、サブクラスは次のいずれかの値になります。<br /><br /> **Connecting**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がトランスポート接続を開始しています。<br /><br /> **Connected**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がトランスポート接続を確立しました。<br /><br /> **Connect Failed**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がトランスポート接続を確立できませんでした。<br /><br /> **Closing**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がトランスポート接続を終了しています。<br /><br /> **Closed**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がトランスポート接続を終了しました。<br /><br /> **Accept**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が他のインスタンスからのトランスポート接続を許可しました。<br /><br /> **Send IO Error**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がメッセージの送信中にトランスポート エラーを検出しました。<br /><br /> **Receive IO Error**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がメッセージの受信中にトランスポート エラーを検出しました。|21|はい|  
|**GUID**|**uniqueidentifier**|この接続のエンドポイント ID。|54|いいえ|  
|**HostName**|**nvarchar**|クライアントが実行しているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、 **HOST_NAME** 関数を使用します。|8|はい|  
|**IntegerData**|**int**|この接続が閉じられた回数。|25|はい|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。<br /><br /> 0 = ユーザー<br /><br /> 1 = システム|60|いいえ|  
|**LoginSid**|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|**NTDomainName**|**nvarchar**|ユーザーが属している Windows ドメイン。|7|はい|  
|**NTUserName**|**nvarchar**|このイベントが生成された接続を所有するユーザーの名前。|6|はい|  
|**ObjectName**|**nvarchar**|ダイアログのメッセージ交換ハンドル。|34|いいえ|  
|**ServerName**|**nvarchar**|トレースされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|**SPID**|**int**|クライアントに関連付けられているプロセスに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって割り当てられているサーバー プロセス ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**TextData**|**ntext**|イベントに関係するエラー メッセージのテキスト。 エラーを報告しないイベントの場合、このフィールドは空です。 エラー メッセージは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー メッセージか Windows のエラー メッセージです。|1|はい|  
|**TransactionID**|**bigint**|トランザクションに対してシステムが割り当てた ID。|4|いいえ|  
  
  
