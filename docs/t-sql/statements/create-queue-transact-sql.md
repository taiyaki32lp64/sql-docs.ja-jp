---
title: CREATE QUEUE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- QUEUE_TSQL
- CREATE QUEUE
- QUEUE
- CREATE_QUEUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE QUEUE statement
- internal activation [Service Broker]
- stored procedure activation [Service Broker]
- message retention [Service Broker]
- unavailable queues [Service Broker]
- activation stored procedures [Service Broker]
- queues [Service Broker], creating
ms.assetid: fce80faf-2bdc-475d-8ca1-31438ed41fb0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b1446d4b43524a1e670084812279284d86eb1b0b
ms.sourcegitcommit: 4c7151f9f3f341f8eae70cb2945f3732ddba54af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71326095"
---
# <a name="create-queue-transact-sql"></a>CREATE QUEUE (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

データベースに新しいキューを作成します。 キューにはメッセージが格納されます。 サービス用のメッセージを受信すると、そのメッセージは [!INCLUDE[ssSB](../../includes/sssb-md.md)] によって、サービスに関連付けられているキューに格納されます。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>構文

```
CREATE QUEUE <object>
   [ WITH
     [ STATUS = { ON | OFF } [ , ] ]
     [ RETENTION = { ON | OFF } [ , ] ]
     [ ACTIVATION (
         [ STATUS = { ON | OFF } , ]
           PROCEDURE_NAME = <procedure> ,
           MAX_QUEUE_READERS = max_readers ,
           EXECUTE AS { SELF | 'user_name' | OWNER }
            ) [ , ] ]
     [ POISON_MESSAGE_HANDLING (
         [ STATUS = { ON | OFF } ] ) ]
    ]
     [ ON { filegroup | [ DEFAULT ] } ]
[ ; ]

<object> ::=
{ database_name.schema_name.queue_name | schema_name.queue_name | queue_name }

<procedure> ::=
{ database_name.schema_name.stored_procedure_name | schema_name.stored_procedure_name | stored_procedure_name }

```

## <a name="arguments"></a>引数

*database_name* (オブジェクト) は、新しいキューを作成するデータベースの名前です。 *database_name* には、既存のデータベース名を指定する必要があります。 *database_name* が指定されていない場合、キューは現在のデータベースに作成されます。

*schema_name* (オブジェクト) は、新しいキューが所属するスキーマの名前です。 省略すると、ステートメントを実行するユーザーの既定のスキーマが使用されます。 CREATE QUEUE ステートメントが、sysadmin 固定サーバー ロールのメンバー、または *database_name* で指定されるデータベース内の db_dbowner または db_ddladmin 固定データベース ロールのメンバーによって実行される場合、*schema_name* には、現在の接続のログインに関連付けられているスキーマ以外のスキーマを指定できます。 それ以外の場合、*schema_name* には、ステートメントを実行するユーザーの既定のスキーマを指定する必要があります。

*queue_name* は、作成するキューの名前です。 この名前は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別子のガイドラインに従っている必要があります。

STATUS (キュー) は、キューが使用可能 (ON) か、使用不可能 (OFF) かを指定します。 キューが使用不可能な場合、キューにメッセージを追加したり、キューからメッセージを削除することはできません。 ALTER QUEUE ステートメントによってキューが使用可能になるまでキューにメッセージが届かないようにする場合は、キューを使用不可能な状態で作成できます。 この句を省略すると、既定値の ON が使用され、キューは使用可能になります。

RETENTION は、キューのメッセージ保有期間の設定を指定します。 RETENTION = ON の場合、このキューを使用するメッセージ交換で送信または受信されるすべてのメッセージは、メッセージ交換が終了するまでキュー内に保有されます。 このことにより、監査目的でメッセージを保有したり、エラーが発生した場合に補正するトランザクションを実行することができます。 この句を指定しない場合、保有期間の設定は既定で OFF になります。

> [!NOTE]
> RETENTION = ON を設定すると、パフォーマンスが低下する場合があります。 この設定はアプリケーションに必要な場合にのみ使用してください。

ACTIVATION は、このキュー内のメッセージを処理するために開始する必要があるストアド プロシージャの情報を指定します。

STATUS (アクティブ化) は、[!INCLUDE[ssSB](../../includes/sssb-md.md)] によってストアド プロシージャを開始するかどうかを指定します。 STATUS = ON の場合は、現在実行中のプロシージャの数が MAX_QUEUE_READERS より少なく、ストアド プロシージャによるメッセージの受信よりも早くメッセージがキューに到着する場合に、PROCEDURE_NAME で指定されるストアド プロシージャがキューによって開始されます。 STATUS = OFF の場合は、キューによってストアド プロシージャが開始されません。 この句を指定しない場合、既定値は ON になります。

