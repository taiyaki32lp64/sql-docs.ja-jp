---
title: QN:Dynamics イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- event classes [SQL Server], QN:Dynamics
ms.assetid: 3c1ffa0c-c9e5-40a6-a26b-28339f60ebc3
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 575ca341e19d36055d7780fd1deec8d05e370111
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67940613"
---
# <a name="qndynamics-event-class"></a>QN:Dynamics イベント クラス
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  QN:Dynamics イベント クラスでは、クエリ通知をサポートするために [!INCLUDE[ssDE](../../includes/ssde-md.md)] が実行するバックグラウンドの利用状況に関する情報が報告されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]内部では、バックグラウンド スレッドでサブスクリプションのタイムアウト、実行を待機しているサブスクリプション、およびパラメーター テーブルの破棄が監視されています。  
  
## <a name="qndynamics-event-class-data-columns"></a>QN:Dynamics イベント クラスのデータ列  
  
|データ列|型|[説明]|列番号|フィルターの適用|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|ClientProcessID|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターによって割り当てられた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|はい|  
|DatabaseID|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database*ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|**nvarchar**|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|EventClass|**int**|イベントの種類 = 202。|27|いいえ|  
|EventSequence|**int**|このイベントのシーケンス番号。|51|いいえ|  
|EventSubClass|**nvarchar**|イベント サブクラスの種類です。各イベント クラスについての詳細な情報を提供します。 この列には次の値が含まれます。<br /><br /> **Clock run started**: 有効期限が切れたパラメーター テーブルのクリーンアップをスケジュールする、[!INCLUDE[ssDE](../../includes/ssde-md.md)]のバックグラウンド スレッドが開始されたことを示します。<br /><br /> **Clock run finished**: 有効期限が切れたパラメーター テーブルのクリーンアップをスケジュールする、[!INCLUDE[ssDE](../../includes/ssde-md.md)]のバックグラウンド スレッドが終了したことを示します。<br /><br /> **Master cleanup task started**: 有効期限が切れたクエリ通知サブスクリプションのデータを削除するクリーンアップ (ガベージ コレクション) が開始された日時を示します。<br /><br /> **Master cleanup task finished**: 有効期限が切れたクエリ通知サブスクリプションのデータを削除するクリーンアップ (ガベージ コレクション) が終了した日時を示します。<br /><br /> **Master cleanup task skipped**: [!INCLUDE[ssDE](../../includes/ssde-md.md)]で、有効期限が切れたクエリ通知サブスクリプションのデータを削除するクリーンアップ (ガベージ コレクション) が実行されなかったことを示します。|21|はい|  
|GroupID|**int**|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|HostName|**nvarchar**|クライアントが実行しているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|IsSystem|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。<br /><br /> 0 = ユーザー<br /><br /> 1 = システム|60|いいえ|  
|LoginName|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは *DOMAIN\Username*という形式の Windows ログイン資格情報)。|11|いいえ|  
|LoginSID|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|NTDomainName|**nvarchar**|ユーザーが属している Windows ドメイン。|7|はい|  
|NTUserName|**nvarchar**|このイベントが生成された接続を所有するユーザーの名前。|6|はい|  
|RequestID|**int**|ステートメントを含む要求の ID。|49|はい|  
|ServerName|**nvarchar**|トレースされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|SessionLoginName|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、アプリケーションから、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|SPID|**int**|イベントが発生したセッションの ID。|12|はい|  
|StartTime|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|TextData|**ntext**|このイベント固有の情報を含む XML ドキュメントを返します。 このドキュメントは、 [SQL Server Query Notification Profiler Event Schema](https://go.microsoft.com/fwlink/?LinkId=63331) ページから入手できる XML スキーマに準拠しています。|1|はい|  
  
  
