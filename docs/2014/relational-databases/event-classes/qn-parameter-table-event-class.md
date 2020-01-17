---
title: QN:Parameter Table イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event classes [SQL Server], QN:Parameter Table
ms.assetid: 292da1ed-4c7e-4bd2-9b84-b9ee09917724
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 395df605926f0ff4ddc30970cdcebce0f1d0c8fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63044447"
---
# <a name="qnparameter-table-event-class"></a>QN:Parameter Table イベント クラス
  QN:Parameter table イベントでは、パラメーター情報を格納する内部テーブルの作成や削除、およびその内部テーブルに対する参照カウンターの管理に必要な操作に関する情報が報告されます。 また、このイベントでは、内部的な動作状況も報告されます。この情報はパラメーター テーブルの使用カウントをリセットするために使用されます。  
  
## <a name="qnparameter-table-event-class-data-columns"></a>QN:Parameter table イベント クラスのデータ列  
  
|データ列|型|説明|列番号|フィルターの適用|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|ClientProcessID|`int`|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターによって割り当てられた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|はい|  
|DatabaseID|`int`|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database*ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|`nvarchar`|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|EventClass|`Int`|イベントの種類 = 200。|27|いいえ|  
|EventSequence|`int`|このイベントのシーケンス番号。|51|いいえ|  
|EventSubClass|`nvarchar`|イベント サブクラスの種類です。各イベント クラスについての詳細な情報を提供します。 この列には次の値が含まれます。<br /><br /> テーブルの作成:パラメーター テーブルがデータベースに作成されていることを示します。<br /><br /> テーブルのドロップの操作:データベースが自動的にリソースを解放、未使用のパラメーター テーブルを削除しようとしたことを示します。<br /><br /> テーブルのドロップ操作が失敗しました。データベースが、未使用のパラメーター テーブルを削除しようと、失敗したことを示します。 リソースを解放するために、パラメーター テーブルを削除するスケジュールが [!INCLUDE[ssDE](../../includes/ssde-md.md)] によって自動的に組み直されます。<br /><br /> テーブルを削除します。データベースが、パラメーター テーブルを正常に削除されたことを示します。<br /><br /> ピン留めされたテーブル:内部処理パラメーター テーブルを現在の使用がマークされていることを示します。<br /><br /> Table unpinned:パラメーター テーブルが固定されていることを示します。 内部処理によるこのテーブルの使用は完了しています。<br /><br /> 増加ユーザー数:パラメーター テーブルを参照するクエリ通知サブスクリプションの数が増加したことを示します。<br /><br /> デクリメントされたユーザーの数:パラメーター テーブルを参照するクエリ通知サブスクリプションの数が減少したことを示します。<br /><br /> LRU カウンターのリセット:パラメーター テーブルの使用カウントがリセットされたことを示します。<br /><br /> クリーンアップ タスクを開始します。このパラメーター テーブル内のすべてのサブスクリプションのクリーンアップが開始されたことを示します。 このクリーンアップは、データベースを起動したとき、またはこのパラメーター テーブルのサブスクリプションが基づいているテーブルが削除されたときに発生します。<br /><br /> クリーンアップ タスクが完了しました。このパラメーター テーブル内のすべてのサブスクリプションのクリーンアップがいつ終了したことを示します。|21|はい|  
|GroupID|`int`|SQL トレース イベントが発生したワークロード グループの ID。|66|[はい]|  
|HostName|`nvarchar`|クライアントが実行しているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|IsSystem|`int`|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。<br /><br /> 0 = ユーザー<br /><br /> 1 = システム|60|いいえ|  
|LoginName|`nvarchar`|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DOMAIN *Username*\\*の形式で表された*セキュリティ ログインまたは Windows ログイン資格情報)。|11|いいえ|  
|LoginSID|`image`|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|NTDomainName|`nvarchar`|ユーザーが属している Windows ドメイン。|7|はい|  
|NTUserName|`nvarchar`|このイベントが生成された接続を所有するユーザーの名前。|6|[はい]|  
|RequestID|`int`|ステートメントを含む要求の ID。|49|[はい]|  
|ServerName|`nvarchar`|トレースされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|SessionLoginName|`nvarchar`|セッションを開始したユーザーのログイン名。 たとえば、アプリケーションから、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|[はい]|  
|SPID|`int`|イベントが発生したセッションの ID。|12|はい|  
|StartTime|`datetime`|イベントの開始時刻 (取得できた場合)。|14|はい|  
|TextData|`ntext`|このイベント固有の情報を含む XML ドキュメントを返します。 このドキュメントは、 [SQL Server Query Notification Profiler Event Schema](https://go.microsoft.com/fwlink/?LinkId=63331) ページから入手できる XML スキーマに準拠しています。|1|はい|  
  
  