PROCEDURE_NAME = \<プロシージャ> は、このキュー内のメッセージを処理するために開始するストアド プロシージャの名前を指定します。 この値は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の識別子にする必要があります。

*database_name* (プロシージャ) は、ストアド プロシージャを含むデータベースの名前です。

*schema_name* (プロシージャ) は、ストアド プロシージャを含むスキーマの名前です。

*procedure_name* は、ストアド プロシージャの名前です。

MAX_QUEUE_READERS =*max_readers* は、キューで同時に開始する、アクティブ化ストアド プロシージャの最大インスタンス数を指定します。 *max_readers* の値には、**0** から **32767** の数値を指定する必要があります。

EXECUTE AS は、アクティブ化ストアド プロシージャを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ユーザー アカウントを指定します。 キューによってストアド プロシージャが開始されたときに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではこのユーザーの権限を確認できる必要があります。 ドメイン ユーザーの場合は、プロシージャが開始されるかアクティブ化が失敗したとき、サーバーがドメインに接続している必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーの場合は、サーバーで常に権限を確認できます。

SELF は、現在のユーザーとしてストアド プロシージャを実行することを指定します。 (対象の CREATE QUEUE ステートメントを実行しているデータベース プリンシパル。)

'*user_name*' は、ストアド プロシージャを実行するユーザーの名前を指定します。 *user_name* パラメーターには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別子として有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーを指定する必要があります。 現在のユーザーは、指定した *user_name* に対して IMPERSONATE 権限を保持している必要があります。

OWNER は、キューの所有者としてストアド プロシージャを実行することを指定します。

POISON_MESSAGE_HANDLING は、キューに対する有害なメッセージの処理が有効になっているかどうかを指定します。 既定値は ON です。

有害なメッセージの処理が OFF に設定されているキューは、トランザクションのロールバックが連続して 5 回実行されても無効になりません。 これにより、カスタムの有害なメッセージの処理システムをアプリケーションで定義できます。

ON *filegroup |* **[DEFAULT]** は、このキューを作成する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ファイル グループを指定します。 *filegroup* パラメーターを使用してファイル グループを指定するか、DEFAULT 識別子を使用して Service Broker データベースの既定のファイル グループを指定することができます。 この句のコンテキストでは、DEFAULT はキーワードとして扱われないため、識別子として区切り記号で区切る必要があります。 ファイル グループを指定しない場合、キューの作成ではデータベースの既定のファイル グループが使用されます。

## <a name="remarks"></a>Remarks

キューは SELECT ステートメントの対象にすることができますが、 キューの内容を変更するには、SEND、RECEIVE、END CONVERSATION など、[!INCLUDE[ssSB](../../includes/sssb-md.md)] のメッセージ交換で動作するステートメントを使用する必要があります。 キューは、INSERT、UPDATE、DELETE、または TRUNCATE ステートメントの対象にすることはできません。

キューは一時オブジェクトとして指定できません。 したがって、 **#** で始まるキューの名前は無効になります。

キューを非アクティブ状態で作成した場合、サービス用のインフラストラクチャを配置してから、キューでメッセージを受信することができます。

キューにメッセージがない場合、[!INCLUDE[ssSB](../../includes/sssb-md.md)] によってアクティブ化ストアド プロシージャは停止されません。 アクティブ化ストアド プロシージャは、しばらくの間キューに使用できるメッセージがないときには終了してください。

アクティブ化ストアド プロシージャの権限は、キューの作成時ではなく、[!INCLUDE[ssSB](../../includes/sssb-md.md)] によってストアド プロシージャが開始されるときに確認されます。 CREATE QUEUE ステートメントでは、EXECUTE AS 句で指定したユーザーに、PROCEDURE NAME 句で指定したストアド プロシージャの実行権限があるかどうかは確認されません。

キューが使用できない場合、[!INCLUDE[ssSB](../../includes/sssb-md.md)] では、データベースの転送キュー内にあるキューを使用するサービスのメッセージが保持されます。 カタログ ビュー sys.transmission_queue では、転送キューのビューが提供されます。

キューはスキーマが所有するオブジェクトです。 キューは、sys.objects カタログ ビューに表示されます。

次の表は、キューの列の一覧です。

