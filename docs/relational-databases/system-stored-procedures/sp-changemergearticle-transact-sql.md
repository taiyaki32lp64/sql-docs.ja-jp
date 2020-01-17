---
title: sp_changemergearticle (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/09/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergearticle_TSQL
- sp_changemergearticle
helpviewer_keywords:
- sp_changemergearticle
ms.assetid: 0dc3da5c-4af6-45be-b5f0-074da182def2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 35d1ef721df6f67e4cd5c0f993458238394ac0e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104512"
---
# <a name="spchangemergearticle-transact-sql"></a>sp_changemergearticle (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  マージ アーティクルのプロパティを変更します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changemergearticle [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` アーティクルが存在するパブリケーションの名前です。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @article = ] 'article'` 変更するアーティクルの名前です。 *記事*は**sysname**、既定値はありません。  
  
`[ @property = ] 'property'` 指定されたアーティクルとパブリケーションを変更するプロパティです。 *プロパティ*は**nvarchar (30)** 、指定できると、値の 1 つの表にします。  
  
`[ @value = ] 'value'` 指定したプロパティの新しい値です。 *値*は**nvarchar (1000)** 、指定できると、値の 1 つの表にします。  
  
 このテーブルには、記事、これらのプロパティの値のプロパティについて説明します。  
  
|プロパティ|値|説明|  
|--------------|------------|-----------------|  
|**allow_interactive_resolver**|**true**|アーティクルに対してインタラクティブ競合回避モジュールの使用を有効にします。|  
||**false**|アーティクルに対して、インタラクティブ競合回避モジュールの使用を無効にします。|  
|**article_resolver**||アーティクルのカスタム競合回避モジュール。 テーブル アーティクルにのみ適用されます。|  
|**check_permissions** (ビットマップ)|**0x00**|テーブルレベルの権限は確認されません。|  
||**0x10**|サブスクライバーで実行された INSERT ステートメントをパブリッシャーで適用する前に、テーブルレベルの権限がパブリッシャーで確認されます。|  
||**0x20**|テーブル レベルのアクセス許可は、サブスクライバーで実行された UPDATE ステートメントがパブリッシャーで適用される前に、パブリッシャー側でチェックされます。|  
||**0x40**|サブスクライバーの DELETE ステートメントがパブリッシャーで適用される前に、パブリッシャー側でテーブル レベルのアクセス許可がチェックされます。|  
|**column_tracking**|**true**|列レベルの追跡をオンにします。 テーブル アーティクルにのみ適用されます。<br /><br /> 注:パブリッシュが複数の 246 列を含むテーブルと列レベルの追跡を使用できません。|  
||**false**|列レベルの追跡をオフにして、行レベルで競合検出のままです。 テーブル アーティクルにのみ適用されます。|  
|**compensate_for_errors**|**true**|同期中にエラーが発生したときに、補正操作が実行されます。 詳細については、次を参照してください。 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)します。|  
||**false**|補正アクションは行われません、これは既定の動作。 詳細については、次を参照してください。 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)します。<br /><br /> **\*\* 重要な\* \*** エラーに対処するとすぐに収束に、影響を受けた行のデータが表示されますが変更を適用して、データが収束します。 アーティクルのソース テーブルが別のパブリケーションの値で既にパブリッシュされている場合*compensate_for_errors*の両方のアーティクルで同じである必要があります。|  
|**creation_script**||パスとサブスクリプション データベースでアーティクルを作成するために使用、オプションのアーティクル スキーマ スクリプトの名前。|  
|**delete_tracking**|**true**|DELETE ステートメントがレプリケートされます。これは既定の動作です。|  
||**false**|削除ステートメントはレプリケートされません。<br /><br /> **\*\* 重要な\* \*** 設定**delete_tracking**に**false**収束、および削除された行の結果を手動で削除する必要があります。|  
|**description**||アーティクルの説明エントリします。|  
|**destination_owner**||ない場合、サブスクリプション データベース内のオブジェクトの所有者の名前**dbo**します。|  
|**identity_range**||**bigint**場合、アーティクルは、新しい id 値を割り当てるときに使用する範囲のサイズを指定する**identityrangemanagementoption**設定**自動**または**auto_identity_範囲**設定**true**します。 テーブル アーティクルのみに適用されます。 詳細については、の「マージ レプリケーション」セクションを参照してください。 [Id 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)します。|  
|**identityrangemanagementoption**|**手動**|自動での ID 範囲の管理を無効にします。 NOT FOR REPLICATION を使用して、手動による id 範囲処理を有効にする id 列をマークします。 詳細については、「[Replicate Identity Columns](../../relational-databases/replication/publish/replicate-identity-columns.md)」 (ID 列のレプリケート) を参照してください。|  
||**none**|すべての ID 範囲の管理を無効にします。|  
|**logical_record_level_conflict_detection**|**true**|任意の場所、論理レコードに変更があった場合に、競合が検出されます。 必要があります**logical_record_level_conflict_resolution**に設定する**true**します。|  
||**false**|既定の競合検出を使用して指定した**column_tracking**します。|  
|**logical_record_level_conflict_resolution**|**true**|全体の優先されなかった論理レコードは、優先されなかった論理レコードを上書きします。|  
||**false**|優先される行は論理レコードに制約されません。|  
|**partition_options**|**0**|アーティクルのフィルター処理または静的のいずれか、つまり「重複する」パーティションまたは各パーティションのデータの一意なサブセットは生成されません。|  
||**1**|パーティションは重複しています。サブスクライバーで実行された DML 更新では、行が属するパーティションを変更できません。|  
||**2**|重複しないパーティションでは、アーティクルのフィルター処理が生成されますが、複数のサブスクライバーが同じパーティションを受け取ることができます。|  
||**3**|アーティクルのフィルター処理には、サブスクリプションごとに固有の重複しないパーティションが生成されます。<br /><br /> 注:値を指定する場合**3**の**partition_options**を単一のサブスクリプションのみパーティションごとにそのアーティクル内のデータがあります。 第 2 のサブスクリプションを作成し、その新しいサブスクリプションのフィルター選択条件が既存のサブスクリプションと同じパーティションとして判別される場合、既存のサブスクリプションは削除されます。|  
|**pre_creation_command**|**none**|サブスクライバーでテーブルが既に存在する場合、アクションは行われません。|  
||**delete**|サブセット フィルターの WHERE 句に基づいて削除を発行します。|  
||**drop**|テーブルを再作成する前に削除します。|  
||**truncate**|変換先テーブルを切り捨てます。|  
|**processing_order**||**int**マージ パブリケーションでアーティクルの処理順序を示します。|  
|**identity_range**||**bigint**場合、アーティクルは、サーバー サブスクリプションを使用してサブスクライバーに割り当てる範囲のサイズを指定する**identityrangemanagementoption**設定**自動**または**ツールidentity_range**設定**true**します。 この ID 範囲は、再パブリッシュ元のサブスクライバーが自らのサブスクライバーに割り当てるために予約されています。 テーブル アーティクルのみに適用されます。 詳細については、の「マージ レプリケーション」セクションを参照してください。 [Id 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)します。|  
|**published_in_tran_pub**|**true**|アーティクルはトランザクション パブリケーションでもパブリッシュされます。|  
||**false**|アーティクルはトランザクション パブリケーションではパブリッシュされません。|  
|**resolver_info**||カスタム競合回避モジュールが必要な追加情報の指定に使用されます。 いくつかの[!INCLUDE[msCoName](../../includes/msconame-md.md)]競合回避モジュールが、競合回避モジュールへの入力として提供されている列が必要です。 **resolver_info**は**nvarchar (255)** 、既定値は NULL です。 詳細については、「 [Microsoft COM ベースの競合回避モジュール](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)」を参照してください。|  
|**schema_option** (ビットマップ)||詳細については、このトピックで後述する「解説」を参照してください。|  
||**0x00**|スナップショット エージェントによるスクリプト作成を無効にし、提供するスクリプトを使用して**creation_script**します。|  
||**0x01**|オブジェクトの作成スクリプト (CREATE TABLE、CREATE PROCEDURE など) を生成します。|  
||**0x10**|対応するクラスター化インデックスを生成します。|  
||**0x20**|ユーザー定義データ型をサブスクライバーでのデータ型を基本に変換します。 UDT 列が主キーの一部である場合、または計算列は、UDT 列を参照している場合、ユーザー定義型 (UDT) 列のチェックまたは既定の制約がある場合に、このオプションを使用することはできません。|  
||**0x40**|対応する非クラスター化インデックスを生成します。|  
||**0x80**|宣言された参照整合性を主キーに含めます。|  
||**0x100**|定義されている場合、テーブル アーティクル上のユーザー トリガーをレプリケートします。|  
||**0x200**|FOREIGN KEY 制約をレプリケートします。 参照先のテーブルがパブリケーションの一部は、パブリッシュされたテーブルですべての FOREIGN KEY 制約はレプリケートされません。|  
||**0x400**|CHECK 制約をレプリケートします。|  
||**0x800**|既定値をレプリケートします。|  
||**0x1000**|列レベルの照合順序をレプリケートします。|  
||**0x2000**|パブリッシュされたアーティクルのソース オブジェクトに関連付けられた拡張プロパティをレプリケートします。|  
||**0x4000**|テーブル アーティクルで定義されている場合は、一意なキーをレプリケートします。|  
||**0x8000**|制約をスクリプト化する場合は、ALTER TABLE ステートメントを生成します。|  
||**0x10000**|制約が同期中に適用されないように、CHECK 制約を NOT FOR REPLICATION としてレプリケートします。|  
||**0x20000**|制約が同期中に適用されないように、FOREIGN KEY 制約を NOT FOR REPLICATION としてレプリケートします。|  
||**0x40000**|パーティション テーブルまたはインデックスに関連付けられているファイル グループをレプリケートします。|  
||**これに対して、0x80000**|パーティション テーブルのパーティション構成をレプリケートします。|  
||**0x100000**|パーティション インデックスのパーティション構成をレプリケートします。|  
||**0x200000**|テーブルな統計をレプリケートします。|  
||**0x400000**|既定のバインドをレプリケートします。|  
||**0x800000**|ルールのバインドをレプリケートします|  
||**0x1000000**|フルテキスト インデックスをレプリケートします。|  
||**0x2000000**|バインドされた XML スキーマ コレクション**xml**列はレプリケートされません。|  
||**0x4000000**|インデックスをレプリケート**xml**列。|  
||**0x8000000**|サブスクライバーにまだ存在しないスキーマを作成します。|  
||**0x10000000**|変換します**xml**列**ntext**サブスクライバーにします。|  
||**0x20000000**|変換の大きなオブジェクトのデータ型 (**nvarchar (max)** 、 **varchar (max)** 、および**varbinary (max)** ) で導入された[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]はサポートされているデータ型に[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]します。|  
||**0x40000000**|アクセス許可をレプリケートします。|  
||**0x80000000**|パブリケーションの一部ではない任意のオブジェクトに対する依存関係を削除しようとしてください。|  
||**0x100000000**|このオプションを使用して、指定されている場合は、FILESTREAM 属性をレプリケートする**varbinary (max)** 列。 テーブルをレプリケートする場合は、このオプションを指定しない[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]サブスクライバー。 FILESTREAM 列を持つテーブルをレプリケート[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]サブスクライバーがサポートされていません、このスキーマ オプションを設定する方法に関係なく、します。 関連するオプションを参照してください。 **0x800000000**します。|  
||**0x200000000**|日付と時刻のデータ型に変換 (**日付**、**時間**、 **datetimeoffset**、および**datetime2**) で導かれ[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]以前のバージョンでサポートされているデータ型に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。|  
||**0x400000000**|データとインデックスの圧縮オプションをレプリケートします。 詳細については、「 [Data Compression](../../relational-databases/data-compression/data-compression.md)」を参照してください。|  
||**0x800000000**|このオプションを設定すると、サブスクライバーの独自のファイル グループに FILESTREAM データを格納できます。 このオプションが設定されていない場合は、FILESTREAM データが既定のファイル グループに格納されます。 レプリケーションが; ファイル グループを作成できません。したがって、このオプションを設定する場合、サブスクライバーでスナップショットを適用する前に、ファイル グループを作成する必要があります。 スナップショットを適用する前に、オブジェクトを作成する方法の詳細については、次を参照してください。[前にスクリプトを実行し、後のスナップショットが適用される](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)します。<br /><br /> 関連するオプションを参照してください。 **0x100000000**します。|  
||**0x1000000000**|共通言語ランタイム (CLR) ユーザー定義型 (Udt) に変換します**varbinary (max)** を実行しているサブスクライバーに UDT 型の列をレプリケートできるように[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]します。|  
||**0x2000000000**|変換、 **hierarchyid**のデータ型**varbinary (max)** ように型の列**hierarchyid**実行しているサブスクライバーにレプリケートできる[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 使用する方法の詳細についての**hierarchyid**レプリケートされたテーブル内の列を参照してください[hierarchyid &#40;TRANSACT-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)します。|  
||**0x4000000000**|テーブルにフィルター選択されたインデックスをレプリケートします。 フィルター選択されたインデックスの詳細については、次を参照してください。 [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)します。|  
||**0x8000000000**|変換、 **geography**と**geometry**データ型を**varbinary (max)** を実行しているサブスクライバーにこれらの型の列をレプリケートできるように[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x10000000000**|型の列にインデックスをレプリケート**geography**と**geometry**します。|  
||NULL|システムの自動生成されたアーティクルに対する有効なスキーマ オプション。|  
|**status**|**アクティブ**|テーブルをパブリッシュする初期処理スクリプトを実行します。|  
||**unsynced**|テーブルをパブリッシュする初期処理スクリプトは、次回、スナップショット エージェントを実行を実行します。|  
|**stream_blob_columns**|**true**|バイナリ ラージ オブジェクトの列をレプリケートするときに、データ ストリームの最適化が使用されます。 ただし、論理レコードなど、特定のマージ レプリケーション機能は使用されている、ストリームの最適化も防ぐことができます。 *stream_blob_columns* FILESTREAM が有効な場合は true に設定されます。 これにより、最適に実行し、メモリ使用率を低減する FILESTREAM データのレプリケーションができます。 Blob ストリームを使用しないように FILESTREAM のテーブル アーティクルを強制的には、次のように設定します。 *stream_blob_columns*を false にします。<br /><br /> **\*\* 重要な\* \*** 同期中に、マージ エージェントのパフォーマンスが低下する可能性がありますこのメモリ最適化を有効にします。 このオプションは、メガバイト単位のデータを含む列をレプリケートする場合にのみ使用する必要があります。|  
||**false**|バイナリ ラージ オブジェクト列をレプリケートするときに、最適化は使用されません。|  
|**subscriber_upload_options**|**0**|更新プログラムがクライアント サブスクリプションです。 使用したサブスクライバー側での制限なし変更はパブリッシャーにアップロードされます。 このプロパティの変更が必要既存のサブスクライバーを再初期化します。|  
||**1**|変更がクライアント サブスクリプションを使用したサブスクライバーで許可されますが、パブリッシャーにはアップロードされません。|  
||**2**|クライアント サブスクリプションを使用したサブスクライバー側では、変更することはできません。|  
|**subset_filterclause**||水平方向のフィルター処理を指定する WHERE 句です。 テーブル アーティクルにのみ適用されます。<br /><br /> **\*\* 重要な\* \*** パフォーマンス上の理由をお勧めする関数を適用しないパラメーター化された行フィルター句内の列名など`LEFT([MyColumn]) = SUSER_SNAME()`します。 使用する場合[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)フィルター句と HOST_NAME 値を使用してデータ型を変換する必要があります[変換](../../t-sql/functions/cast-and-convert-transact-sql.md)します。 この場合のベスト プラクティスの詳細については、の「HOST_NAME() 値のオーバーライド」セクションを参照してください[Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)します。|  
|**threshold**||実行しているサブスクライバーに使用されるパーセンテージ値[!INCLUDE[ssEW](../../includes/ssew-md.md)]または以前のバージョンの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 **しきい値**マージ エージェントが新しい id 範囲を割り当てるときを制御します。 しきい値で指定された値の割合を使用すると、マージ エージェントは新しい id 範囲を作成します。 ときに使用される**identityrangemanagementoption**に設定されている**自動**または**auto_identity_range**に設定されている**true**します。 テーブル アーティクルのみに適用されます。 詳細については、の「マージ レプリケーション」セクションを参照してください。 [Id 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)します。|  
|**verify_resolver_signature**|**1**|カスタム競合回避モジュールのデジタル署名が信頼できる発行元がかどうかを判断することを確認します。|  
||**0**|カスタム競合回避モジュールのデジタル署名について、信頼されるソースからの署名であるかを判断するための検証を行いません。|  
|NULL (既定値)||サポートされている値の一覧を返します*プロパティ*します。|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` このストアド プロシージャが実行する操作が既存のスナップショットが無効になることを確認します。 *更によって*は、**ビット**、既定値は**0**します。  
  
 **0**スナップショットが無効であることをマージ アーティクルへの変更が発生しないことを指定します。 ストアド プロシージャは、変更は、新しいスナップショットを必要になることを検出する場合は、エラーが発生し、変更は行われません。  
  
 **1**手段に、マージ アーティクルへの変更には、スナップショットを無効になる可能性がありますを新しいスナップショットを必要とする既存のサブスクリプションがある場合は、不使用とマークするのには、既存のスナップショットを新しいスナップショットを生成のアクセス許可を付与します。  
  
 プロパティは、「解説」を参照してください、変更された場合、新しいスナップショットの生成が必要です。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` このストアド プロシージャが実行されるアクションでは、既存のサブスクリプションの再初期化される場合がありますかを確認します。 *更によって*は、**ビット**、既定値は**0**します。  
  
 **0**マージ アーティクルへの変更では、サブスクリプションを再初期化するのには発生しないことを指定します。 ストアド プロシージャは、変更が既存のサブスクリプションを再初期化する必要になることを検出する場合は、エラーが発生し、変更は行われません。  
  
 **1**マージ アーティクルへの変更が発生する既存のサブスクリプションを再初期化するサブスクリプションの再初期化を許可します。  
  
 変更によって既存のサブスクリプションの再初期化が必要になるプロパティについては、「解説」を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_changemergearticle**はマージ レプリケーションで使用します。  
  
 **Sp_changemergearticle**を使用して最初に指定されたアーティクルのプロパティを変更するために使用[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)を参照してください[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)これらのプロパティの詳細についてはします。  
  
 次のプロパティを変更するには、新しいスナップショットを生成することが必要ですし、値を指定する必要があります**1**の*更によって*パラメーター。  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **schema_options**  
  
-   **subset_filterclause**  
  
 次のプロパティを変更する場合は、既存する必要があります、サブスクリプションを再初期化の値を指定する必要があります**1**の*更によって*パラメーター。  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **identityrangemanagementoption**  
  
-   **subscriber_upload_options**  
  
-   **subset_filterclause**  
  
-   **creation_script**  
  
-   **schema_option**  
  
-   **logical_record_level_conflict_detection**  
  
-   **logical_record_level_conflict_resolution**  
  
 3 の値を指定するときに**partition_options**メタデータのクリーンアップ、マージ エージェントを実行し、パーティション スナップショット有効期限が短くされるたびにします。 このオプションを使用する場合は、要求されたパーティション スナップショットをサブスクライバーの有効化を検討してください。 詳しくは、「 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」をご覧ください。  
  
 設定するときに、 **column_tracking**プロパティ、テーブルが他のマージ パブリケーションで既にパブリッシュされている場合、列を追跡する必要がありますこのテーブルに基づく既存のアーティクルで使用されている値と同じです。 このパラメーターは、テーブル アーティクルのみに固有のものです。  
  
 複数のパブリケーションでは、同じ基になるテーブルに基づくアーティクルをパブリッシュ、変更、 **delete_tracking**プロパティまたは**compensate_for_errors**プロパティを 1 つのアーティクルと同じ変更を同じテーブルに基づくその他のアーティクルをに対してください。  
  
 マージ処理が使用するパブリッシャーのログインまたはユーザー アカウントが正しいテーブル権限を持っていない場合、無効な変更は競合としてログに記録されます。  
  
 値を変更するときに**schema_option**システムでは、ビットごとの更新は実行されません。 つまり、設定すると、 **schema_option**を使用して**sp_changemergearticle**既存ビット設定がオフにすることがあります。 実行する必要があります、既存の設定を保持する[& (ビット演算子 AND)](../../t-sql/language-elements/bitwise-and-transact-sql.md)値は、設定して、現在の値の間で*schema_option*を実行することによって、によって判断できます[sp_helpmergearticle](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)します。  
  
> [!CAUTION]  
>  して多く (おそらく何百も) を実行して、パブリケーション内のアーティクルの**sp_changemergearticle**記事の 1 つは、完了までに長い時間をかかる場合があります。  
  
## <a name="valid-schema-option-table"></a>有効なスキーマ オプションの一覧  
 次の表に、許可されている説明*schema_option*アーティクルの種類によっての値。  
  
|アーティクルの種類|スキーマ オプションの値|  
|------------------|--------------------------|  
|**func スキーマのみ**|**0x01**と**0x2000**|  
|**インデックス付きビュー スキーマのみ**|**0x01**、 **0x040**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x1000000**、および**0x200000**|  
|**proc スキーマのみ**|**0x01**と**0x2000**|  
|**table**|すべてのオプション。|  
|**ビュー スキーマのみ**|**0x01**、 **0x040**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x1000000**、および**0x200000**|  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_changemergearticle](../../relational-databases/replication/codesnippet/tsql/sp-changemergearticle-tr_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_changemergearticle**します。  
  
## <a name="see-also"></a>参照  
 [表示およびアーティクルのプロパティの変更](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [パブリケーションとアーティクルのプロパティの変更](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergearticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_dropmergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
