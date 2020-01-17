---
title: sys.dm_broker_connections (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/08/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_connections
- dm_broker_connections
- sys.dm_broker_connections_TSQL
- dm_broker_connections_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_connections dynamic management view
ms.assetid: d9e20433-67fe-4fcc-80e3-b94335b2daef
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2df4786147a5301e4e9167cbe121b9151e72190f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68099163"
---
# <a name="sysdmbrokerconnections-transact-sql"></a>sys.dm_broker_connections (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  それぞれの行を返します[!INCLUDE[ssSB](../../includes/sssb-md.md)]ネットワーク接続。 次の表では、詳しく説明します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**connection_id**|**uniqueidentifier**|接続の識別子。 NULL 値を許容します。|  
|**transport_stream_id**|**uniqueidentifier**|識別子、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] TCP/IP 通信にこの接続で使用されるネットワーク インターフェイス (SNI) 接続します。 NULL 値を許容します。|  
|**state**|**smallint**|接続の現在の状態。 NULL 値を許容します。 設定可能な値:<br /><br /> 1 = NEW<br /><br /> 2 = 接続<br /><br /> 3 = CONNECTED<br /><br /> 4 = LOGGED_IN<br /><br /> 5 = 終了|  
|**state_desc**|**nvarchar(60)**|接続の現在の状態。 NULL 値を許容します。 設定可能な値:<br /><br /> NEW<br /><br /> CONNECTING<br /><br /> CONNECTED<br /><br /> LOGGED_IN<br /><br /> CLOSED|  
|**connect_time**|**datetime**|接続が開いた日付と時刻。 NULL 値を許容します。|  
|**login_time**|**datetime**|日付と時刻ログインで接続に成功しました。 NULL 値を許容します。|  
|**authentication_method**|**nvarchar(128)**|NTLM または KERBEROS など、Windows 認証方法の名前。 値は、Windows から取得します。 NULL 値を許容します。|  
|**principal_name**|**nvarchar(128)**|接続権限が検証されたログインの名前。 Windows 認証では、この値は、リモート ユーザー名です。 証明書認証の場合、この値は証明書の所有者になります。 NULL 値を許容します。|  
|**remote_user_name**|**nvarchar(128)**|Windows 認証で使用されるその他のデータベースからのピア ユーザーの名前。 NULL 値を許容します。|  
|**last_activity_time**|**datetime**|日付と時刻を接続を送信または受信の情報を最後に使用されます。 NULL 値を許容します。|  
|**is_accept**|**bit**|接続がリモート側で発生したかどうかを示します。 NULL 値を許容します。<br /><br /> 1 = 接続はリモート インスタンスから、要求が受け入れられました。<br /><br /> 0 = ローカル インスタンスで開始された接続。|  
|**login_state**|**smallint**|この接続のログイン プロセスの状態。 設定可能な値:<br /><br /> 0 = 初期<br /><br /> 1 = 待機ログイン ネゴシエート<br /><br /> 2 = ONE ISC<br /><br /> 3 = 1 つの ASC<br /><br /> 4 = TWO ISC<br /><br /> 5 = 2 つの ASC<br /><br /> 6 = 待機 ISC ことを確認します<br /><br /> 7 = 待機 ASC ことを確認します<br /><br /> 8 = 待機の拒否<br /><br /> 9 = 待機 PRE-MASTER SECRET<br /><br /> 10 = WAIT VALIDATION<br /><br /> 11 = 待機調停<br /><br /> 12 = オンライン<br /><br /> 13 = エラー|  
|**login_state_desc**|**nvarchar(60)**|リモート コンピューターからのログインの現在の状態。 設定可能な値:<br /><br /> 接続ハンドシェイクを初期化しています。<br /><br /> 接続ハンドシェイクは、Login Negotiate メッセージを待機しています。<br /><br /> 接続ハンドシェイクが初期化され、認証用のセキュリティ コンテキストを送信します。<br /><br /> 接続ハンドシェイクを受信し、認証用のセキュリティ コンテキストを承諾しました。<br /><br /> 接続ハンドシェイクが初期化され、認証用のセキュリティ コンテキストを送信します。 ピアを認証するために使用できるオプションのメカニズムがあります。<br /><br /> 接続ハンドシェイクを受信し、認証用のセキュリティ コンテキストを送信しました。 ピアを認証するために使用できるオプションのメカニズムがあります。<br /><br /> 接続ハンドシェイクは、Initialize Security Context Confirmation メッセージを待機しています。<br /><br /> 接続ハンドシェイクは、Accept Security Context Confirmation メッセージを待機しています。<br /><br /> 接続ハンドシェイクは、失敗した認証に関する SSPI 拒否メッセージを待機しています。<br /><br /> 接続ハンドシェイクは、Pre-master Secret メッセージを待機しています。<br /><br /> 接続ハンドシェイクは、Validation メッセージを待機しています。<br /><br /> 接続ハンドシェイクは、Arbitration メッセージを待機しています。<br /><br /> 接続ハンドシェイクが完了し、メッセージ交換が、オンライン (準備完了状態)。<br /><br /> 接続はエラーにあります。|  
|**peer_certificate_id**|**int**|認証でリモート インスタンスによって使用される証明書のローカル オブジェクト ID。 この証明書の所有者への CONNECT 権限が必要、[!INCLUDE[ssSB](../../includes/sssb-md.md)]エンドポイント。 NULL 値を許容します。|  
|**encryption_algorithm**|**smallint**|接続で使用される暗号化アルゴリズム。 NULL 値を許容します。 設定可能な値:<br /><br /> **値&#124;説明&#124;対応する DDL オプション**<br /><br /> 0 &#124; none&#124;無効になっています。<br /><br /> 1&#124;署名のみ<br /><br /> 2 &#124; AES、RC4&#124;必要&#124;アルゴリズム RC4 が必要}<br /><br /> 3 &#124; AES&#124;アルゴリズム AES が必要<br /><br /> **注:** RC4 アルゴリズムは、旧バージョンとの互換性のためにのみサポートされています。 データベース互換性レベルが 90 または 100 の場合、新しい素材は RC4 または RC4_128 を使用してのみ暗号化できます (非推奨)。AES アルゴリズムのいずれかなど、新しいアルゴリズムを使用してください。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降のバージョンでは、どの互換性レベルでも、RC4 または RC4_128 を使用して暗号化された素材を暗号化解除できます。|  
|**encryption_algorithm_desc**|**nvarchar(60)**|暗号化アルゴリズムのテキスト表示。 NULL 値を許容します。 有効値は次のとおりです。<br /><br /> **説明&#124;対応する DDL オプション**<br /><br /> NONE&#124;無効になっています。<br /><br /> RC4 &#124; {0} に必要な&#124;アルゴリズム RC4 が必要}<br /><br /> AES&#124;アルゴリズム AES が必要<br /><br /> NONE、RC4 &#124; {サポート&#124;アルゴリズム RC4 をサポート}<br /><br /> NONE、AES&#124;アルゴリズム RC4 をサポート<br /><br /> RC4、AES&#124;ために必要なアルゴリズム RC4 AES<br /><br /> AES、RC4&#124;アルゴリズム AES RC4 が必要<br /><br /> NONE、RC4、AES&#124;サポート アルゴリズム RC4 AES<br /><br /> NONE、AES、RC4&#124;アルゴリズム AES RC4 をサポート|  
|**receives_posted**|**smallint**|この接続でまだ完了していない非同期ネットワーク受信の数。 NULL 値を許容します。|  
|**is_receive_flow_controlled**|**bit**|ネットワークがビジー状態のときに行われたフロー制御が原因で、ネットワーク受信が延期されたかどうか。 NULL 値を許容します。<br /><br /> 1 = True|  
|**sends_posted**|**smallint**|非同期のネットワークの数をまだ完了していないこの接続に送信します。 NULL 値を許容します。|  
|**is_send_flow_controlled**|**bit**|ネットワークで送信するかどうかが延期されているネットワーク フロー制御のため、ネットワークがビジー状態です。 NULL 値を許容します。<br /><br /> 1 = True|  
|**total_bytes_sent**|**bigint**|この接続で送信されたバイトの合計数。 NULL 値を許容します。|  
|**total_bytes_received**|**bigint**|この接続で受信された合計バイト数。 NULL 値を許容します。|  
|**total_fragments_sent**|**bigint**|この接続で送信された [!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージ フラグメントの合計数。 NULL 値を許容します。|  
|**total_fragments_received**|**bigint**|この接続で受信された [!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージ フラグメントの合計数。 NULL 値を許容します。|  
|**total_sends**|**bigint**|この接続で発行されたネットワーク送信要求の合計数。 NULL 値を許容します。|  
|**total_receives**|**bigint**|ネットワークの合計数は、この接続によって発行された要求を受信します。 NULL 値を許容します。|  
|**peer_arbitration_id**|**uniqueidentifier**|エンドポイントの内部識別子です。 NULL 値を許容します。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="physical-joins"></a>物理結合  
 ![Sys.dm_broker_connections の結合](../../relational-databases/system-dynamic-management-views/media/join-dm-broker-connections-1.gif "sys.dm_broker_connections の結合")  
  
## <a name="relationship-cardinalities"></a>リレーションシップの基数  
  
|From|変換先|リレーションシップ|  
|----------|--------|------------------|  
|**dm_broker_connections.connection_id**|**dm_exec_connections.connection_id**|一対一|  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Service Broker 関連の動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