|列名|データ型|[説明]|
|-----------------|---------------|-----------------|
|ステータス|**tinyint**|メッセージの状態。 RECEIVE ステートメントでは、status が **1** のメッセージがすべて返されます。 メッセージの保有が指定されている場合は、status が 0 に設定されます。 メッセージの保有が指定されていない場合は、メッセージがキューから削除されます。 キューのメッセージには、次のいずれかの値を含めることができます。<br /><br /> **0** = 保持されている受信メッセージ<br /><br /> **1** = 受信準備完了<br /><br /> **2** = 未完了<br /><br /> **3** = 保持されている送信メッセージ|
|priority|**tinyint**|このメッセージに割り当てられている優先度レベル。|
|queuing_order|**bigint**|キュー内のメッセージの順序番号。|
|conversation_group_id|**uniqueidentifier**|メッセージが属するメッセージ交換グループの識別子。|
|conversation_handle|**uniqueidentifier**|メッセージが属するメッセージ交換のハンドル。|
|message_sequence_number|**bigint**|メッセージ交換内でのメッセージのシーケンス番号。|
|service_name|**nvarchar(512)**|メッセージ交換の対象サービスの名前。|
|service_id|**int**|メッセージ交換の対象サービスに関する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクト識別子。|
|service_contract_name|**nvarchar (256)**|メッセージ交換が従うコントラクトの名前。|
|service_contract_id|**int**|メッセージ交換が従うコントラクトに関する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクト識別子。|
|message_type_name|**nvarchar (256)**|メッセージの種類を示すメッセージ型の名前。|
|message_type_id|**int**|メッセージの種類を示すメッセージ型に関する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクト識別子。|
|validation|**nchar(2)**|メッセージに使用される検証。<br /><br /> E = 空<br /><br /> N = なし<br /><br /> X = XML|
|message_body|**varbinary(max)**|メッセージの内容。|
|message_id|**uniqueidentifier**|メッセージの一意識別子。|

## <a name="permissions"></a>アクセス許可

キューを作成する権限では、`db_ddladmin` 固定データベース ロールまたは `db_owner` 固定データベース ロールのメンバー、または `sysadmin` 固定サーバー ロールのメンバーを使用します。

キューに対する `REFERENCES` 権限は、既定ではキューの所有者、`db_ddladmin` 固定データベース ロールまたは `db_owner` 固定データベース ロールのメンバー、または `sysadmin` 固定サーバー ロールのメンバーに与えられています。

キューに対する `RECEIVE` 権限は、既定ではキューの所有者、`db_owner` 固定データベース ロールのメンバー、または `sysadmin` 固定サーバー ロールのメンバーに与えられています。

## <a name="examples"></a>使用例

### <a name="a-creating-a-queue-with-no-parameters"></a>A. パラメーターなしでキューを作成する

次の例では、メッセージの受信に使用できるキューを作成します。 キューにアクティブ化ストアド プロシージャは指定しません。

```sql
CREATE QUEUE ExpenseQueue ;
```

### <a name="b-creating-an-unavailable-queue"></a>B. 使用できないキューを作成する

次の例では、メッセージの受信に使用できないキューを作成します。 キューにアクティブ化ストアド プロシージャは指定しません。

```sql
CREATE QUEUE ExpenseQueue WITH STATUS=OFF ;
```

### <a name="c-creating-a-queue-and-specify-internal-activation-information"></a>C. キューを作成し、内部アクティブ化情報を指定する

次の例では、メッセージの受信に使用できるキューを作成します。 メッセージがキューに格納されると、キューによってストアド プロシージャ `expense_procedure` が起動されます。 ストアド プロシージャは、ユーザー `ExpenseUser` として実行されます。 キューによって、ストアド プロシージャのインスタンスが `5` 個まで起動されます。

```sql
CREATE QUEUE ExpenseQueue
    WITH STATUS=ON,
    ACTIVATION (
        PROCEDURE_NAME = expense_procedure
        , MAX_QUEUE_READERS = 5
        , EXECUTE AS 'ExpenseUser' ) ;
```

### <a name="d-creating-a-queue-on-a-specific-filegroup"></a>D. 特定のファイル グループにキューを作成する

次の例では、ファイル グループ `ExpenseWorkFileGroup` にキューを作成します。

```sql
CREATE QUEUE ExpenseQueue
    ON ExpenseWorkFileGroup ;
```

### <a name="e-creating-a-queue-with-multiple-parameters"></a>E. 複数のパラメーターでキューを作成する

次の例では、`DEFAULT` ファイル グループにキューを作成します。 このキューは使用不可能な状態になります。 メッセージは、それらが属するメッセージ交換が終わるまでキューに保持されます。 ALTER QUEUE を使用してキューを使用できるようにすると、キューによってストアド プロシージャ `2008R2.dbo.expense_procedure` が開始され、メッセージが処理されます。 このストアド プロシージャは、`CREATE QUEUE` ステートメントを実行したユーザーとして実行されます。 キューによって、ストアド プロシージャのインスタンスが `10` 個まで起動されます。

```sql
CREATE QUEUE ExpenseQueue
    WITH STATUS = OFF
      , RETENTION = ON
      , ACTIVATION (
          PROCEDURE_NAME = AdventureWorks2012.dbo.expense_procedure
          , MAX_QUEUE_READERS = 10
          , EXECUTE AS SELF )
    ON [DEFAULT];
```

## <a name="see-also"></a>参照

- [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md)
- [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)
- [DROP QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-queue-transact-sql.md)
- [RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)
- [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
