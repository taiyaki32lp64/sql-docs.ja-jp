---
title: QN:Parameter Table イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- event classes [SQL Server], QN:Parameter Table
ms.assetid: 292da1ed-4c7e-4bd2-9b84-b9ee09917724
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cb89f83f0a916a9d56443e7494ce5e8284350bb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67940628"
---
# <a name="qnparameter-table-event-class"></a>QN:Parameter Table イベント クラス
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  QN:Parameter table イベントでは、パラメーター情報を格納する内部テーブルの作成や削除、およびその内部テーブルに対する参照カウンターの管理に必要な操作に関する情報が報告されます。 また、このイベントでは、内部的な動作状況も報告されます。この情報はパラメーター テーブルの使用カウントをリセットするために使用されます。  
  
## <a name="qnparameter-table-event-class-data-columns"></a>QN:Parameter table イベント クラスのデータ列  
  
|データ列|型|[説明]|列番号|フィルターの適用|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|ClientProcessID|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターによって割り当てられた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|はい|  
|DatabaseID|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database*ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|**nvarchar**|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|EventClass|**Int**|イベントの種類 = 200。|27|いいえ|  
|EventSequence|**int**|このイベントのシーケンス番号。|51|いいえ|  
|EventSubClass|**nvarchar**|イベント サブクラスの種類です。各イベント クラスについての詳細な情報を提供します。 この列には次の値が含まれます。<br /><br /> **Table created**: パラメーター テーブルがデータベース内で作成されたことを示します。<br /><br /> **Table drop attempt**: リソースを解放するために、未使用のパラメーター テーブルの自動削除がデータベースによって試行されたことを示します。<br /><br /> **Table drop attempt failed**: 未使用のパラメーター テーブルの削除がデータベースによって試行され、失敗したことを示します。 リソースを解放するために、パラメーター テーブルを削除するスケジュールが [!INCLUDE[ssDE](../../includes/ssde-md.md)] によって自動的に組み直されます。<br /><br /> **Table dropped**: パラメーター テーブルがデータベースによって正常に削除されたことを示します。<br /><br /> **Table pinned**: パラメーター テーブルが内部処理の現在の使用対象としてマークされていることを示します。<br /><br /> **Table unpinned**: パラメーター テーブルが固定解除されたことを示します。 内部処理によるこのテーブルの使用は完了しています。<br /><br /> **Number of users incremented**: パラメーター テーブルを参照するクエリ通知サブスクリプションの数が増加したことを示します。<br /><br /> **Number of users decremented**: パラメーター テーブルを参照するクエリ通知サブスクリプションの数が減少したことを示します。<br /><br /> **LRU counter reset**: パラメーター テーブルの使用カウントがリセットされたことを示します。<br /><br /> **Cleanup task started**: このパラメーター テーブル内のすべてのサブスクリプションのクリーンアップが開始されたことを示します。 このクリーンアップは、データベースを起動したとき、またはこのパラメーター テーブルのサブスクリプションが基づいているテーブルが削除されたときに発生します。<br /><br /> **Cleanup task finished**: このパラメーター テーブル内のすべてのサブスクリプションのクリーンアップが終了したことを示します。|21|はい|  
|GroupID|**int**|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|HostName|**nvarchar**|クライアントが実行しているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|IsSystem|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。<br /><br /> 0 = ユーザー<br /><br /> 1 = システム|60|いいえ|  
|LoginName|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DOMAIN *Username*\\*の形式で表された*セキュリティ ログインまたは Windows ログイン資格情報)。|11|いいえ|  
|LoginSID|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|NTDomainName|**nvarchar**|ユーザーが属している Windows ドメイン。|7|はい|  
|NTUserName|**nvarchar**|このイベントが生成された接続を所有するユーザーの名前。|6|はい|  
|RequestID|**int**|ステートメントを含む要求の ID。|49|はい|  
|ServerName|**nvarchar**|トレースされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|SessionLoginName|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、アプリケーションから、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|SPID|**int**|イベントが発生したセッションの ID。|12|はい|  
|StartTime|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|TextData|**ntext**|このイベント固有の情報を含む XML ドキュメントを返します。 このドキュメントは、 [SQL Server Query Notification Profiler Event Schema](https://go.microsoft.com/fwlink/?LinkId=63331) ページから入手できる XML スキーマに準拠しています。|1|はい|  
  
  
