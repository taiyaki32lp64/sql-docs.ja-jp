---
title: sp_addarticle (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addarticle
- sp_addarticle_TSQL
helpviewer_keywords:
- sp_addarticle
ms.assetid: 0483a157-e403-4fdb-b943-23c1b487bef0
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: e337e04714b0d8dcc9a8227ca48ad9dc33dcc3dc
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811386"
---
# <a name="sp_addarticle-transact-sql"></a>sp_addarticle (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  アーティクルを作成し、パブリケーションに追加します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addarticle [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
    [ , [ @source_table = ] 'source_table' ]  
    [ , [ @destination_table = ] 'destination_table' ]   
    [ , [ @vertical_partition = ] 'vertical_partition' ]   
    [ , [ @type = ] 'type' ]   
    [ , [ @filter = ] 'filter' ]   
    [ , [ @sync_object= ] 'sync_object' ]   
        [ , [ @ins_cmd = ] 'ins_cmd' ]   
    [ , [ @del_cmd = ] 'del_cmd' ]   
        [ , [ @upd_cmd = ] 'upd_cmd' ]   
    [ , [ @creation_script = ] 'creation_script' ]   
    [ , [ @description = ] 'description' ]   
    [ , [ @pre_creation_cmd = ] 'pre_creation_cmd' ]   
    [ , [ @filter_clause = ] 'filter_clause' ]   
    [ , [ @schema_option = ] schema_option ]   
    [ , [ @destination_owner = ] 'destination_owner' ]   
    [ , [ @status = ] status ]   
    [ , [ @source_owner = ] 'source_owner' ]   
    [ , [ @sync_object_owner = ] 'sync_object_owner' ]   
    [ , [ @filter_owner = ] 'filter_owner' ]   
    [ , [ @source_object = ] 'source_object' ]   
    [ , [ @artid = ] article_ID  OUTPUT ]   
    [ , [ @auto_identity_range = ] 'auto_identity_range' ]   
    [ , [ @pub_identity_range = ] pub_identity_range ]   
    [ , [ @identity_range = ] identity_range ]   
    [ , [ @threshold = ] threshold ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @use_default_datatypes = ] use_default_datatypes  
    [ , [ @identityrangemanagementoption = ] identityrangemanagementoption ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @fire_triggers_on_snapshot = ] 'fire_triggers_on_snapshot' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`アーティクルを含むパブリケーションの名前を指定します。 名前はデータベース内で一意である必要があります。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @article = ] 'article'`アーティクルの名前を指定します。 名前はパブリケーション内で一意であることが必要です。 *アーティクル*は**sysname**で、既定値はありません。  
  
`[ @source_table = ] 'source_table'`このパラメーターは非推奨とされました。代わりに*source_object*を使用してください。  
  
 *このパラメーターは、Oracle パブリッシャーではサポートされていません。*  
  
`[ @destination_table = ] 'destination_table'`*ソーステーブル*またはストアドプロシージャと異なる場合に、インポート先 (サブスクリプション) テーブルの名前を指定します。 *destination_table*は**sysname**の既定値は NULL には、つまり*source_table*と等しい*destination_table **。*  
  
`[ @vertical_partition = ] 'vertical_partition'`テーブルアーティクルの列フィルター処理を有効または無効にします。 *vertical_partition*は**nchar (5)** ,、既定値は FALSE です。  
  
 **false**は、列方向のフィルター処理が行われず、すべての列がパブリッシュされることを示します。  
  
 **true**を設定すると、宣言された主キー、null 値を許容する列、および一意のキー列を除くすべての列が消去されます。 列は[sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)を使用して追加されます。  
  
`[ @type = ] 'type'`アーティクルの種類を示します。 *種類*は**sysname**で、次のいずれかの値を指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**集計スキーマのみ**|スキーマのみを使用する集計関数。|  
|**func スキーマのみ**|スキーマのみを使用する関数。|  
|**インデックス付きビュー logbased**|ログベースのインデックス付きビューアーティクル。 Oracle パブリッシャーではサポートされていません。 この種類の記事では、ベーステーブルを個別にパブリッシュする必要はありません。|  
|**インデックス付きビュー logbased manualboth**|手動フィルターと手動ビューを使用する、ログベースのインデックス付きビュー アーティクルです。 このオプションでは、 *sync_object*パラメーターと*filter*パラメーターの両方を指定する必要があります。 この種類の記事では、ベーステーブルを個別にパブリッシュする必要はありません。 Oracle パブリッシャーではサポートされていません。|  
|**インデックス付きビュー logbased manualfilter**|手動フィルターを使用したログベースのインデックス付きビューアーティクル。 このオプションでは、 *sync_object*パラメーターと*filter*パラメーターの両方を指定する必要があります。 この種類の記事では、ベーステーブルを個別にパブリッシュする必要はありません。 Oracle パブリッシャーではサポートされていません。|  
|**インデックス付きビュー logbased manualview**|手動ビューを使用する、ログベースのインデックス付きビュー アーティクルです。 このオプションでは、 *sync_object*パラメーターを指定する必要があります。 この種類の記事では、ベーステーブルを個別にパブリッシュする必要はありません。 Oracle パブリッシャーではサポートされていません。|  
|**インデックス付きビュースキーマのみ**|スキーマのみを使用するインデックス付きビュー。 この種類のアーティクルでは、ベーステーブルもパブリッシュする必要があります。|  
|**logbased**標準|ログベースのアーティクル。|  
|**logbased manualboth**|手動フィルターと手動ビューを使用したログベースのアーティクル。 このオプションでは、 *sync_object*パラメーターと*filter*パラメーターの両方を指定する必要があります。 Oracle パブリッシャーではサポートされていません。|  
|**logbased manualfilter**|手動フィルターを使用したログベースのアーティクル。 このオプションでは、 *sync_object*パラメーターと*filter*パラメーターの両方を指定する必要があります。 Oracle パブリッシャーではサポートされていません。|  
|**logbased manualview**|手動ビューを使用する、ログベースのアーティクルです。 このオプションでは、 *sync_object*パラメーターを指定する必要があります。 Oracle パブリッシャーではサポートされていません。|  
|**proc exec**|アーティクルのすべてのサブスクライバーにストアド プロシージャの実行をレプリケートします。 Oracle パブリッシャーではサポートされていません。 **Proc exec**ではなく**serializable proc exec**オプションを使用することをお勧めします。 詳細については、「[トランザクションレプリケーションでのストアドプロシージャの実行のパブリッシュ](../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)」の「ストアドプロシージャの実行に関する記事の種類」を参照してください。 変更データ キャプチャが有効な場合は使用できません。|  
|**proc スキーマのみ**|スキーマのみを使用するプロシージャ。 Oracle パブリッシャーではサポートされていません。|  
|**serializable proc exec**|シリアライゼーション可能なトランザクションのコンテキスト内で実行される場合にのみ、ストアド プロシージャの実行をレプリケートします。 Oracle パブリッシャーではサポートされていません。<br /><br /> プロシージャは、プロシージャの実行をレプリケートするために、明示的なトランザクション内で実行する必要もあります。|  
|**スキーマのみを表示**|スキーマのみを使用するビュー。 Oracle パブリッシャーではサポートされていません。 このオプションを使用する場合は、ベーステーブルもパブリッシュする必要があります。|  
  
`[ @filter = ] 'filter'`テーブルを水平方向にフィルター選択するために使用されるストアドプロシージャ (FOR REPLICATION で作成) です。 *フィルター*は**nvarchar (386)** ,、既定値は NULL です。 ビューとフィルターストアドプロシージャを作成するには、 [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)と[sp_articlefilter](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)を手動で実行する必要があります。 NULL 以外を指定した場合は、ストアド プロシージャが手動で作成されるものと見なされるため、フィルター プロシージャは作成されません。  
  
`[ @sync_object = ] 'sync_object'`このアーティクルのスナップショットを表すために使用するデータファイルの生成に使用されるテーブルまたはビューの名前を指定します。 *sync_object*は**nvarchar (386)** ,、既定値は NULL です。 NULL の場合、 [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)が呼び出され、出力ファイルの生成に使用するビューが自動的に作成されます。 このエラーは、 [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)を使用して列を追加した後に発生します。 NULL 以外を指定した場合は、ビューが手動で作成されるものと見なされるため、ビューは作成されません。  
  
`[ @ins_cmd = ] 'ins_cmd'`このアーティクルの挿入をレプリケートするときに使用されるレプリケーションコマンドの種類を示します。 *ins_cmd*は**nvarchar (255)** ,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**NONE**|アクションは実行されません。|  
|**Sp_MSins_ の呼び出し**<br /> **_テーブル_** 標準<br /><br /> \- または -<br /><br /> **Custom_stored_procedure_name の呼び出し**|サブスクライバー側で実行されるストアド プロシージャを呼び出します。 このレプリケーション方法を使用するには、 *schema_option*を使用してストアドプロシージャの自動作成を指定するか、アーティクルの各サブスクライバーの転送先データベースに指定されたストアドプロシージャを作成します。 *custom_stored_procedure* 、ユーザーが作成したストアドプロシージャの名前を指定します。 <strong>sp_MSins_*テーブル*</strong>には、パラメーターの*テーブル*部分の代わりに、変換先テーブルの名前が含まれています。 *Destination_owner*を指定すると、コピー先のテーブル名の前に付加されます。 たとえば、サブスクライバーで**実稼働**スキーマによって所有さ`CALL sp_MSins_ProductionProductCategory`れている**productcategory**テーブルの場合、パラメーターはになります。 ピアツーピアレプリケーショントポロジ内のアーティクルの場合、*テーブル*には GUID 値が付加されます。 *Custom_stored_procedure*の指定は、サブスクライバーの更新ではサポートされていません。|  
|**SQL**または NULL|INSERT ステートメントをレプリケートします。 INSERT ステートメントでは、アーティクル内にある、パブリッシュされるすべての列の値が指定されます。 次のコマンドは挿入時にレプリケートされます。<br /><br /> `INSERT INTO <table name> VALUES (c1value, c2value, c3value, ..., cnvalue)`|  
  
 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
`[ @del_cmd = ] 'del_cmd'`このアーティクルの削除をレプリケートするときに使用するレプリケーションコマンドの種類を示します。 *del_cmd*は**nvarchar (255)** ,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**NONE**|アクションは実行されません。|  
|**CALLsp_MSdel_**<br /> **_テーブル_** 標準<br /><br /> \- または -<br /><br /> **Custom_stored_procedure_name の呼び出し**|サブスクライバー側で実行されるストアド プロシージャを呼び出します。 このレプリケーション方法を使用するには、 *schema_option*を使用してストアドプロシージャの自動作成を指定するか、アーティクルの各サブスクライバーの転送先データベースに指定されたストアドプロシージャを作成します。 *custom_stored_procedure* 、ユーザーが作成したストアドプロシージャの名前を指定します。 <strong>sp_MSdel_*テーブル*</strong>には、パラメーターの*テーブル*部分の代わりに、変換先テーブルの名前が含まれています。 *Destination_owner*を指定すると、コピー先のテーブル名の前に付加されます。 たとえば、サブスクライバーで**実稼働**スキーマによって所有さ`CALL sp_MSdel_ProductionProductCategory`れている**productcategory**テーブルの場合、パラメーターはになります。 ピアツーピアレプリケーショントポロジ内のアーティクルの場合、*テーブル*には GUID 値が付加されます。 *Custom_stored_procedure*の指定は、サブスクライバーの更新ではサポートされていません。|  
|**XCALL sp_MSdel_**<br /> **_一覧_**<br /><br /> \- または -<br /><br /> **XCALL custom_stored_procedure_name**|XCALL スタイルのパラメーターを使用してストアド プロシージャを呼び出します。 このレプリケーション方法を使用するには、 *schema_option*を使用してストアドプロシージャの自動作成を指定するか、アーティクルの各サブスクライバーの転送先データベースに指定されたストアドプロシージャを作成します。 ユーザーが作成したストアドプロシージャの指定は、サブスクライバーの更新では許可されていません。|  
|**SQL**または NULL|DELETE ステートメントをレプリケートします。 DELETE ステートメントには、すべての主キー列の値が指定されています。 このコマンドは、削除時にレプリケートされます。<br /><br /> `DELETE FROM <table name> WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
`[ @upd_cmd = ] 'upd_cmd'`このアーティクルの更新をレプリケートするときに使用されるレプリケーションコマンドの種類を示します。 *upd_cmd*は**nvarchar (255)** ,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**NONE**|アクションは実行されません。|  
|**Sp_MSupd_ の呼び出し**<br /> **_一覧_**<br /><br /> \- または -<br /><br /> **Custom_stored_procedure_name の呼び出し**|サブスクライバー側で実行されるストアド プロシージャを呼び出します。 このレプリケーション方法を使用するには、 *schema_option*を使用してストアドプロシージャの自動作成を指定するか、アーティクルの各サブスクライバーの転送先データベースに指定されたストアドプロシージャを作成します。|  
|**MCALL sp_MSupd_**<br /> **_一覧_**<br /><br /> \- または -<br /><br /> **MCALL custom_stored_procedure_name**|MCALL スタイルパラメーターを取得するストアドプロシージャを呼び出します。 このレプリケーション方法を使用するには、 *schema_option*を使用してストアドプロシージャの自動作成を指定するか、アーティクルの各サブスクライバーの転送先データベースに指定されたストアドプロシージャを作成します。 *custom_stored_procedure* 、ユーザーが作成したストアドプロシージャの名前を指定します。 <strong>sp_MSupd_*テーブル*</strong>には、パラメーターの*テーブル*部分の代わりに、変換先テーブルの名前が含まれています。 *Destination_owner*を指定すると、コピー先のテーブル名の前に付加されます。 たとえば、サブスクライバーで**実稼働**スキーマによって所有さ`MCALL sp_MSupd_ProductionProductCategory`れている**productcategory**テーブルの場合、パラメーターはになります。 ピアツーピアレプリケーショントポロジ内のアーティクルの場合、*テーブル*には GUID 値が付加されます。 ユーザーが作成したストアドプロシージャの指定は、サブスクライバーの更新では許可されていません。|  
|**SCALL sp_MSupd_**<br /> **_テーブル_** 標準<br /><br /> \- または -<br /><br /> **SCALL custom_stored_procedure_name**|SCALL スタイルパラメーターを受け取るストアドプロシージャを呼び出します。 このレプリケーション方法を使用するには、 *schema_option*を使用してストアドプロシージャの自動作成を指定するか、アーティクルの各サブスクライバーの転送先データベースに指定されたストアドプロシージャを作成します。 *custom_stored_procedure* 、ユーザーが作成したストアドプロシージャの名前を指定します。 <strong>sp_MSupd_*テーブル*</strong>には、パラメーターの*テーブル*部分の代わりに、変換先テーブルの名前が含まれています。 *Destination_owner*を指定すると、コピー先のテーブル名の前に付加されます。 たとえば、サブスクライバーで**実稼働**スキーマによって所有さ`SCALL sp_MSupd_ProductionProductCategory`れている**productcategory**テーブルの場合、パラメーターはになります。 ピアツーピアレプリケーショントポロジ内のアーティクルの場合、*テーブル*には GUID 値が付加されます。 ユーザーが作成したストアドプロシージャの指定は、サブスクライバーの更新では許可されていません。|  
|**XCALL sp_MSupd_**<br /> **_一覧_**<br /><br /> \- または -<br /><br /> **XCALL custom_stored_procedure_name**|XCALL スタイルのパラメーターを使用してストアド プロシージャを呼び出します。 このレプリケーション方法を使用するには、 *schema_option*を使用してストアドプロシージャの自動作成を指定するか、アーティクルの各サブスクライバーの転送先データベースに指定されたストアドプロシージャを作成します。 ユーザーが作成したストアドプロシージャの指定は、サブスクライバーの更新では許可されていません。|  
|**SQL**または NULL|UPDATE ステートメントをレプリケートします。 UPDATE ステートメントでは、すべての列の値と主キー列の値が指定されます。 このコマンドは更新時にレプリケートされます。<br /><br /> `UPDATE <table name> SET c1 = c1value, SET c2 = c2value, SET cn = cnvalue WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
> [!NOTE]  
>  CALL、MCALL、SCALL、および XCALL 構文は、サブスクライバーに反映されるデータの量が異なります。 CALL 構文では、挿入されたすべての列および削除されたすべての列に関するすべての値が渡されます。 SCALL 構文では、影響を受けた列の値のみが渡されます。 XCALL 構文は、列の前の値を含め、変更されたかどうかにかかわらず、すべての列の値を渡します。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
`[ @creation_script = ] 'creation_script'`サブスクリプションデータベースでアーティクルを作成するために使用する、オプションのアーティクルスキーマスクリプトのパスと名前を指定します。 *creation_script*は**nvarchar (255)** ,、既定値は NULL です。  
  
`[ @description = ] 'description'`アーティクルの内容を示すエントリです。 *説明*は**nvarchar (255)** ,、既定値は NULL です。  
  
`[ @pre_creation_cmd = ] 'pre_creation_cmd'`このアーティクルのスナップショットを適用するときに、サブスクライバーで同じ名前の既存のオブジェクトが検出された場合にシステムが実行する操作を指定します。 *pre_creation_cmd*は**nvarchar (10)** ,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**none**|コマンドを使用しません。|  
|**delete**|スナップショットを適用する前に、レプリケーション先テーブルからデータを削除します。 アーティクルが行方向にフィルター選択されると、フィルター句によって指定された列のデータのみが削除されます。 行フィルターが定義されている場合は、Oracle パブリッシャーに対してはサポートされません。|  
|**ドロップ**標準|変換先テーブルを削除します。|  
|**truncate**|変換先テーブルを切り捨てます。 は、ODBC または OLE DB のサブスクライバーに対しては無効です。|  
  
`[ @filter_clause = ] 'filter_clause'`は、水平フィルターを定義する restriction (WHERE) 句です。 制限句を入力する場合は、WHERE キーワードを省略します。 *filter_clause*は**ntext**,、既定値は NULL です。 詳細については、「[パブリッシュされたデータのフィルター選択](../../relational-databases/replication/publish/filter-published-data.md)」を参照してください。  
  
`[ @schema_option = ] schema_option`指定されたアーティクルのスキーマ生成オプションのビットマスクです。 *schema_option*は**binary (8)** ,、| を指定することができます。 [(ビットごとの OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md)次の1つまたは複数の値の積:  
  
> [!NOTE]  
>  この値が NULL の場合は、他のアーティクルのプロパティに応じて、アーティクルの有効なスキーマ オプションが自動生成されます。 「解説」に記載されている**既定のスキーマオプション**の表は、アーティクルの種類とレプリケーションの種類の組み合わせに基づいて選択される値を示しています。  
  
|値|説明|  
|-----------|-----------------|  
|**0x00**|スナップショットエージェントによるスクリプト作成を無効にし、 *creation_script*を使用します。|  
|**0x01**|オブジェクト作成スクリプト (CREATE TABLE、CREATE PROCEDURE など) を生成します。 この値は、ストアドプロシージャアーティクルの既定値です。|  
|**除く**|定義されている場合、アーティクルの変更を反映するストアド プロシージャを生成します。|  
|**0x04**|Id 列は、IDENTITY プロパティを使用してスクリプト化されます。|  
|**0x08**|**タイムスタンプ**列をレプリケートします。 設定しない場合、**タイムスタンプ**列は**バイナリ**としてレプリケートされます。|  
|**0x10**|対応するクラスター化インデックスを生成します。 このオプションが設定されていない場合でも、主キーと一意の制約に関連するインデックスは、パブリッシュされたテーブルで既に定義されている場合に生成されます。|  
|**0x20**|ユーザー定義データ型 (UDT) をサブスクライバー側の基本データ型に変換します。 Udt 列に CHECK 制約または DEFAULT 制約がある場合、UDT 列が主キーの一部である場合、または計算列が UDT 列を参照している場合は、このオプションを使用できません。 *Oracle パブリッシャーではサポートされていません*。|  
|**0x40**|対応する非クラスター化インデックスを生成します。 このオプションが設定されていない場合でも、主キーと一意の制約に関連するインデックスは、パブリッシュされたテーブルで既に定義されている場合に生成されます。|  
|**0x80**|主キー制約をレプリケートします。 オプションの**0x10**と**0x40**が有効になっていない場合でも、制約に関連するすべてのインデックスもレプリケートされます。|  
|**0x100**|定義されている場合、テーブル アーティクル上のユーザー トリガーをレプリケートします。 *Oracle パブリッシャーではサポートされていません*。|  
|**0x200**|Foreign key 制約をレプリケートします。 参照先のテーブルがパブリケーションの一部でない場合、パブリッシュされたテーブルのすべての foreign key 制約はレプリケートされません。 *Oracle パブリッシャーではサポートされていません*。|  
|**0x400**|Check 制約をレプリケートします。 *Oracle パブリッシャーではサポートされていません*。|  
|**0x800**|既定値をレプリケートします。 *Oracle パブリッシャーではサポートされていません*。|  
|**0x1000**|列レベルの照合順序をレプリケートします。<br /><br /> **注:** Oracle パブリッシャーの場合は、このオプションを設定して、大文字と小文字を区別する比較を有効にする必要があります。|  
|**0x2000**|パブリッシュされたアーティクルのソースオブジェクトに関連付けられた拡張プロパティをレプリケートします。 *Oracle パブリッシャーではサポートされていません*。|  
|**0x4000**|UNIQUE 制約をレプリケートします。 オプションの**0x10**と**0x40**が有効になっていない場合でも、制約に関連するすべてのインデックスもレプリケートされます。|  
|**0x8000**|このオプションは、パブリッシャーに[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]対しては無効です。|  
|**0x10000**|CHECK 制約を NOT FOR REPLICATION としてレプリケートし、同期中に制約が適用されないようにします。|  
|**0x20000**|では、制約が同期中に適用されないように、外部キー制約は NOT FOR REPLICATION としてレプリケートされます。|  
|**0x40000**|パーティション テーブルまたはインデックスに関連付けられているファイル グループをレプリケートします。|  
|**0x80000**|パーティション テーブルのパーティション構成をレプリケートします。|  
|**0x100000**|パーティションインデックスのパーティション構成をレプリケートします。|  
|**0x200000**|テーブルの統計をレプリケートします。|  
|**0x400000**|既定のバインドです。|  
|**0x800000**|ルールのバインドです。|  
|**0x1000000**|フルテキスト インデックスです。|  
|**0x2000000**|**Xml**列にバインドされている xml スキーマコレクションはレプリケートされません。|  
|**0x4000000**|**Xml**列のインデックスをレプリケートします。|  
|**0x8000000**|サブスクライバーにまだ存在しないスキーマを作成します。|  
|**0x10000000**|サブスクライバーで**xml**列を**ntext**に変換します。|  
|**0x20000000**|で[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]導入されたラージオブジェクトデータ型 (**nvarchar (max)** 、 **varchar (max)** 、 **varbinary (max)** ) を、でサポートされ[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]ているデータ型に変換します。|  
|**0x40000000**|権限をレプリケートします。|  
|**0x80000000 です**|パブリケーションに含まれていないオブジェクトへの依存関係を削除しようとしています。|  
|**0x100000000**|このオプションを使用すると、 **varbinary (max)** 列に FILESTREAM 属性が指定されている場合に、その属性をレプリケートできます。 テーブルをサブスクライバーに[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]レプリケートする場合は、このオプションを指定しないでください。 このスキーマオプションを設定する方法[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]に関係なく、FILESTREAM 列を持つテーブルをサブスクライバーにレプリケートすることはサポートされていません。<br /><br /> 関連オプション**0x800000000**を参照してください。|  
|**0x200000000**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で導入[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]された日付と時刻のデータ型 (date、 **time**、datetimeoffset、および datetime2) を、以前のバージョンのでサポートされているデータ型に変換します。|  
|**0x400000000**|データとインデックスの圧縮オプションをレプリケートします。 詳細については、「[Data Compression](../../relational-databases/data-compression/data-compression.md)」を参照してください。|  
|**0x800000000**|このオプションを設定すると、サブスクライバーの独自のファイル グループに FILESTREAM データを格納できます。 このオプションが設定されていない場合、FILESTREAM データは既定のファイルグループに格納されます。 レプリケーションでは、ファイルグループは作成されません。したがって、このオプションを設定する場合は、サブスクライバーでスナップショットを適用する前にファイルグループを作成する必要があります。 スナップショットを適用する前にオブジェクトを作成する方法の詳細については、「[スナップショットが適用される前および後のスクリプトの実行](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)」を参照してください。<br /><br /> 関連オプション**0x100000000**を参照してください。|  
|**0x1000000000**|2バイトを8000超える共通言語ランタイム (CLR) ユーザー定義型 (Udt) を**varbinary (max)** に変換します。これにより、udt 型の列を、を実行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]しているサブスクライバーにレプリケートできるようになります。|  
|**0x2000000000**|**Hierarchyid**データ型を**varbinary (max)** に変換します。これにより、 **hierarchyid**型の列を、を[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]実行しているサブスクライバーにレプリケートできるようになります。 レプリケートされたテーブルでの**hierarchyid**列の使用方法の詳細については、「[hierarchyid &#40;transact-sql&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)」を参照してください。|  
|**0x4000000000**|テーブルのフィルター選択されたインデックスをレプリケートします。 フィルター選択されたインデックスの詳細については、「[フィルター選択](../../relational-databases/indexes/create-filtered-indexes.md)されたインデックスの作成」をご覧ください。|  
|**0x8000000000**|**Geography**および**geometry**データ型を**varbinary (max)** に変換して、これらの型の列を、を実行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]しているサブスクライバーにレプリケートできるようにします。|  
|**0x10000000000**|**Geography**型および**geometry**型の列のインデックスをレプリケートします。|  
|**0x20000000000**|列のスパース属性をレプリケートします。 この属性の詳細については、「[スパース列の使用](../../relational-databases/tables/use-sparse-columns.md)」を参照してください。|  
|**0x40000000000**|サブスクライバーにメモリ最適化テーブルを作成するには、スナップショットエージェントによるスクリプト作成を有効にします。|  
|**0x80000000000**|メモリ最適化アーティクルのクラスター化インデックスを非クラスター化インデックスに変換します。|  
|**0x400000000000**|テーブルの非クラスター化列ストアインデックスをレプリケートします。|  
|**0x800000000000**|テーブルのすべての flitered リングされた非クラスター化列ストアインデックスをレプリケートします。|  
|NULL|レプリケーションでは、 *schema_option*が既定値に自動的に設定されます。この値は、他のアーティクルのプロパティによって異なります。 「解説」の「既定のスキーマオプション」の表は、アーティクルの種類とレプリケーションの種類に基づく既定のスキーマオプションを示しています。<br /><br /> 以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリケーションの既定値は**0x050d3**です。|  
  
 すべての*schema_option*値がすべての種類のレプリケーションとアーティクルの種類に対して有効であるとは限りません。 「解説」の**有効なスキーマオプション**の表は、アーティクルの種類とレプリケーションの種類の組み合わせに基づいて選択できる有効なスキーマオプションを示しています。  
  
`[ @destination_owner = ] 'destination_owner'`対象オブジェクトの所有者の名前を指定します。 *destination_owner*は**sysname**,、既定値は NULL です。 *Destination_owner*が指定されていない場合、所有者は次の規則に基づいて自動的に指定されます。  
  
|条件|対象オブジェクトの所有者|  
|---------------|------------------------------|  
|パブリケーションはネイティブ モードの一括コピーを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバーのみをサポートする初期スナップショットを生成します。|既定値は*source_owner*です。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリッシャーからパブリッシュされます。|既定では、転送先データベースの所有者になります。|  
|パブリケーションでは、キャラクターモードの一括コピーを使用して、以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のサブスクライバーをサポートする初期スナップショットを生成します。|割り当てられていません。|  
  
 以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のサブスクライバーをサポートするには、 *destination_owner*を NULL にする必要があります。  
  
`[ @status = ] status`アーティクルがアクティブかどうか、および変更の反映方法に関する追加オプションを指定します。 *状態*は**tinyint**で、| を指定できます。 [(ビットごとの OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md)これらの値の1つ以上の積。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|アーティクルはアクティブです。|  
|**8**|INSERT ステートメントに列名を含めます。|  
|**16** (既定値)|パラメーター化されたステートメントを使用します。|  
|**24**|INSERT ステートメントに列名を含め、パラメーター化されたステートメントを使用します。|  
|**64**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 たとえば、パラメーター化されたステートメントを使用するアクティブなアーティクルの場合、この列の値は 17 になります。 値**0**は、アーティクルが非アクティブであり、追加のプロパティが定義されていないことを示します。  
  
`[ @source_owner = ] 'source_owner'`は、ソースオブジェクトの所有者です。 *source_owner*は**sysname**,、既定値は NULL です。 Oracle パブリッシャーの場合は、 *source_owner*を指定する必要があります。  
  
`[ @sync_object_owner = ] 'sync_object_owner'`パブリッシュされたアーティクルを定義するビューの所有者を示します。 *sync_object_owner*は**sysname**,、既定値は NULL です。  
  
`[ @filter_owner = ] 'filter_owner'`フィルターの所有者を選択します。 *filter_owner*は**sysname**,、既定値は NULL です。  
  
`[ @source_object = ] 'source_object'`パブリッシュするデータベースオブジェクトを指定します。 *source_object*は**sysname**,、既定値は NULL です。 *ソーステーブル*が null の場合、 *source_object*を null にすることはできません。*ソーステーブル*の代わりに*source_object*を使用する必要があります。 スナップショットレプリケーションまたはトランザクションレプリケーションを使用してパブリッシュできるオブジェクトの種類の詳細については、「[データとデータベースオブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)」を参照してください。  
  
`[ @artid = ] _article_ID_ OUTPUT`新しいアーティクルのアーティクル ID を示します。 *コ*は**int** 、既定値は NULL の場合、出力パラメーターです。  
  
`[ @auto_identity_range = ] 'auto_identity_range'`パブリケーションの作成時に、パブリケーションに対する自動 id 範囲処理を有効または無効にします。 *auto_identity_range*は**nvarchar (5)** ,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**true**|自動 id 範囲の処理を有効にします|  
|**false**|自動 ID 範囲処理を無効にします。|  
|NULL (既定値)|Id 範囲の処理は、 *identityrangemanagementoption*によって設定されます。|  
  
> [!NOTE]  
>  *auto_identity_range*は非推奨とされており、旧バージョンとの互換性のために用意されています。 Id 範囲管理オプションを指定するには、 *identityrangemanagementoption*を使用する必要があります。 詳細については、「[ID 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)」を参照してください。  
  
`[ @pub_identity_range = ] pub_identity_range`アーティクルの*identityrangemanagementoption*が**auto**に設定されているか、 *auto_identity_range*が**true**に設定されている場合、パブリッシャーでの範囲サイズを制御します。 *pub_identity_range*は**bigint**,、既定値は NULL です。 *Oracle パブリッシャーではサポートされていません*。  
  
`[ @identity_range = ] identity_range`アーティクルの*identityrangemanagementoption*が**auto**に設定されているか、 *auto_identity_range*が**true**に設定されている場合、サブスクライバーでの範囲のサイズを制御します。 *identity_range*は**bigint**,、既定値は NULL です。 *Auto_identity_range*が**true**に設定されている場合に使用します。 *Oracle パブリッシャーではサポートされていません*。  
  
`[ @threshold = ] threshold`ディストリビューションエージェントが新しい id 範囲を割り当てるタイミングを制御するパーセンテージの値です。 [*しきい*値] で指定した値のパーセンテージが使用されると、ディストリビューションエージェントによって新しい id 範囲が作成されます。 *しきい値*は**bigint**,、既定値は NULL です。 *Identityrangemanagementoption*が**auto**に設定されている場合、または*auto_identity_range*が**true**に設定されている場合に使用します。 *Oracle パブリッシャーではサポートされていません*。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`このストアドプロシージャによって実行される操作によって既存のスナップショットが無効になる可能性があることを確認します。 *force_invalidate_snapshot*は**ビット**,、既定値は0です。  
  
 **0**に設定すると、アーティクルを追加してもスナップショットが無効になることはありません。 変更に新しいスナップショットが必要であることをストアド プロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1**に設定すると、アーティクルの追加によってスナップショットが無効になる場合があります。また、新しいスナップショットを必要とするサブスクリプションが存在する場合は、既存のスナップショットを古い形式としてマークし、新しいスナップショットを生成することができます。  
  
`[ @use_default_datatypes = ] use_default_datatypes`Oracle パブリッシャーからアーティクルをパブリッシュするときに、列の既定のデータ型マッピングを使用するかどうかを指定します。 *use_default_datatypes*はビット,、既定値は1です。  
  
 **1** = 既定のアーティクル列マッピングが使用されます。 既定のデータ型のマッピングを表示するには、 [sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)を実行します。  
  
 **0** = カスタムアーティクル列のマッピングが定義されているため、 [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)は**sp_addarticle**によって呼び出されません。  
  
 *Use_default_datatypes*が**0**に設定されている場合は、列マッピングが既定値から変更されるたびに[sp_changearticlecolumndatatype](../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md)を実行する必要があります。 すべてのカスタム列マッピングが定義されたら、 [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)を実行する必要があります。  
  
> [!NOTE]  
>  このパラメーターは、Oracle パブリッシャーに対してのみ使用してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーに対して*use_default_datatypes*を**0**に設定すると、エラーが生成されます。  
  
`[ @identityrangemanagementoption = ] identityrangemanagementoption`アーティクルに対する id 範囲管理の処理方法を指定します。 *identityrangemanagementoption*は**nvarchar (10)** ,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**none**|明示的な ID 範囲の管理は行われません。 このオプションは、以前のバージョンの SQL Server との下位互換性のためにのみ推奨されます。 ピアレプリケーションには許可されていません。|  
|**手動**|NOT FOR REPLICATION を使用して id 列をマークし、手動による id 範囲処理を有効にします。|  
|**auto**|Id 範囲の自動管理を指定します。|  
|NULL (既定値)|*Auto_identity_range*の値が**true**でない場合、既定値は**none**です。 既定では、ピアツーピアトポロジの既定値は **[手動]** になります (*auto_identity_range*は無視されます)。|  
  
 旧バージョンとの互換性のために、 *identityrangemanagementoption*の値が NULL の場合、 *auto_identity_range*の値がチェックされます。 ただし、 *identityrangemanagementoption*の値が NULL でない場合、 *auto_identity_range*の値は無視されます。  
  
 詳細については、「[ID 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)」を参照してください。  
  
`[ @publisher = ] 'publisher'`以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーを指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーにアーティクルを追加する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーを使用しないでください。  
  
`[ @fire_triggers_on_snapshot = ] 'fire_triggers_on_snapshot'`初期スナップショットが適用されるときに、レプリケートされたユーザートリガーが実行されるかどうかを示します。 *fire_triggers_on_snapshot*は**nvarchar (5)** ,、既定値は FALSE。 **true**は、スナップショットが適用されるときに、レプリケートされたテーブルのユーザートリガーが実行されることを意味します。 トリガーをレプリケートするには、ビットマスク値*schema_option*に値**0x100**を含める必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_addarticle**は、スナップショットレプリケーションまたはトランザクションレプリケーションで使用します。  
  
 既定では、列データ型がレプリケーションによってサポートされていない場合は、レプリケーションによってソース テーブル内の列がパブリッシュされることはありません。 このような列をパブリッシュする必要がある場合は、 [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)を実行して列を追加する必要があります。  
  
 ピアツーピアトランザクションレプリケーションをサポートするパブリケーションにアーティクルを追加する場合は、次の制限が適用されます。  
  
-   パラメーター化されたステートメントは、すべての logbased アーティクルに対して指定する必要があります。 *Status*値には**16**を含める必要があります。  
  
-   コピー先のテーブルの名前と所有者は、ソーステーブルと一致している必要があります。  
  
-   アーティクルは、行方向または列方向にフィルター選択することはできません。  
  
-   自動 ID 範囲管理はサポートされていません。 *Identityrangemanagementoption*の値に manual を指定する必要があります。  
  
-   **Timestamp**列がテーブル内に存在する場合は、列を**timestamp**としてレプリケートするために、 *schema_option*に0x08 を含める必要があります。  
  
-   *Ins_cmd*、 *upd_cmd*、および*del_cmd*には、 **SQL**の値を指定できません。  
  
 詳細については、「[ピア ツー ピア トランザクション レプリケーション](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)」を参照してください。  
  
 オブジェクトをパブリッシュすると、その定義がサブスクライバーにコピーされます。 1つ以上の他のオブジェクトに依存するデータベースオブジェクトをパブリッシュする場合は、参照されているすべてのオブジェクトをパブリッシュする必要があります。 たとえば、テーブルに依存しているビューをパブリッシュする場合は、そのテーブルもパブリッシュする必要があります。  
  
 *Vertical_partition*が**true**に設定されている場合、 **sp_addarticle**は、(最後の[sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)が追加された後に) [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)が呼び出されるまで、ビューの作成を延期します。  
  
 パブリケーションで更新サブスクリプションが許可されていて、パブリッシュされたテーブルに**uniqueidentifier**列がない場合、 **sp_addarticle**は自動的に**uniqueidentifier**列をテーブルに追加します。  
  
 の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスではないサブスクライバー (異種レプリケーション) にレプリケートする場合、 **INSERT**、 [!INCLUDE[tsql](../../includes/tsql-md.md)] **UPDATE**、および**DELETE**の各コマンドに対してステートメントのみがサポートされます。  
  
 ログリーダーエージェントが実行されている場合、ピアツーピアパブリケーションにアーティクルを追加すると、ログリーダーエージェントとアーティクルを追加するプロセスの間でデッドロックが発生する可能性があります。 この問題を回避するには、アーティクルをピアツーピアパブリケーションに追加する前に、レプリケーションモニターを使用して、アーティクルを追加するノード上のログリーダーエージェントを停止します。 アーティクルを追加した後、ログリーダーエージェントを再起動します。  
  
 または`@del_cmd = 'NONE'` `@ins_cmd = 'NONE'`を設定するときに、制限された更新が行われたときにコマンドを送信しないことによって、**更新**コマンドの反映が影響を受ける可能性があります。 (制限付き更新とは、サブスクライバーで DELETE/INSERT ペアとしてレプリケートされる、パブリッシャーからの UPDATE ステートメントの種類です)。  
  
## <a name="default-schema-options"></a>既定のスキーマ オプション  
 次の表では、 *schema_options*がユーザーによって指定されていない場合に、レプリケーションによって設定される既定値について説明します。この値は、レプリケーションの種類 (上部に表示) とアーティクルの種類 (最初の列に表示されます) によって異なります。  
  
|アーティクルの種類|レプリケーションの種類||  
|------------------|----------------------|------|  
||トランザクション|スナップショット|  
|**集計スキーマのみ**|**0x01**|**0x01**|  
|**func スキーマのみ**|**0x01**|**0x01**|  
|**インデックス付きビュースキーマのみ**|**0x01**|**0x01**|  
|**インデックス付きビュー logbased**|**0x30F3**|**0x3071**|  
|**インデックス付きビュー底 manualboth**|**0x30F3**|**0x3071**|  
|**インデックス付きビュー logbased manualfilter**|**0x30F3**|**0x3071**|  
|**インデックス付きビュー logbased manualview**|**0x30F3**|**0x3071**|  
|**logbased**|**0x30F3**|**0x3071**|  
|**logbased manualfilter**|**0x30F3**|**0x3071**|  
|**logbased manualview**|**0x30F3**|**0x3071**|  
|**proc exec**|**0x01**|**0x01**|  
|**proc スキーマのみ**|**0x01**|**0x01**|  
|**serializable proc exec**|**0x01**|**0x01**|  
|**スキーマのみを表示**|**0x01**|**0x01**|  
  
> [!NOTE]
>  パブリケーションでキュー更新が有効になっている場合は、テーブルに表示される既定値に*schema_option*値**0x80**が追加されます。 以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリケーションの既定の*schema_option*は**0x050d3**です。  
  
## <a name="valid-schema-options"></a>有効なスキーマ オプション  
 次の表では、レプリケーションの種類 (上部に表示) とアーティクルの種類 (最初の列) に基づいて、使用可能な*schema_option*の値を示します。  
  
|アーティクルの種類|レプリケーションの種類||  
|------------------|----------------------|------|  
||トランザクション|スナップショット|  
|**logbased**|すべてのオプション|すべてのオプション ( **0x02** )|  
|**logbased manualfilter**|すべてのオプション|すべてのオプション ( **0x02** )|  
|**logbased manualview**|すべてのオプション|すべてのオプション ( **0x02** )|  
|**インデックス付きビュー logbased**|すべてのオプション|すべてのオプション ( **0x02** )|  
|**インデックス付きビュー logbased manualfilter**|すべてのオプション|すべてのオプション ( **0x02** )|  
|**インデックス付きビュー logbased manualview**|すべてのオプション|すべてのオプション ( **0x02** )|  
|**インデックス付きビュー底 manualboth**|すべてのオプション|すべてのオプション ( **0x02** )|  
|**proc exec**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x800000**、 **0x10000000**、 **0x20000000**、 **0x40000000**、および**0x80000000**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x800000**、 **0x10000000**、 **0x20000000**、 **0x40000000**、および**0x80000000**|  
|**serializable proc exec**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x800000**、 **0x10000000**、 **0x20000000**、 **0x40000000**、および**0x80000000**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x800000**、 **0x10000000**、 **0x20000000**、 **0x40000000**、および**0x80000000**|  
|**proc スキーマのみ**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x800000**、 **0x10000000**、 **0x20000000**、 **0x40000000**、および**0x80000000**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x800000**、 **0x10000000**、 **0x20000000**、 **0x40000000**、および**0x80000000**|  
|**スキーマのみを表示**|**0x01**、 **0x010**、 **0x020**、 **0x010**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x100000**、 **0x200000**、 **0x400000**、 **0x800000**、 **0x200000**、 **0x800000**、**0x40000000**、 **0x80000000**|**0x01**、 **0x010**、 **0x020**、 **0x010**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x100000**、 **0x200000**、 **0x400000**、 **0x800000**、 **0x200000**、 **0x800000**、**0x40000000**、 **0x80000000**|  
|**func スキーマのみ**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x800000**、 **0x10000000**、 **0x20000000**、 **0x40000000**、および**0x80000000**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x800000**、 **0x10000000**、 **0x20000000**、 **0x40000000**、および**0x80000000**|  
|**インデックス付きビュースキーマのみ**|**0x01**、 **0x010**、 **0x020**、 **0x010**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x100000**、 **0x200000**、 **0x400000**、 **0x800000**、 **0x200000**、 **0x800000**、**0x40000000**、 **0x80000000**|**0x01**、 **0x010**、 **0x020**、 **0x010**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x100000**、 **0x200000**、 **0x400000**、 **0x800000**、 **0x200000**、 **0x800000**、**0x40000000**、 **0x80000000**|  
  
> [!NOTE]
>  キュー更新パブリケーションの場合、 *schema_option*の値**0x8000**と**0x80**を有効にする必要があります。 以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリケーションでは、次のような*schema_option*値がサポートされます。**0x01**、 **0x02**、 **0x10**、 **0x40**、 **0x80**、 **0x1000**、 **0x4000** 、 **0x8000**。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-addarticle-transact-sql_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addarticle**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [アーティクルの定義](../../relational-databases/replication/publish/define-an-article.md)   
 [sp_articlecolumn (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_articlefilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_articleview &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [データとデータベース オブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
