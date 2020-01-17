---
title: sp_helpmergearticle (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticle
- sp_helpmergearticle_TSQL
helpviewer_keywords:
- sp_helpmergearticle
ms.assetid: 0fb9986a-3c33-46ef-87bb-297396ea5a6a
author: stevestein
ms.author: sstein
ms.openlocfilehash: e1c297e050121c3013242c40938fdd4c0ba8b936
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122340"
---
# <a name="sphelpmergearticle-transact-sql"></a>sp_helpmergearticle (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  アーティクルに関する情報を返します。 このストアド プロシージャは、パブリッシャー、パブリケーション データベースに対して、またはサブスクリプション データベースに対して再パブリッシュ サブスクライバーで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpmergearticle [ [ @publication = ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` に関する情報を取得するパブリケーションの名前です。 *パブリケーション*は**sysname**、既定値は **%** 、現在のデータベース内のすべてのパブリケーションに含まれるすべてのマージ アーティクルに関する情報が返されます。  
  
`[ @article = ] 'article'` 情報を返すアーティクルの名前です。 *記事*は**sysname**、既定値は **%** 、指定したパブリケーションのすべてのマージ アーティクルに関する情報が返されます。  
  
## <a name="result-set"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|アーティクルの識別子。|  
|**name**|**sysname**|アーティクルの名前。|  
|**source_owner**|**sysname**|ソース オブジェクトの所有者の名前です。|  
|**source_object**|**sysname**|追加するアーティクルのソース オブジェクトの名前。|  
|**sync_object_owner**|**sysname**|パブリッシュされたアーティクルを定義するビューの所有者の名前。|  
|**sync_object**|**sysname**|パーティションの最初のデータを確立するために使用されるカスタム オブジェクトの名前。|  
|**description**|**nvarchar (255)**|この記事の説明です。|  
|**status**|**tinyint**|アーティクルの状態。次のいずれかの値になります。<br /><br /> **1** = 非アクティブ<br /><br /> **2** = アクティブ<br /><br /> **5** = 保留中のデータ定義言語 (DDL) 操作<br /><br /> **6**新しく生成されたスナップショットを使った DDL 操作を =<br /><br /> 注:アーティクルが再初期化される値の**5**と**6**に変更されます**2**します。|  
|**creation_script**|**nvarchar (255)**|パスとサブスクリプション データベースでアーティクルを作成するために使用、オプションのアーティクル スキーマ スクリプトの名前。|  
|**conflict_table**|**nvarchar(270)**|挿入または更新の競合を記録するテーブルの名前。|  
|**article_resolver**|**nvarchar (255)**|アーティクルのカスタム競合回避モジュール。|  
|**subset_filterclause**|**nvarchar(1000)**|水平方向のフィルター処理を指定する WHERE 句です。|  
|**pre_creation_command**|**tinyint**|事前作成メソッドは、次のいずれかを指定できます。<br /><br /> **0** = なし<br /><br /> **1**ドロップを =<br /><br /> **2** = delete<br /><br /> **3** = truncate|  
|**schema_option**|**binary(8)**|アーティクルに対するスキーマ生成オプションのビットマップです。 このビットマップ オプションについては、次を参照してください。 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)または[sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)します。|  
|**type**|**smallint**|アーティクルの種類。次のいずれかの値になります。<br /><br /> **10** = テーブル<br /><br /> **32**ストアド プロシージャを =<br /><br /> **64** = ビューまたはインデックス付きビュー<br /><br /> **128** = ユーザー定義関数<br /><br /> **160** = シノニム スキーマのみ|  
|**column_tracking**|**int**|列レベルの追跡の設定場所**1**列レベルの追跡が、上にあることを意味し、 **0**列レベルの追跡がオフであることを意味します。|  
|**resolver_info**|**nvarchar (255)**|アーティクルの競合回避モジュールの名前。|  
|**vertical_partition**|**bit**|アーティクルが垂直方向にパーティション分割されている場合場所**1** 、情報の記事を垂直方向にパーティション分割することを意味し、 **0**でないことを意味します。|  
|**destination_owner**|**sysname**|対象オブジェクトの所有者です。 ストアド プロシージャ、ビュー、およびユーザー定義関数 (UDF) スキーマ アーティクルをマージするときのみ適用されます。|  
|**identity_support**|**int**|自動 id 範囲処理が有効の場合場所**1**を有効にし、 **0**は無効です。|  
|**identity_range**|**bigint**|新しい id 値を割り当てるときに使用する範囲のサイズ。 詳細については、の「マージ レプリケーション」セクションを参照してください。 [Id 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)します。|  
|**identity_range**|**bigint**|新しい id 値を割り当てるときに使用する範囲のサイズ。 詳細については、の「マージ レプリケーション」セクションを参照してください。 [Id 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)します。|  
|**threshold**|**int**|実行しているサブスクライバーに使用されるパーセンテージ値[!INCLUDE[ssEW](../../includes/ssew-md.md)]または以前のバージョンの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 **しきい値**マージ エージェントが新しい id 範囲を割り当てるときを制御します。 しきい値で指定された値の割合を使用すると、マージ エージェントは新しい id 範囲を作成します。 詳細については、の「マージ レプリケーション」セクションを参照してください。 [Id 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)します。|  
|**verify_resolver_signature**|**int**|マージ レプリケーションで競合回避モジュールを使用する前に、デジタル署名を検証する場合場所**0** 、署名が確認しないことを意味し、 **1**元が信頼できるかどうかを署名を検証することを意味します。|  
|**destination_object**|**sysname**|対象オブジェクトの名前です。 ストアド プロシージャ、ビュー、および UDF スキーマ アーティクルをマージするときのみ適用されます。|  
|**allow_interactive_resolver**|**int**|アーティクルで、インタラクティブ競合回避モジュールを使用する場合場所**1**この競合回避モジュールを使用することを意味し、 **0**使用しないことを意味します。|  
|**fast_multicol_updateproc**|**int**|有効または、1 つの UPDATE ステートメントで同じ行で複数の列に変更を適用するマージ エージェントを無効にします。場所**1** 1 つのステートメントで複数の列が更新されることを意味し、 **0** UPDATE ステートメントを分離する手段が更新される各列の問題。|  
|**check_permissions**|**int**|確認されるテーブル レベル権限のビットマップを表す整数値。 使用可能な値の一覧は、次を参照してください。 [sp_addmergearticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)します。|  
|**processing_order**|**int**|データ変更は、パブリケーションのアーティクルに適用する順序。|  
|**upload_options**|**tinyint**|クライアント サブスクリプションを使用したサブスクライバー側での更新に対する制限を定義します。次のいずれかの値になります。<br /><br /> **0** = クライアント サブスクリプションを使用したサブスクライバーで行われる更新に制限はありません。 すべての変更がパブリッシャーにアップロードされます。<br /><br /> **1** = 変更は、クライアント サブスクリプションを使用したサブスクライバーで許可されますが、パブリッシャーにはアップロードされません。<br /><br /> **2** = クライアント サブスクリプションを使用したサブスクライバーでの変更は許可されません。<br /><br /> 詳細については、「[ダウンロード専用アーティクルを使用したマージ レプリケーションのパフォーマンス最適化](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)」を参照してください。|  
|**identityrangemanagementoption**|**int**|自動 id 範囲処理が有効の場合場所**1**を有効にし、 **0**は無効です。|  
|**delete_tracking**|**bit**|削除がレプリケートされる; 場合場所**1**削除がレプリケートされることを意味し、 **0**いないことを意味します。|  
|**compensate_for_errors**|**bit**|同期中にエラーが発生したときに、補正アクションが行われるかどうかを示します場所**1**補正アクションが実行されることを示しますと**0**補正アクションが考慮されないことを意味します。|  
|**partition_options**|**tinyint**|アーティクル内のデータをパーティション分割する方法を定義します。パーティション分割することにより、すべての行が 1 つのパーティションまたは 1 つのサブスクリプションに属している場合に、パフォーマンスを最適化できます。 *partition_options*値は次のいずれかを指定できます。<br /><br /> **0** = アーティクルのフィルター処理または静的のいずれかの各パーティションのデータの一意のサブセットを作成しません。 これは、"重複する"パーティションがあります。<br /><br /> **1** = パーティションが重複していると、データ操作言語 (DML) の更新がサブスクライバーで行が属しているパーティションを変更することはできません。<br /><br /> **2**記事、重複しないパーティションが得られますが、複数のサブスクライバーが同じパーティションを受け取ることができます = フィルター選択します。<br /><br /> **3** =、フィルタ リング、情報の記事には、サブスクリプションごとに固有の重複しないパーティションが得られます。|  
|**artid**|**uniqueidentifier**|アーティクルを一意に識別する識別子。|  
|**pubid**|**uniqueidentifier**|アーティクルがパブリッシュされるパブリケーションを一意に識別する識別子。|  
|**stream_blob_columns**|**bit**|バイナリ ラージ オブジェクト列をレプリケートするときに、データ ストリームの最適化が使用されているかどうかです。 **1**最適化が使用されていることを意味し、 **0**最適化が使用されていないことを意味します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helpmergearticle**はマージ レプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **db_owner** 、パブリケーション データベースの固定データベース ロール、 **replmonitor** を実行できるは、ディストリビューションデータベースまたはパブリケーションのパブリケーションアクセスリストでのロール**sp_helpmergearticle**します。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_helpmergearticle](../../relational-databases/replication/codesnippet/tsql/sp-helpmergearticle-tran_1.sql)]  
  
## <a name="see-also"></a>参照  
 [表示およびアーティクルのプロパティの変更](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [sp_addmergearticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_dropmergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
