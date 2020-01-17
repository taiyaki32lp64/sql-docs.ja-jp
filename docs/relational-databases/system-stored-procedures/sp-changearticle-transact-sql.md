---
title: sp_changearticle (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changearticle
- sp_changearticle_TSQL
helpviewer_keywords:
- sp_changearticle
ms.assetid: 24c33ca5-f03a-4417-a267-131ca5ba6bb5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8fe752b17af683f59078bd7c37eb702a9408a530
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771400"
---
# <a name="spchangearticle-transact-sql"></a>sp_changearticle (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  トランザクションパブリケーションまたはスナップショットパブリケーションのアーティクルのプロパティを変更します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changearticle [ [@publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`アーティクルを含むパブリケーションの名前を指定します。 *publication*は**sysname**,、既定値は NULL です。  
  
`[ @article = ] 'article'`プロパティを変更するアーティクルの名前を指定します。 *アーティクル*は**sysname**で、既定値は NULL です。  
  
`[ @property = ] 'property'`変更するアーティクルのプロパティを設定します。 *プロパティ*は**nvarchar (100)** です。  
  
`[ @value = ] 'value'`アーティクルプロパティの新しい値を指定します。 *値*は**nvarchar (255)** です。  
  
 次の表では、アーティクルのプロパティとそれらのプロパティの値について説明します。  
  
|プロパティ|値|説明|  
|--------------|------------|-----------------|  
|**creation_script**||ターゲットテーブルを作成するために使用されるアーティクルスキーマスクリプトのパスと名前です。 既定値は NULL です。|  
|**del_cmd**||実行する DELETE ステートメントです。指定しないと、ログから作成されます。|  
|**description**||記事の新しい説明エントリ。|  
|**dest_object**||これは旧バージョンとの互換性のために用意されています。 **Dest_table**を使用します。|  
|**dest_table**||新しい変換先テーブル。|  
|**destination_owner**||対象オブジェクトの所有者の名前。|  
|**フィルター (filter)**||テーブルをフィルターによって選択 (行方向のフィルター選択) するために使用される新しいストアド プロシージャです。 既定値は NULL です。 ピアツーピアレプリケーションのパブリケーションの場合、を変更することはできません。|  
|**fire_triggers_on_snapshot**|**true**|レプリケートされたユーザートリガーは、初期スナップショットが適用されるときに実行されます。<br /><br /> 注:トリガーをレプリケートするには、ビットマスク値*schema_option*に値**0x100**を含める必要があります。|  
||**false**|初期スナップショットが適用されたときに、レプリケートされたユーザー トリガーが実行されません。|  
|**identity_range**||サブスクライバーで割り当てられた、割り当て済みの ID 範囲のサイズを管理します。 ピア ツー ピア レプリケーションではサポートされません。|  
|**ins_cmd**||実行する INSERT ステートメントです。それ以外の場合は、ログから作成されます。|  
|**pre_creation_cmd**||同期が適用される前に、レプリケーション先のテーブルを削除したり、切り捨てたりできる作成準備コマンドです。|  
||**none**|コマンドを使用しません。|  
||**drop**|変換先テーブルを削除します。|  
||**delete**|変換先テーブルを削除します。|  
||**truncate**|変換先テーブルを切り捨てます。|  
|**pub_identity_range**||サブスクライバーで割り当てられた、割り当て済みの ID 範囲のサイズを管理します。 ピア ツー ピア レプリケーションではサポートされません。|  
|**schema_option**||指定されたアーティクルのスキーマ生成オプションのビットマップを指定します。 *schema_option*は**binary (8)** です。 詳細については、このトピックで後述する「解説」を参照してください。|  
||**0x00**|スナップショット エージェントによるスクリプト作成を無効にします。|  
||**0x01**|オブジェクトの作成 (CREATE TABLE、CREATE PROCEDURE など) を生成します。|  
||**除く**|定義されている場合、アーティクルの変更を反映するストアド プロシージャを生成します。|  
||**0x04**|Id 列は、IDENTITY プロパティを使用してスクリプト化されます。|  
||**0x08**|**タイムスタンプ**列をレプリケートします。 設定しない場合、**タイムスタンプ**列は**バイナリ**としてレプリケートされます。|  
||**0x10**|対応するクラスター化インデックスを生成します。|  
||**0x20**|ユーザー定義データ型 (UDT) をサブスクライバー側の基本データ型に変換します。 Udt 列に CHECK 制約または DEFAULT 制約がある場合、UDT 列が主キーの一部である場合、または計算列が UDT 列を参照している場合は、このオプションを使用できません。 Oracle パブリッシャーではサポートされていません。|  
||**0x40**|対応する非クラスター化インデックスを生成します。|  
||**0x80**|宣言された参照整合性を主キーに含めます。|  
||**0x100**|定義されている場合、テーブル アーティクル上のユーザー トリガーをレプリケートします。|  
||**0x200**|FOREIGN KEY 制約をレプリケートします。 参照先のテーブルがパブリケーションの一部でない場合、パブリッシュされたテーブルのすべての FOREIGN KEY 制約はレプリケートされません。|  
||**0x400**|CHECK 制約をレプリケートします。|  
||**0x800**|既定値をレプリケートします。|  
||**0x1000**|列レベルの照合順序をレプリケートします。|  
||**0x2000**|パブリッシュされたアーティクルのソースオブジェクトに関連付けられた拡張プロパティをレプリケートします。|  
||**0x4000**|テーブルアーティクルで定義されている場合は、一意キーをレプリケートします。|  
||**0x8000**|ALTER TABLE ステートメントを使用して、テーブルアーティクルの主キーと一意キーを制約としてレプリケートします。<br /><br /> 注:このオプションは非推奨とされます。 代わりに、 **0x80**と**0x4000**を使用してください。|  
||**0x10000**|CHECK 制約を NOT FOR REPLICATION としてレプリケートし、同期中に制約が適用されないようにします。|  
||**0x20000**|では、制約が同期中に適用されないように、外部キー制約は NOT FOR REPLICATION としてレプリケートされます。|  
||**0x40000**|パーティション テーブルまたはインデックスに関連付けられているファイル グループをレプリケートします。|  
||**0x80000**|パーティション テーブルのパーティション構成をレプリケートします。|  
||**0x100000**|パーティションインデックスのパーティション構成をレプリケートします。|  
||**0x200000**|テーブルの統計をレプリケートします。|  
||**0x400000**|既定のバインドです。|  
||**0x800000**|ルールのバインドです。|  
||**0x1000000**|フルテキスト インデックスです。|  
||**0x2000000**|**Xml**列にバインドされている xml スキーマコレクションはレプリケートされません。|  
||**0x4000000**|**Xml**列のインデックスをレプリケートします。|  
||**0x8000000**|サブスクライバーにまだ存在しないスキーマを作成します。|  
||**0x10000000**|サブスクライバーで**xml**列を**ntext**に変換します。|  
||**0x20000000**|で[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]導入されたラージオブジェクトデータ型 (**nvarchar (max)** 、 **varchar (max**)、 **varbinary (max)** ) を、で[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]サポートされているデータ型に変換します。|  
||**0x40000000**|権限をレプリケートします。|  
||**0x80000000 です**|パブリケーションに含まれていないオブジェクトへの依存関係を削除しようとしています。|  
||**0x100000000**|このオプションを使用すると、 **varbinary (max)** 列に FILESTREAM 属性が指定されている場合に、その属性をレプリケートできます。 テーブルをサブスクライバーに[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]レプリケートする場合は、このオプションを指定しないでください。 このスキーマオプションを設定する方法[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]に関係なく、FILESTREAM 列を持つテーブルをサブスクライバーにレプリケートすることはサポートされていません。<br /><br /> 関連オプション**0x800000000**を参照してください。|  
||**0x200000000**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で導入[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]された日付と時刻のデータ型 (date、 **time**、datetimeoffset、および datetime2) を、以前のバージョンのでサポートされているデータ型に変換します。|  
||**0x400000000**|データとインデックスの圧縮オプションをレプリケートします。 詳細については、「 [Data Compression](../../relational-databases/data-compression/data-compression.md)」を参照してください。|  
||**0x800000000**|このオプションを設定すると、サブスクライバーの独自のファイル グループに FILESTREAM データを格納できます。 このオプションが設定されていない場合、FILESTREAM データは既定のファイルグループに格納されます。 レプリケーションでは、ファイルグループは作成されません。したがって、このオプションを設定する場合は、サブスクライバーでスナップショットを適用する前にファイルグループを作成する必要があります。 スナップショットを適用する前にオブジェクトを作成する方法の詳細については、「[スナップショットが適用される前および後のスクリプトの実行](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)」を参照してください。<br /><br /> 関連オプション**0x100000000**を参照してください。|  
||**0x1000000000**|共通言語ランタイム (CLR) ユーザー定義型 (Udt) が8000バイトを超える値を**varbinary (max)** に変換します。これにより、udt 型の列を[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、を実行しているサブスクライバーにレプリケートできるようになります。|  
||**0x2000000000**|**Hierarchyid**データ型を**varbinary (max)** に変換します。これにより、 **hierarchyid**型の列を、を[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]実行しているサブスクライバーにレプリケートできるようになります。 レプリケートされたテーブルでの**hierarchyid**列の使用方法の詳細については、「 [hierarchyid &#40;transact-sql&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)」を参照してください。|  
||**0x4000000000**|テーブルのフィルター選択されたインデックスをレプリケートします。 フィルター選択されたインデックスの詳細については、「[フィルター選択](../../relational-databases/indexes/create-filtered-indexes.md)されたインデックスの作成」をご覧ください。|  
||**0x8000000000**|**Geography**および**geometry**データ型を**varbinary (max)** に変換して、これらの型の列を、を実行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]しているサブスクライバーにレプリケートできるようにします。|  
||**0x10000000000**|**Geography**型および**geometry**型の列のインデックスをレプリケートします。|  
||**0x20000000000**|列のスパース属性をレプリケートします。 この属性の詳細については、「[スパース列の使用](../../relational-databases/tables/use-sparse-columns.md)」を参照してください。|  
||**0x40000000000**|サブスクライバーにメモリ最適化テーブルを作成するには、スナップショットエージェントによるスクリプト作成を有効にします。|  
||**0x80000000000**|メモリ最適化アーティクルのクラスター化インデックスを非クラスター化インデックスに変換します。|  
|**status**||プロパティの新しいステータスを指定します。|  
||**dts 行分割**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
||**列名を含める**|列名が、レプリケートされる INSERT ステートメントに含まれます。|  
||**列名がありません**|列名は、レプリケートされる INSERT ステートメントに含まれません。|  
||**dts 行分割がありません**|アーティクルの行方向のパーティション分割は、変換可能なサブスクリプションによって定義されません。|  
||**none**|[Sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)テーブルのすべての状態オプションをクリアし、アーティクルを非アクティブとしてマークします。|  
||**parameters**|パラメーター化コマンドを使用して、変更がサブスクライバーに反映されます。 これは新しいアーティクルに対する既定値です。|  
||**文字列リテラル**|変更は、文字列リテラル値を使用してサブスクライバーに反映されます。|  
|**sync_object**||同期出力ファイルを生成するために使用されるテーブルまたはビューの名前。 既定値は NULL です。 Oracle パブリッシャーではサポートされていません。|  
|**テーブルスペース**||Oracle データベースからパブリッシュされたアーティクルのログ テーブルによって使用されたテーブルスペースを識別します。 詳細については、「[Manage Oracle Tablespaces](../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md)」 (Oracle テーブルスペースの管理) を参照してください。|  
|**threshold**||ディストリビューション エージェントがどの時点で新しい ID 範囲を割り当てるかを制御するパーセンテージの値です。 ピア ツー ピア レプリケーションではサポートされません。|  
|**type**||Oracle パブリッシャーではサポートされていません。|  
||**logbased**|ログベースのアーティクル。|  
||**logbased manualboth**|手動フィルターと手動ビューを使用したログベースのアーティクル。 このオプションでは、 *sync_object*プロパティと*filter*プロパティも設定する必要があります。 Oracle パブリッシャーではサポートされていません。|  
||**logbased manualfilter**|手動フィルターを使用したログベースのアーティクル。 このオプションでは、 *sync_object*プロパティと*filter*プロパティも設定する必要があります。 Oracle パブリッシャーではサポートされていません。|  
||**logbased manualview**|手動ビューを使用する、ログベースのアーティクルです。 このオプションでは、 *sync_object*プロパティも設定する必要があります。 Oracle パブリッシャーではサポートされていません。|  
||**インデックス付き viewlogbased**|ログベースのインデックス付きビューアーティクル。 Oracle パブリッシャーではサポートされていません。 この種類の記事では、ベーステーブルを個別にパブリッシュする必要はありません。|  
||**インデックス付き viewlogbased manualboth**|手動フィルターと手動ビューを使用する、ログベースのインデックス付きビュー アーティクルです。 このオプションでは、 *sync_object*プロパティと*filter*プロパティも設定する必要があります。 この種類の記事では、ベーステーブルを個別にパブリッシュする必要はありません。 Oracle パブリッシャーではサポートされていません。|  
||**インデックス付き viewlogbased manualfilter**|手動フィルターを使用したログベースのインデックス付きビューアーティクル。 このオプションでは、 *sync_object*プロパティと*filter*プロパティも設定する必要があります。 この種類の記事では、ベーステーブルを個別にパブリッシュする必要はありません。 Oracle パブリッシャーではサポートされていません。|  
||**インデックス付き viewlogbased manualview**|手動ビューを使用する、ログベースのインデックス付きビュー アーティクルです。 このオプションでは、 *sync_object*プロパティも設定する必要があります。 この種類の記事では、ベーステーブルを個別にパブリッシュする必要はありません。 Oracle パブリッシャーではサポートされていません。|  
|**upd_cmd**||実行する UPDATE ステートメント。それ以外の場合は、ログから作成されます。|  
|NULL|NULL|変更することができるアーティクルのプロパティの一覧を返します。|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`このストアドプロシージャによって実行される操作によって既存のスナップショットが無効になる可能性があることを確認します。 *force_invalidate_snapshot*は**ビット**,、既定値は**0**です。  
  
 **0**を指定すると、アーティクルへの変更によってスナップショットが無効になることはありません。 変更に新しいスナップショットが必要であることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1**に設定すると、アーティクルへの変更によってスナップショットが無効になることがあります。また、新しいスナップショットを必要とする既存のサブスクリプションが存在する場合は、既存のスナップショットが古い形式としてマークされ、新しいスナップショットが生成されることを示します。  
  
 変更時に新しいスナップショットの生成が必要になるプロパティについては、「解説」を参照してください。  
  
`[ @force_reinit_subscription = ]force_reinit_subscription_`このストアドプロシージャによって実行されるアクションで、既存のサブスクリプションの再初期化が必要になる可能性があることを確認します。 *force_reinit_subscription*は**ビット**で、既定値は**0**です。  
  
 **0**に設定すると、アーティクルへの変更によってサブスクリプションが再初期化されることはありません。 変更によって既存のサブスクリプションが再初期化される必要があることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1**に設定すると、アーティクルへの変更によって既存のサブスクリプションが再初期化され、サブスクリプションの再初期化を行う権限が与えられます。  
  
 変更によって既存のサブスクリプションの再初期化が必要になるプロパティについては、「解説」を参照してください。  
  
`[ @publisher = ] 'publisher'`以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーを指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーでアーティクルの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プロパティを変更する場合は、パブリッシャーを使用しないでください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_changearticle**は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 アーティクルがピアツーピアトランザクションレプリケーションをサポートするパブリケーションに属している場合、 **description**、 **ins_cmd**、 **upd_cmd**、および**del_cmd**の各プロパティだけを変更できます。  
  
 次のいずれかのプロパティを変更するには、新しいスナップショットを生成する必要があります。また、 *force_invalidate_snapshot*パラメーターに値**1**を指定する必要があります。  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **ins_cmd**  
  
-   **pre_creation_cmd**  
  
-   **schema_options**  
  
-   **upd_cmd**  
  
 次のいずれかのプロパティを変更するには、既存のサブスクリプションを再初期化する必要があります。また、 *force_reinit_subscription*パラメーターに値**1**を指定する必要があります。  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **フィルター (filter)**  
  
-   **ins_cmd**  
  
-   **status**  
  
-   **upd_cmd**  
  
 既存のパブリケーション内では、パブリケーション全体を削除して再作成しなくても、 **sp_changearticle**を使用してアーティクルを変更できます。  
  
> [!NOTE]  
>  *Schema_option*の値を変更しても、ビットごとの更新は実行されません。 これは、 **sp_changearticle**を使用して*schema_option*を設定すると、既存のビット設定が無効になる場合があることを意味します。 既存の設定を保持するには、| を実行する必要があります。 [(ビットごとの OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md)設定する値と*schema_option*の現在の値の間で、 [sp_helparticle](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)を実行することによって決定できます。  
  
## <a name="valid-schema-options"></a>有効なスキーマ オプション  
 次の表では、レプリケーションの種類 (上部に表示) とアーティクルの種類 (最初の列に表示されます) に基づく*schema_option*の許容値について説明します。  
  
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
>  キュー更新パブリケーションの場合、 *schema_option*の値**0x80**を有効にする必要があります。 以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリケーションでは、次のような*schema_option*値がサポートされます。**0x01**、 **0x02**、 **0x10**、 **0x40**、 **0x80**、 **0x1000** 、 **0x4000**。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_changetranarticle](../../relational-databases/replication/codesnippet/tsql/sp-changearticle-transac_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changearticle**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [アーティクルのプロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [パブリケーションとアーティクルのプロパティの変更](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addarticle &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)  
  
  
