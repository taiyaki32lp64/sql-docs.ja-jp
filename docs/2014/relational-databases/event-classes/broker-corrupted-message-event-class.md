---
title: Broker:Corrupted Message イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Corrupted Message event class
ms.assetid: 084bf198-2138-438e-bdc7-4ff1e04300f7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a49f10826496e9e8fea46b1846b74535a173f821
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62664087"
---
# <a name="brokercorrupted-message-event-class"></a>Broker:Corrupted Message イベント クラス
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、Service Broker が破損したメッセージを受信すると、 **Broker:Corrupted Message** イベントが作成されます。  
  
## <a name="brokercorrupted-message-event-class-data-columns"></a>Broker:Corrupted Message イベント クラスのデータ列  
  
|データ列|型|説明|列番号|フィルターの適用|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|**BigintData1**|**bigint**|このメッセージのシーケンス番号。|52|いいえ|  
|**BinaryData**|**image**|メッセージのメッセージ本文。|2|はい|  
|**ClientProcessID**|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターによって割り当てられた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|はい|  
|**DatabaseID**|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|**Error**|**int**|イベント内のテキストの、 **sys.messages** 内でのメッセージ ID 番号。|31|いいえ|  
|**EventClass**|**int**|キャプチャされたイベント クラスの種類。 **Broker:Corrupted Message** の場合は、常に **161**です。|27|いいえ|  
|**EventSequence**|**int**|このイベントのシーケンス番号。|51|いいえ|  
|**FileName**|**nvarchar**|リモート エンドポイントのネットワーク アドレス。|36|いいえ|  
|**GUID**|**uniqueidentifier**|破損したメッセージが所属するメッセージ交換のメッセージ交換 ID。 この ID はメッセージの一部として転送され、メッセージ交換の両側で共有されます。|54|いいえ|  
|**Host Name**|**nvarchar**|クライアントが実行しているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|**IntegerData**|**int**|このメッセージのフラグメント番号。|25|[はい]|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|いいえ|  
|**LoginSid**|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 各 SID はサーバーのログインごとに一意です。|41|[はい]|  
|**NTDomainName**|**nvarchar**|ユーザーが属している Windows ドメイン。|7|はい|  
|**NTUserName**|**nvarchar**|このイベントが生成された接続を所有するユーザーの名前。|6|はい|  
|**ObjectName**|**nvarchar**|メッセージ交換の相手側のサービス名、およびこのデータベースに接続するためにリモート データベースで使用される接続文字列。|34|いいえ|  
|**RoleName**|**nvarchar**|このメッセージを受信するエンドポイントのロール。 次の値のうちの 1 つです。<br /><br /> **initiator**:<br />                  受信エンドポイントはメッセージ交換の発信側です。<br /><br /> **target**:<br />                  受信エンドポイントはメッセージ交換の対象となる側です。|38|いいえ|  
|**ServerName**|**nvarchar**|トレースされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|**Severity**|**int**|エラーが原因で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でメッセージが削除される場合の、エラーの重要度。|29|いいえ|  
|**SPID**|**int**|クライアントに関連付けられているプロセスに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって割り当てられているサーバー プロセス ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**状態**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のソース コード内のイベントが生成された場所を示します。 イベントが生成された場所によって、状態コードが異なることがあります。 マイクロソフトのサポート エンジニアはこの状態コードを使用して、イベントが生成されたソース コード内の場所を特定することができます。|30|いいえ|  
|**TextData**|**ntext**|検出された破損についての説明。|1|はい|  
|**Transaction ID**|**bigint**|トランザクションに対してシステムが割り当てた ID。|4|いいえ|  
  
 このイベントの **TextData** 列には、メッセージとその問題点を説明するメッセージが含まれています。  
  
  
