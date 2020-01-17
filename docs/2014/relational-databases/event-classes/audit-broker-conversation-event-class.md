---
title: Audit Broker Conversation イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Audit Broker Conversation event class
ms.assetid: d58e3577-e297-42e5-b8fe-206665a75d13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e92b8dacf3f1d4c9bf4992739acc7592f2135386
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62912196"
---
# <a name="audit-broker-conversation-event-class"></a>Audit Broker Conversation イベント クラス
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **Audit Broker Conversation** イベントを作成して、Service Broker のダイアログ セキュリティに関連した監査メッセージを報告します。  
  
## <a name="audit-broker-conversation-event-class-data-columns"></a>Audit Broker Conversation イベント クラスのデータ列  
  
|データ列|型|説明|列番号|フィルターの適用|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|**BigintData1**|**bigint**|メッセージのメッセージ シーケンス番号。|52|いいえ|  
|**ClientProcessID**|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターによって割り当てられた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|はい|  
|**DatabaseID**|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|**Error**|**int**|(このイベントによってエラーが報告された場合) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー番号。|31|いいえ|  
|**EventClass**|**int**|キャプチャされたイベント クラスの種類。 **Audit Broker Conversation** の場合は、常に **158**です。|27|いいえ|  
|**EventSubClass**|**int**|イベント サブクラスの種類です。各イベント クラスについての詳細な情報を提供します。 次の表に、このイベントのイベント サブクラス値を示します。|21|はい|  
|**FileName**|**nvarchar**|ログインの失敗理由。 ログインに成功した場合、この列は空です。|36|いいえ|  
|**GUID**|**uniqueidentifier**|ダイアログのメッセージ交換 ID。 この ID はメッセージの一部として転送され、メッセージ交換の両側で共有されます。|54|いいえ|  
|**HostName**|**nvarchar**|クライアントが実行しているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、 **HOST_NAME** 関数を使用します。|8|はい|  
|**IntegerData**|**int**|メッセージのフラグメント番号。|25|いいえ|  
|**NTDomainName**|**nvarchar**|ユーザーが属している Windows ドメイン。|7|[はい]|  
|**NTUserName**|**nvarchar**|このイベントが生成された接続を所有するユーザーの名前。|6|はい|  
|**ObjectId**|**int**|対象サービスのユーザー ID。|22|いいえ|  
|**RoleName**|**nvarchar**|メッセージ交換ハンドルのロール。 **initiator** または **target**のいずれかです。|38|いいえ|  
|**ServerName**|**nvarchar**|トレースされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|**Severity**|**int**|(このイベントによってエラーが報告された場合) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラーの重大度。|29|いいえ|  
|**SPID**|**int**|クライアントに関連付けられているプロセスに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって割り当てられているサーバー プロセス ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**状態**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のソース コード内のイベントが生成された場所を示します。 イベントが生成された場所によって、状態コードが異なることがあります。 マイクロソフトのサポート エンジニアはこの状態コードを使用して、イベントが生成されたソース コード内の場所を特定することができます。|30|いいえ|  
|**TextData**|**ntext**|エラーの場合、失敗理由を説明するメッセージが格納されます。 次のいずれかの値です。<br /><br /> **証明書が見つかりませんでした**: ダイアログ プロトコル セキュリティに指定されたユーザーが証明書を持っていません。<br /><br /> **無効な期間です**: ダイアログ プロトコル セキュリティに指定されたユーザーは証明書を持っていますが、その証明書の有効期限が切れています。<br /><br /> **証明書のサイズが、メモリ割り当てに対して大きすぎます**: ダイアログ プロトコル セキュリティに指定されたユーザーは証明書を持っていますが、その証明書のサイズが大きすぎます。 Service Broker でサポートされる証明書の最大サイズは、32,768 バイトです。<br /><br /> **秘密キーが見つかりません**: ダイアログ プロトコル セキュリティに指定されたユーザーは証明書を持っていますが、その証明書には秘密キーが関連付けられていません。<br /><br /> **証明書の秘密キー サイズと暗号化プロバイダーの互換性がありません**: 証明書の秘密キー サイズが、正常に処理できないサイズです。 秘密キー サイズは 64 バイトの倍数である必要があります。<br /><br /> **証明書の公開キー サイズと暗号化プロバイダーの互換性がありません**: 証明書の公開キー サイズが、正常に処理できないサイズです。 公開キー サイズは 64 バイトの倍数である必要があります。<br /><br /> **証明書の秘密キー サイズと暗号化されたキー交換のキーには互換性がありません**: キー交換のキーで指定されているキー サイズが、証明書の秘密キーのサイズと一致しません。 これは、一般に、リモート コンピューター上の証明書がデータベース内の証明書と一致しないことを示します。<br /><br /> **証明書の公開キー サイズとセキュリティ ヘッダーの署名には互換性がありません**: セキュリティ ヘッダーに、証明書の公開キーを使用して検証できない署名が含まれています。 これは、一般に、リモート コンピューター上の証明書がデータベース内の証明書と一致しないことを示します。|1|はい|  
  
 次の表に、このイベント クラスのサブクラス値を示します。  
  
|ID|サブクラス|説明|  
|--------|--------------|-----------------|  
|1|No Security Header|セキュリティで保護されたメッセージ交換時に、Service Broker がセッション キーを含んでいないメッセージを受信しました。 セキュリティで保護されたメッセージ交換が確立されると、ダイアログのプロトコルは、メッセージ交換で使用されるすべてのメッセージにセッション キーが含まれていることを必要とします。|  
|2|No Certificate|メッセージ交換の送信者または受信者のどちらかの使用可能な証明書を Service Broker で検出できませんでした。 メッセージ交換をセキュリティで保護するには、メッセージ交換の送信者と受信者の両方が使用できる証明書がデータベースに格納されている必要があります。|  
|3|Invalid Signature|送信者が送信者の証明書に公開キーを使用して提供したメッセージの署名を Service Broker で確認できませんでした。 これは、メッセージが破損していること、メッセージが改ざんされたこと、リモート サービスとローカル サービスが同じユーザー証明書を使用して構成されていないこと、または証明書の有効期限が切れていることを示している場合があります。|  
|4|Run As Target Failure|送信先のユーザーが送信先のキューに対する受信権限を持っていません。 Service Broker では、許可されていないユーザーがメッセージを受信できないように、キューからメッセージを受け取れないユーザーを送信先とするメッセージをエンキューしません。これは、メッセージの送信元のユーザーにメッセージをエンキューする権限があるかどうかとは無関係です。|  
  
## <a name="see-also"></a>参照  
 [SQL Server Service Broker (SQL Server Service Broker)](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
