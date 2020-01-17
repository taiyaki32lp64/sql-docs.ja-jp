---
title: sp_addmergearticle (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergearticle
- sp_addmergearticle_TSQL
helpviewer_keywords:
- sp_addmergearticle
ms.assetid: 0df654ea-24e2-4c61-a75a-ecaa7a140a6c
author: stevestein
ms.author: sstein
ms.openlocfilehash: a9163e6d34a0de6200eafd413d163bb6d92fd4a5
ms.sourcegitcommit: 79e6d49ae4632f282483b0be935fdee038f69cc2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2019
ms.locfileid: "72174003"
---
# <a name="sp_addmergearticle-transact-sql"></a>sp_addmergearticle (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  既存のマージパブリケーションにアーティクルを追加します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addmergearticle [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
        , [ @source_object = ] 'source_object'   
    [ , [ @type = ] 'type' ]   
    [ , [ @description = ] 'description' ]   
    [ , [ @column_tracking = ] 'column_tracking' ]   
    [ , [ @status = ] 'status' ]   
    [ , [ @pre_creation_cmd = ] 'pre_creation_cmd' ]   
    [ , [ @creation_script = ] 'creation_script' ]   
    [ , [ @schema_option = ] schema_option ]   
    [ , [ @subset_filterclause = ] 'subset_filterclause' ]   
    [ , [ @article_resolver = ] 'article_resolver' ]   
    [ , [ @resolver_info = ] 'resolver_info' ]   
    [ , [ @source_owner = ] 'source_owner' ]   
    [ , [ @destination_owner = ] 'destination_owner' ]   
    [ , [ @vertical_partition = ] 'vertical_partition' ]   
    [ , [ @auto_identity_range = ] 'auto_identity_range' ]   
    [ , [ @pub_identity_range = ] pub_identity_range ]   
    [ , [ @identity_range = ] identity_range ]   
    [ , [ @threshold = ] threshold ]   
    [ , [ @verify_resolver_signature = ] verify_resolver_signature ]   
    [ , [ @destination_object = ] 'destination_object' ]   
    [ , [ @allow_interactive_resolver = ] 'allow_interactive_resolver' ]   
    [ , [ @fast_multicol_updateproc = ] 'fast_multicol_updateproc' ]   
    [ , [ @check_permissions = ] check_permissions ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @published_in_tran_pub = ] 'published_in_tran_pub' ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @logical_record_level_conflict_detection = ] 'logical_record_level_conflict_detection' ]  
    [ , [ @logical_record_level_conflict_resolution = ] 'logical_record_level_conflict_resolution' ]  
    [ , [ @partition_options = ] partition_options ]  
    [ , [ @processing_order = ] processing_order ]  
    [ , [ @subscriber_upload_options = ] subscriber_upload_options ]  
    [ , [ @identityrangemanagementoption = ] 'identityrangemanagementoption' ]  
    [ , [ @delete_tracking = ] delete_tracking ]  
    [ , [ @compensate_for_errors = ] 'compensate_for_errors' ]   
    [ , [ @stream_blob_columns = ] 'stream_blob_columns' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` には、アーティクルを含むパブリケーションの名前を指定します。 *publication* は **sysname** 、既定値はありません。  
  
`[ @article = ] 'article'` には、アーティクルの名前を指定します。 名前はパブリケーション内で一意であることが必要です。 *アーティクル*は**sysname**で、既定値はありません。 *記事*は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を実行しているローカルコンピューター上にあり、識別子の規則に従っている必要があります。  
  
`[ @source_object = ] 'source_object'` は、パブリッシュされるデータベースオブジェクトです。 *source_object*は**sysname**であり、既定値はありません。 マージレプリケーションを使用してパブリッシュできるオブジェクトの種類の詳細については、「[データとデータベースオブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)」を参照してください。  
  
`[ @type = ] 'type'` はアーティクルの種類です。 *種類*は**sysname**で、既定値は**table**です。次のいずれかの値を指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**table** (既定値)|スキーマとデータを含むテーブル。 レプリケーションはテーブルを監視して、レプリケートするデータを特定します。|  
|**func schema only**|スキーマのみを使用する関数。|  
|**インデックス付きビュー** **スキーマのみ**|スキーマのみを使用するインデックス付きビュー。|  
|**proc schema only**|スキーマのみを使用するストアド プロシージャ。|  
|**synonym schema only**|スキーマのみを使用するシノニム。|  
|**view schema only**|スキーマのみを使用するビュー。|  
  
`[ @description = ] 'description'` は、アーティクルの説明です。 *説明*は**nvarchar (255)** ,、既定値は NULL です。  
  
`[ @column_tracking = ] 'column_tracking'` は、列レベルの追跡の設定です。 *column_tracking*は**nvarchar (10)** ,、既定値は FALSE です。 **true**列の追跡を有効にします。 **false**列の追跡をオフにし、競合の検出を行レベルで行います。 テーブルが他のマージ レプリケーションで既にパブリッシュされている場合は、このテーブルに基づく既存のアーティクルが使用しているものと同じ列追跡値を使用する必要があります。 このパラメーターは、テーブル アーティクルのみに固有のものです。  
  
> [!NOTE]  
>  行レベルの追跡を使用して競合を検出する場合 (既定値)、ベース テーブルには最大 1,024 列含めることができますが、最大 246 列がパブリッシュされるようにアーティクルから列をフィルター選択する必要があります。 列の追跡を使用する場合、ベース テーブルには最大 246 列を含めることができます。  
  
`[ @status = ] 'status'` は、アーティクルの状態です。 *状態*は**nvarchar (10)** ,、既定値は**同期**されていません。 **アクティブ**になっている場合は、テーブルをパブリッシュする初期処理スクリプトが実行されます。 **同期**されていない場合、テーブルをパブリッシュする初期処理スクリプトは、次にスナップショットエージェントを実行したときに実行されます。  
  
`[ @pre_creation_cmd = ] 'pre_creation_cmd'` は、スナップショットを適用するときに、サブスクライバーにテーブルが存在する場合にシステムが実行する処理を指定します。 *pre_creation_cmd*は**nvarchar (10)** で、次のいずれかの値を指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**存在**|テーブルがサブスクライバーに既に存在する場合、アクションは実行されません。|  
|**delete**|サブセットフィルターの WHERE 句に基づいて削除を発行します。|  
|**drop** (既定値)|テーブルを再作成する前に削除します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバーをサポートするために必要です。|  
|**truncate**|変換先テーブルを切り捨てます。|  
  
`[ @creation_script = ] 'creation_script'` は、サブスクリプションデータベースでアーティクルを作成するために使用される、オプションのアーティクルスキーマスクリプトのパスと名前です。 *creation_script*は**nvarchar (255)** ,、既定値は NULL です。  
  
> [!NOTE]  
>  作成スクリプトは [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバー上では実行されません。  
  
`[ @schema_option = ] schema_option` は、指定されたアーティクルのスキーマ生成オプションのビットマップです。 *schema_option*は**binary (8)** で、| を指定できます。 [(ビットごとの OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md)これらの値の1つ以上の積。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**0x00**|スナップショットエージェントによるスクリプト作成を無効にし、 *creation_script*で定義されているスキーマ作成前スクリプトを使用します。|  
|**0x01**|オブジェクトの作成 (CREATE TABLE、CREATE PROCEDURE など) を生成します。 これは、ストアドプロシージャアーティクルの既定値です。|  
|**0x10**|対応するクラスター化インデックスを生成します。 このオプションが設定されていない場合でも、パブリッシュされたテーブルに主キーと UNIQUE 制約が既に定義されている場合は、これらの主キーや制約に関連するインデックスが生成されます。|  
|**0x20**|ユーザー定義データ型 (UDT) をサブスクライバー側の基本データ型に変換します。 Udt 列に CHECK 制約または DEFAULT 制約がある場合、UDT 列が主キーの一部である場合、または計算列が UDT 列を参照している場合は、このオプションを使用できません。|  
|**0x40**|対応する非クラスター化インデックスを生成します。 このオプションが設定されていない場合でも、パブリッシュされたテーブルに主キーと UNIQUE 制約が既に定義されている場合は、これらの主キーや制約に関連するインデックスが生成されます。|  
|**0x80**|PRIMARY KEY 制約をレプリケートします。 オプションの**0x10**と**0x40**が有効になっていない場合でも、制約に関連するすべてのインデックスもレプリケートされます。|  
|**0x100**|定義されている場合、テーブル アーティクル上のユーザー トリガーをレプリケートします。|  
|**0x200**|FOREIGN KEY 制約をレプリケートします。 参照先のテーブルがパブリケーションの一部でない場合、パブリッシュされたテーブルのすべての FOREIGN KEY 制約はレプリケートされません。|  
|**0x400**|CHECK 制約をレプリケートします。|  
|**0x800**|既定値をレプリケートします。|  
|**0x1000**|列レベルの照合順序をレプリケートします。|  
|**0x2000**|パブリッシュされたアーティクルのソースオブジェクトに関連付けられた拡張プロパティをレプリケートします。|  
|**0x4000**|UNIQUE 制約をレプリケートします。 オプションの**0x10**と**0x40**が有効になっていない場合でも、制約に関連するすべてのインデックスもレプリケートされます。|  
|**0x8000**|このオプションは、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンを実行しているパブリッシャーでは有効ではありません。|  
|**0x10000**|CHECK 制約を NOT FOR REPLICATION としてレプリケートし、同期中に制約が適用されないようにします。|  
|**0x20000**|では、制約が同期中に適用されないように、外部キー制約は NOT FOR REPLICATION としてレプリケートされます。|  
|**0x40000**|パーティション テーブルまたはインデックスに関連付けられているファイル グループをレプリケートします。|  
|**0x80000**|パーティション テーブルのパーティション構成をレプリケートします。|  
|**0x100000**|パーティションインデックスのパーティション構成をレプリケートします。|  
|**0x200000**|テーブルの統計をレプリケートします。|  
|**0x400000**|既定のバインドをレプリケートします。|  
|**0x800000**|ルールのバインドをレプリケートします。|  
|**0x1000000**|フルテキストインデックスをレプリケートします。|  
|**0x2000000**|**Xml**列にバインドされている xml スキーマコレクションはレプリケートされません。|  
|**0x4000000**|**Xml**列のインデックスをレプリケートします。|  
|**0x8000000**|サブスクライバーにまだ存在しないスキーマを作成します。|  
|**0x10000000**|サブスクライバーで**xml**列を**ntext**に変換します。|  
|**0x20000000**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で導入されたラージオブジェクトデータ型 (**nvarchar (max)** 、 **varchar (max**)、 **varbinary (max)** ) を、[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]でサポートされるデータ型に変換します。|  
|**0x40000000**|権限をレプリケートします。|  
|**0x80000000 です**|パブリケーションに含まれていないオブジェクトへの依存関係の削除を試みます。|  
|**0x100000000**|このオプションを使用すると、 **varbinary (max)** 列に FILESTREAM 属性が指定されている場合に、その属性をレプリケートできます。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のサブスクライバーにテーブルをレプリケートする場合は、このオプションを指定しないでください。 FILESTREAM 列を持つテーブルを [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] サブスクライバーにレプリケートすることは、このスキーマオプションを設定する方法に関係なく、サポートされていません。 関連オプション**0x800000000**を参照してください。|  
|**0x200000000**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] で導入された日付と時刻のデータ型 (**date**、 **time**、 **datetimeoffset**、および**datetime2**) を、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の以前のバージョンでサポートされているデータ型に変換します。|  
|**0x400000000**|データとインデックスの圧縮オプションをレプリケートします。 詳細については、「 [Data Compression](../../relational-databases/data-compression/data-compression.md)」を参照してください。|  
|**0x800000000**|このオプションを設定すると、サブスクライバーの独自のファイル グループに FILESTREAM データを格納できます。 このオプションが設定されていない場合、FILESTREAM データは既定のファイルグループに格納されます。 レプリケーションでは、ファイルグループは作成されません。したがって、このオプションを設定する場合は、サブスクライバーでスナップショットを適用する前にファイルグループを作成する必要があります。 スナップショットを適用する前にオブジェクトを作成する方法の詳細については、「[スナップショットが適用される前および後のスクリプトの実行](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)」を参照してください。<br /><br /> 関連オプション**0x100000000**を参照してください。|  
|**0x1000000000**|共通言語ランタイム (CLR) ユーザー定義型 (Udt) を**varbinary (max)** に変換します。これにより、udt 型の列を [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]を実行しているサブスクライバーにレプリケートできるようになります。|  
|**0x2000000000**|**Hierarchyid**データ型を**varbinary (max)** に変換して、 **hierarchyid**型の列を [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]を実行しているサブスクライバーにレプリケートできるようにします。 レプリケートされたテーブルでの**hierarchyid**列の使用方法の詳細については、「 [hierarchyid &#40;transact-sql&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)」を参照してください。|  
|**0x4000000000**|テーブルのフィルター選択されたインデックスをレプリケートします。 フィルター選択されたインデックスの詳細については、「[フィルター選択](../../relational-databases/indexes/create-filtered-indexes.md)されたインデックスの作成」をご覧ください。|  
|**0x8000000000**|**Geography**および**geometry**データ型を**varbinary (max)** に変換して、これらの型の列を [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]を実行しているサブスクライバーにレプリケートできるようにします。|  
|**0x10000000000**|**Geography**型および**geometry**型の列のインデックスをレプリケートします。|  
  
 この値が NULL の場合、システムはアーティクルに対して有効なスキーマオプションを自動生成します。 「解説」の**既定のスキーマオプション**の表は、アーティクルの種類に基づいて選択される値を示しています。 また、すべての*schema_option*値がすべての種類のレプリケーションとアーティクルの種類に対して有効であるとは限りません。 「解説」に記載されている**有効なスキーマオプション**テーブルは、特定のアーティクルの種類に対して指定できるオプションを示しています。  
  
> [!NOTE]  
>  *Schema_option*パラメーターは、初期スナップショットのレプリケーションオプションにのみ影響します。 初期スキーマがスナップショットエージェントによって生成され、サブスクライバーで適用されると、サブスクライバーへのパブリケーションスキーマ変更のレプリケーションは、スキーマ変更レプリケーションルールと[sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)で指定された*replicate_ddl*パラメーター設定に基づいて行われます。 詳細については、「[パブリケーション データベースでのスキーマの変更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)」を参照してください。  
  
`[ @subset_filterclause = ] 'subset_filterclause'` は、テーブルアーティクルの行フィルター選択を指定する where 句です。 WHERE 句は含まれません。 *subset_filterclause*の型は**nvarchar (1000)** で、既定値は空の文字列です。  
  
> [!IMPORTANT]  
>  パラメーター化された行フィルター句では列名に関数を適用しないことをお勧めします。これは、 `LEFT([MyColumn]) = SUSER_SNAME()`のように指定すると、パフォーマンスに問題が生じるためです。 フィルター句で[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)を使用し、HOST_NAME の値をオーバーライドする場合は、 [convert](../../t-sql/functions/cast-and-convert-transact-sql.md)を使用してデータ型を変換する必要がある場合があります。 この場合のベストプラクティスの詳細については、「パラメーター化された[行フィルター](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」の「HOST_NAME () 値のオーバーライド」を参照してください。  
  
`[ @article_resolver = ] 'article_resolver'` は、テーブルアーティクルまたはテーブルアーティクルでカスタムビジネスロジックを実行するために呼び出された .NET Framework アセンブリの競合を解決するために使用される COM ベースの競合回避モジュールです。 *article_resolver*は**varchar (255)** ,、既定値は NULL です。 このパラメーターで利用できる値の一覧については、「[!INCLUDE[msCoName](../../includes/msconame-md.md)] カスタム競合回避モジュール」を参照してください。 指定した値が [!INCLUDE[msCoName](../../includes/msconame-md.md)] 競合回避モジュールの値でない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、システムに付属の競合回避モジュールの代わりに指定した競合回避モジュールが使用されます。 **Sp_enumcustomresolvers**を使用して、使用可能なカスタム競合回避モジュールの一覧を列挙します。 詳細については、「[マージ同期中のビジネスロジックの実行](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)」と「[マージレプリケーションの競合の検出と解決](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)」を参照してください。  
  
`[ @resolver_info = ] 'resolver_info'` は、カスタム競合回避モジュールに必要な追加情報を指定するために使用されます。 一部の [!INCLUDE[msCoName](../../includes/msconame-md.md)] 競合回避モジュールには、入力として指定された列が必要です。 *resolver_info*は**nvarchar (255)** ,、既定値は NULL です。 詳細については、「 [Microsoft COM ベースの競合回避モジュール](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)」を参照してください。  
  
`[ @source_owner = ] 'source_owner'` は、 *source_object*の所有者の名前です。 *source_owner*は**sysname**,、既定値は NULL です。 NULL の場合、現在のユーザーは所有者であると見なされます。  
  
`[ @destination_owner = ] 'destination_owner'` は、' dbo ' ではなく、サブスクリプションデータベース内のオブジェクトの所有者です。 *destination_owner*は**sysname**,、既定値は NULL です。 NULL の場合、' dbo ' は所有者と見なされます。  
  
`[ @vertical_partition = ] 'column_filter'` テーブルアーティクルの列フィルター処理を有効または無効にします。 *vertical_partition*は**nvarchar (5)** で、既定値は FALSE です。  
  
 **false**は、列方向のフィルター処理が行われず、すべての列がパブリッシュされることを示します。  
  
 **true**は、宣言された主キーと ROWGUID 列を除くすべての列をクリアします。 列は**sp_mergearticlecolumn**を使用して追加されます。  
  
`[ @auto_identity_range = ] 'automatic_identity_range'` は、パブリケーションの作成時に、このテーブルアーティクルの id 範囲の自動処理を有効または無効にします。 *auto_identity_range*は**nvarchar (5)** ,、既定値は FALSE です。 **true**を指定すると、自動 id 範囲の処理が有効になり、 **false**の場合は無効になります。  
  
> [!NOTE]  
>  *auto_identity_range*は非推奨とされており、旧バージョンとの互換性のためだけに用意されています。 Id 範囲管理オプションを指定するには、 *identityrangemanagementoption*を使用する必要があります。 詳細については、「[ID 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)」を参照してください。  
  
`[ @pub_identity_range = ] pub_identity_range` は、自動 id 範囲管理が使用されている場合に、サーバーサブスクリプションを使用してサブスクライバーに割り当てられる id 範囲のサイズを制御します。 この ID 範囲は、再パブリッシュ元のサブスクライバーが自らのサブスクライバーに割り当てるために予約されています。 *pub_identity_range*は**bigint**,、既定値は NULL です。 *Identityrangemanagementoption*が**auto**の場合、または*auto_identity_range*が**true**の場合は、このパラメーターを指定する必要があります。  
  
`[ @identity_range = ] identity_range` は、自動 id 範囲管理を使用する場合に、パブリッシャーとサブスクライバーの両方に割り当てられる id 範囲のサイズを制御します。 *identity_range*は**bigint**,、既定値は NULL です。 *Identityrangemanagementoption*が**auto**の場合、または*auto_identity_range*が**true**の場合は、このパラメーターを指定する必要があります。  
  
> [!NOTE]  
>  *identity_range*は、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用してサブスクライバーを再パブリッシュするときに、id 範囲のサイズを制御します。  
  
マージエージェントによって新しい id 範囲が割り当てられるタイミングを制御する `[ @threshold = ] threshold` パーセンテージ値。 [*しきい*値] で指定した値のパーセンテージが使用されると、マージエージェントによって新しい id 範囲が作成されます。 *しきい値*は**int**,、既定値は NULL です。 *Identityrangemanagementoption*が**auto**の場合、または*auto_identity_range*が**true**の場合は、このパラメーターを指定する必要があります。  
  
`[ @verify_resolver_signature = ] verify_resolver_signature` は、マージレプリケーションで競合回避モジュールを使用する前に、デジタル署名を検証するかどうかを指定します。 *verify_resolver_signature*は**int**,、既定値は1です。  
  
 **0**は、署名が検証されないことを示します。  
  
 **1**は、署名が信頼できるソースからのものかどうかを確認することを指定します。  
  
`[ @destination_object = ] 'destination_object'` は、サブスクリプションデータベース内のオブジェクトの名前です。 *destination_object*のデータ型は**sysname**で、既定値は **\@source_object**に含まれています。 このパラメーターは、アーティクルがストアドプロシージャ、ビュー、Udf などのスキーマのみのアーティクルである場合にのみ指定できます。 指定したアーティクルがテーブルアーティクルの場合、 *@source_object* の値は*destination_object*の値よりも優先されます。  
  
`[ @allow_interactive_resolver = ] 'allow_interactive_resolver'` は、アーティクルに対してインタラクティブ競合回避モジュールの使用を有効または無効にします。 *allow_interactive_resolver*は**nvarchar (5)** ,、既定値は FALSE です。 **true**にすると、アーティクルでインタラクティブ競合回避モジュールを使用できるようになります。**false**を無効にします。  
  
> [!NOTE]  
>  インタラクティブ競合回避モジュールは [!INCLUDE[ssEW](../../includes/ssew-md.md)] のサブスクライバーではサポートされていません。  
  
`[ @fast_multicol_updateproc = ] 'fast_multicol_updateproc'` このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。  
  
`[ @check_permissions = ] check_permissions` は、マージエージェントがパブリッシャーに変更を適用するときに検証されるテーブルレベルの権限のビットマップです。 マージ処理が使用するパブリッシャーのログインまたはユーザー アカウントが正しいテーブル権限を持っていない場合、無効な変更は競合としてログに記録されます。 *check_permissions*は**int**で、| を指定できます。 [(ビットごとの OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md)次の1つ以上の値の積。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**0x00** (既定値)|権限は確認されません。|  
|**0x10**|サブスクライバーで実行される挿入操作をアップロードする前に、パブリッシャー側で権限をチェックします。|  
|**0x20**|サブスクライバーで実行された更新操作をアップロードする前に、パブリッシャー側で権限をチェックします。|  
|**0x40**|サブスクライバーで実行された削除操作をアップロードする前に、パブリッシャー側で権限をチェックします。|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` は、このストアドプロシージャによって実行される操作によって既存のスナップショットが無効になる可能性があることを確認します。 *force_invalidate_snapshot*は**ビット**,、既定値は0です。  
  
 **0**に設定すると、アーティクルを追加してもスナップショットが無効になることはありません。 変更に新しいスナップショットが必要であることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1**に設定すると、アーティクルの追加によってスナップショットが無効になることがあります。また、新しいスナップショットを必要とする既存のサブスクリプションがある場合は、既存のスナップショットに古いスナップショットをマークし、新しいスナップショットを生成することができます。 既存のスナップショットを持つパブリケーションにアーティクルを追加する場合は、 *force_invalidate_snapshot*が**1**に設定されます。  
  
`[ @published_in_tran_pub = ] 'published_in_tran_pub'` は、マージパブリケーションのアーティクルがトランザクションパブリケーションでもパブリッシュされることを示します。 *published_in_tran_pub*は**nvarchar (5)** ,、既定値は FALSE です。 **true**を指定すると、アーティクルはトランザクションパブリケーションでもパブリッシュされます。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` は、このストアドプロシージャによって実行されるアクションによって既存のサブスクリプションの再初期化が必要になる可能性があることを確認します。 *force_reinit_subscription*は**ビット**,、既定値は0です。  
  
 **0**に設定すると、アーティクルを追加してもサブスクリプションは再初期化されません。 変更によって既存のサブスクリプションが再初期化される必要があることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1**を指定すると、マージアーティクルへの変更によって既存のサブスクリプションが再初期化され、サブスクリプションの再初期化を行う権限が与えられます。 *subset_filterclause*がパラメーター化された行フィルターを指定する場合、 *force_reinit_subscription*は**1**に設定されます。  
  
`[ @logical_record_level_conflict_detection = ] 'logical_record_level_conflict_detection'` は、論理レコードのメンバーであるアーティクルの競合検出レベルを指定します。 *logical_record_level_conflict_detection*は**nvarchar (5)** ,、既定値は FALSE です。  
  
 **true**を指定すると、論理レコードの任意の場所に変更が加えられた場合に競合が検出されます。  
  
 **false**を指定すると、既定の競合検出が*column_tracking*によって指定されたとおりに使用されます。 詳細については、「[Group Changes to Related Rows with Logical Records](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)」(論理レコードによる関連行への変更のグループ化) をご覧ください。  
  
> [!NOTE]  
>  論理レコードは [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバーではサポートされていないため、これらのサブスクライバーをサポートするには、 *logical_record_level_conflict_detection*に**false**の値を指定する必要があります。  
  
`[ @logical_record_level_conflict_resolution = ] 'logical_record_level_conflict_resolution'` は、論理レコードのメンバーであるアーティクルの競合解決レベルを指定します。 *logical_record_level_conflict_resolution*は**nvarchar (5)** ,、既定値は FALSE です。  
  
 **true**を指定すると、優先される論理レコード全体が、失われた論理レコードを上書きします。  
  
 **false**は、優先される行が論理レコードに制約されないことを指定します。 *Logical_record_level_conflict_detection*が**true**の場合、 *logical_record_level_conflict_resolution*も**true**に設定する必要があります。 詳細については、「[Group Changes to Related Rows with Logical Records](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)」(論理レコードによる関連行への変更のグループ化) をご覧ください。  
  
> [!NOTE]  
>  論理レコードは [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバーではサポートされていないため、これらのサブスクライバーをサポートするには、 *logical_record_level_conflict_resolution*に**false**の値を指定する必要があります。  
  
`[ @partition_options = ] partition_options` は、アーティクル内のデータをパーティション分割する方法を定義します。これにより、すべての行が1つのパーティションまたは1つのサブスクリプションのみに属している場合に、パフォーマンスを最適化できます。 *partition_options*は**tinyint**で、次のいずれかの値を指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**0** (既定値)|アーティクルのフィルター選択は、静的であるか、パーティションごとに一意のデータのサブセットを生成しません。つまり、"重複する" パーティションになります。|  
|**1**|パーティションは重複しており、サブスクライバーで行われたデータ操作言語 (DML) の更新では、行が属するパーティションを変更することはできません。|  
|**2**|アーティクルのフィルター選択によって重複しないパーティションが生成されますが、複数のサブスクライバーが同じパーティションを受け取ることができます。|  
|**3**|アーティクルのフィルター選択により、各サブスクリプションに一意の重複しないパーティションが生成されます。|  
  
> [!NOTE]  
>  アーティクルのソーステーブルが別のパブリケーションで既にパブリッシュされている場合、 *partition_options*の値は両方のアーティクルで同じである必要があります。  
  
`[ @processing_order = ] processing_order` は、マージパブリケーション内のアーティクルの処理順序を示します。 *processing_order*は**int**,、既定値は0です。 **0**は、アーティクルが順序付けられていないことを示します。その他の値は、このアーティクルの処理順序の序数値を表します。 アーティクルは、最も小さい値から最も大きい値の順序で処理されます。 2つのアーティクルの値が同じである場合、処理順序は、 [sysmergearticles](../../relational-databases/system-tables/sysmergearticles-transact-sql.md)システムテーブルのアーティクルのニックネームの順序によって決まります。 詳細については、「[Specify Merge Replication properties](../../relational-databases/replication/merge/specify-merge-replication-properties.md)」 (マージ レプリケーションのプロパティの指定) を参照してください。  
  
`[ @subscriber_upload_options = ] subscriber_upload_options` は、クライアントサブスクリプションを使用して、サブスクライバーで行われた更新に対する制限を定義します。 詳細については、「[ダウンロード専用アーティクルを使用したマージ レプリケーションのパフォーマンス最適化](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)」を参照してください。 *subscriber_upload_options*は**tinyint**で、次のいずれかの値を指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**0** (既定値)|制限はありません。 サブスクライバー側で行われた変更は、パブリッシャーにアップロードされます。|  
|**1**|サブスクライバーでの変更は許可されますが、パブリッシャーにはアップロードされません。|  
|**2**|サブスクライバーでの変更は許可されていません。|  
  
 *Subscriber_upload_options*を変更するには、 [sp_reinitmergepullsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md)を呼び出してサブスクリプションを再初期化する必要があります。  
  
> [!NOTE]  
>  アーティクルのソーステーブルが別のパブリケーションで既にパブリッシュされている場合、 *subscriber_upload_options*の値は両方のアーティクルで同じである必要があります。  
  
アーティクルに対して id 範囲管理をどのように処理するかを指定 `[ @identityrangemanagementoption = ] identityrangemanagementoption` です。 *identityrangemanagementoption*は**nvarchar (10)** ,、値は次のいずれかを指定することができます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**存在**|Id 範囲の管理を無効にします。|  
|**手動**|NOT FOR REPLICATION を使用して id 列をマークし、手動による id 範囲処理を有効にします。|  
|**自動**|Id 範囲の自動管理を指定します。|  
|NULL (既定値)|*Auto_identity_range*の値が**true**でない場合、既定値は**none**です。|  
  
 旧バージョンとの互換性のために、 *identityrangemanagementoption*の値が NULL の場合、 *auto_identity_range*の値がチェックされます。 ただし、 *identityrangemanagementoption*の値が NULL でない場合、 *auto_identity_range*の値は無視されます。 詳細については、「[ID 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)」を参照してください。  
  
`[ @delete_tracking = ] 'delete_tracking'` は、削除をレプリケートするかどうかを示します。 *delete_tracking*は**nvarchar (5)** ,、既定値は TRUE です。 **false**は、削除がレプリケートされないことを示し、 **true**は、マージレプリケーションの通常の動作である削除がレプリケートされることを示します。 *Delete_tracking*が**false**に設定されている場合、サブスクライバー側で削除された行はパブリッシャー側で手動で削除する必要があり、パブリッシャー側で削除された行はサブスクライバー側で手動で削除する必要があります。  
  
> [!IMPORTANT]  
>  *Delete_tracking*を**false**に設定すると、非収束になります。 アーティクルのソーステーブルが別のパブリケーションで既にパブリッシュされている場合、 *delete_tracking*の値は両方のアーティクルで同じである必要があります。  
  
> [!NOTE]  
>  *delete_tracking*のオプションは、パブリケーションの**新規作成ウィザード**または **[パブリケーションのプロパティ]** ダイアログボックスを使用して設定することはできません。  
  
`[ @compensate_for_errors = ] 'compensate_for_errors'` は、同期中にエラーが発生した場合に補正アクションを実行するかどうかを示します。 *compensate_for_errors i*s **nvarchar (5)** ,、既定値は FALSE です。 **True**に設定されている場合、同期中にサブスクライバーまたはパブリッシャーで適用できない変更は、常に、変更を元に戻す補正アクションにつながります。ただし、誤って構成された1つのサブスクライバーがエラーを生成すると、他のサブスクライバーやパブリッシャーでの変更が元に戻される可能性があります。 **false**を設定すると、これらの補正アクションは無効になりますが、エラーは補正と同様にログに記録され、それ以降のマージでは、成功するまで変更を適用しようとし続けます。  
  
> [!IMPORTANT]  
>  影響を受ける行のデータは収束されないように見えますが、エラーを解決すると、変更は直ちに適用可能となり、データは収束されます。 アーティクルのソーステーブルが別のパブリケーションで既にパブリッシュされている場合、 *compensate_for_errors*の値は両方のアーティクルで同じである必要があります。  
  
`[ @stream_blob_columns = ] 'stream_blob_columns'` バイナリラージオブジェクトの列をレプリケートするときに、データストリームの最適化を使用することを指定します。 *stream_blob_columns*は**nvarchar (5)** ,、既定値は FALSE です。 **true**は、最適化が試行されることを意味します。 FILESTREAM が有効になっている場合、 *stream_blob_columns*は true に設定されます。 これにより、FILESTREAM データのレプリケーションを最適な方法で実行し、メモリ使用量を減らすことができます。 FILESTREAM テーブルアーティクルで blob ストリーミングを使用しないように強制するには、 **sp_changemergearticle**を使用して*stream_blob_columns*を false に設定します。  
  
> [!IMPORTANT]  
>  このメモリ最適化を有効にすると、同期中にマージエージェントのパフォーマンスが低下する可能性があります。 このオプションは、mb 単位のデータを含む列をレプリケートする場合にのみ使用してください。  
  
> [!NOTE]  
>  論理レコードなど特定のマージレプリケーション機能では、 *stream_blob_columns*が**true**に設定されていても、バイナリラージオブジェクトをレプリケートするときにストリームの最適化が使用されない場合があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>Remarks  
 **sp_addmergearticle**は、マージレプリケーションで使用します。  
  
 オブジェクトをパブリッシュすると、その定義がサブスクライバーにコピーされます。 1つ以上の他のオブジェクトに依存するデータベースオブジェクトをパブリッシュする場合は、参照されているすべてのオブジェクトをパブリッシュする必要があります。 たとえば、テーブルに依存しているビューをパブリッシュする場合は、そのテーブルもパブリッシュする必要があります。  
  
 *Partition_options*に**3**を指定した場合、そのアーティクル内のデータの各パーティションに対して1つのサブスクリプションのみを使用できます。 第 2 のサブスクリプションを作成し、その新しいサブスクリプションのフィルター選択条件が既存のサブスクリプションと同じパーティションとして判別される場合、既存のサブスクリプションは削除されます。  
  
 *Partition_options*に3を指定すると、マージエージェントが実行され、パーティションスナップショットの有効期限が短くなるたびにメタデータがクリーンアップされます。 このオプションを使用する場合は、サブスクライバーによって要求されたパーティションスナップショットを有効にすることを検討してください。 詳しくは、「 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」をご覧ください。  
  
 *Subset_filterclause*を使用して静的な水平フィルターを持つアーティクルを、パラメーター化されたフィルターを持つアーティクルを含む既存のパブリケーションに追加するには、サブスクリプションを再初期化する必要があります。  
  
 *Processing_order*を指定する場合は、アーティクルの順序の値の間にギャップを残しておくことをお勧めします。これにより、将来の新しい値の設定が簡単になります。 たとえば、Article1、Article2、Article3 の3つの記事がある場合は、1、2、3ではなく、 *processing_order*を10、20、および30に設定します。 詳細については、「[Specify Merge Replication properties](../../relational-databases/replication/merge/specify-merge-replication-properties.md)」 (マージ レプリケーションのプロパティの指定) を参照してください。  
  
## <a name="default-schema-option-table"></a>既定のスキーマオプションテーブル  
 次の表では、アーティクルの種類に依存する*schema_option*に NULL 値が指定されている場合に、ストアドプロシージャによって設定される既定値について説明します。  
  
|アーティクルの種類|スキーマ オプションの値|  
|------------------|-------------------------|  
|**func schema only**|**0x01**|  
|**インデックス付きビュースキーマのみ**|**0x01**|  
|**proc schema only**|**0x01**|  
|**テーブル**|**0X0c034fd1** - [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降の互換性のあるパブリケーションとネイティブモードのスナップショット。<br /><br /> **0X08034ff1** - 、キャラクターモードのスナップショットを使用した [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降の互換性のあるパブリケーション。|  
|**view schema only**|**0x01**|  
  
> [!NOTE]  
>  パブリケーションが以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をサポートしている場合、**テーブル**の既定のスキーマオプションは**0X30034ff1**です。  
  
## <a name="valid-schema-option-table"></a>有効なスキーマオプションテーブル  
 次の表では、アーティクルの種類に応じて*schema_option*許可される値について説明します。  
  
|アーティクルの種類|スキーマオプションの値|  
|------------------|--------------------------|  
|**func schema only**|**0x01**と**0x2000**|  
|**インデックス付きビュースキーマのみ**|**0x01**、 **0x040,** 、 **0x0100**、 **0x2000**、 **0x40000**、 **0x1000000**、および**0x200000**|  
|**proc schema only**|**0x01**と**0x2000**|  
|**テーブル**|すべてのオプション。|  
|**view schema only**|**0x01**、 **0x040,** 、 **0x0100**、 **0x2000**、 **0x40000**、 **0x1000000**、および**0x200000**|  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-addmergearticle-trans_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールまたは **db_owner** 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [アーティクルの定義](../../relational-databases/replication/publish/define-an-article.md)   
 [データとデータベース オブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Id 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [sp_changemergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_dropmergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
