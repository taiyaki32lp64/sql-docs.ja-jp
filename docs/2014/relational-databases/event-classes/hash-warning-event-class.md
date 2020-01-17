---
title: Hash Warning イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Hash Warning event class
ms.assetid: cb93c620-4be9-4362-8bf0-af3f2048bdaf
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc2b6d2ba25ee487053a7f9f711c499356a5ec59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62662346"
---
# <a name="hash-warning-event-class"></a>Hash Warning イベント クラス
  Hash Warning イベント クラスを使用して、ハッシュ演算中にハッシュの再帰、またはハッシュの中断 (ハッシュの保留) が発生する時点を監視できます。  
  
 使用できるメモリ内にビルド入力が収まらないときに、ハッシュの再帰が発生します。その結果、入力が複数のパーティションに分割され、個別に処理されます。 複数のパーティションに分割されても使用できるメモリ内に収まらない場合は、さらにサブパーティションに分割され、個別に処理されます。 この分割プロセスは、使用できるメモリ内に各パーティションが収まるようになるまで、または (IntegerData データ列に表示された) 最大再帰レベルに到達するまで続けられます。  
  
 ハッシュ演算が最大再帰レベルに到達するとハッシュの保留が発生し、パーティション分割された残りのデータを処理するための代替プランに移行されます。 通常、ハッシュの保留は非対称データにより発生します。  
  
 ハッシュの再帰やハッシュの保留により、サーバーのパフォーマンスが低下することになります。 ハッシュの再帰や保留を取り除いたり、頻度を減らすには、次のいずれかの操作を行います。  
  
-   結合またはグループ化される列に、統計が存在していることを確認します。  
  
-   列に統計が存在する場合は、統計を更新します。  
  
-   異なる種類の結合を使用します。 たとえば、適切であれば、MERGE 結合または LOOP 結合を代用します。  
  
-   コンピューターで使用できるメモリを増やします。 メモリ不足でクエリを適切に処理できず、ディスクへの書き込みが必要になると、ハッシュの再帰や保留が発生します。  
  
 結合に関係する列に統計を作成したり、その統計を更新することが、ハッシュの再帰や保留の発生数を減らすのに最も効果的です。  
  
> [!NOTE]  
>  *猶予ハッシュ結合* および *再帰的ハッシュ結合* という用語は、ハッシュの保留を表すためにも使用されます。  
  
> [!IMPORTANT]  
>  クエリ オプティマイザーが実行プランを生成するときに Hash Warning イベントが発生している場所を特定するには、トレースで Showplan イベント クラスも収集する必要があります。 ノード ID を返さない Showplan Text イベント クラスと Showplan Text (Unencoded) イベント クラスを除く、任意の Showplan イベント クラスを選択できます。 Showplans のノード ID で、クエリ オプティマイザーがクエリ実行プランの生成時に実行する各操作が特定されます。 これらの操作は *オペレーター*と呼ばれ、Showplan の各オペレーターにはノード ID があります。 Hash Warning イベントの ObjectID 列は Showplan のノード ID に対応するので、エラーの原因であるオペレーターつまり操作を判別できます。  
  
## <a name="hash-warning-event-class-data-columns"></a>Hash Warning イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|ClientProcessID|`int`|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによってクライアント プロセス ID が指定された場合、このデータ列にデータが格納されます。|9|はい|  
|DatabaseID|`int`|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|DatabaseName|`nvarchar`|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|EventClass|`int`|イベントの種類 = 55。|27|いいえ|  
|EventSequence|`int`|要求内の特定のイベントのシーケンス。|51|いいえ|  
|EventSubClass|`int`|イベント サブクラスの種類。<br /><br /> 0 = 再帰<br /><br /> 1 = 保留|21|はい|  
|GroupID|`int`|SQL トレース イベントが発生したワークロード グループの ID。|66|はい|  
|HostName|`nvarchar`|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|IntegerData|`int`|再帰レベル (ハッシュの再帰のみ)。|25|はい|  
|IsSystem|`int`|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|LoginName|`nvarchar`|ユーザーのログイン名 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは *\<DOMAIN>\\<username\>* という形式の Windows ログイン資格情報)。|11|はい|  
|LoginSid|`image`|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|NTDomainName|`nvarchar`|ユーザーが所属する Windows ドメイン。|7|はい|  
|NTUserName|`nvarchar`|Windows のユーザー名。|6|はい|  
|ObjectID|`int`|パーティション再分割に関係するハッシュ チームのルートのノード ID。 Showplan のノード ID と一致します。|22|はい|  
|RequestID|`int`|ステートメントを含んでいる要求の ID。|49|はい|  
|ServerName|`nvarchar`|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26||  
|SessionLoginName|`nvarchar`|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|SPID|`int`|イベントが発生したセッションの ID。|12|はい|  
|StartTime|`datetime`|イベントの開始時刻 (取得できた場合)。|14|はい|  
|TransactionID|`bigint`|システムによって割り当てられたトランザクション ID。|4|はい|  
|XactSequence|`bigint`|現在のトランザクションを説明するトークン。|50|はい|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
