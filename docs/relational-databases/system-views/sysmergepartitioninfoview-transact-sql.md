---
title: sysmergepartitioninfoview (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergepartitioninfoview
- sysmergepartitioninfoview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepartitioninfoview view
ms.assetid: 714e2935-1bc7-4901-aea2-64b1bbda03d6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 40b1ebc5319c13b5aa84a28e1a5c5546dd62bd03
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094824"
---
# <a name="sysmergepartitioninfoview-transact-sql"></a>sysmergepartitioninfoview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Sysmergepartitioninfoview**ビューはテーブル アーティクルのパーティション分割情報を公開します。 このビューは、パブリッシャー側のパブリケーション データベース、およびサブスクライバー側のサブスクリプション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|アーティクルの名前です。|  
|**type**|**tinyint**|アーティクルの種類。次のいずれかになります。<br /><br /> **0x0a**テーブルを = です。<br /><br /> **0x20** = プロシージャ スキーマのみです。<br /><br /> **0x40** = ビュー スキーマのみ、またはインデックス付きビュー スキーマのみです。<br /><br /> **0x80** = 関数スキーマのみです。|  
|**objid**|**int**|パブリッシュされたオブジェクトの識別子です。|  
|**sync_objid**|**int**|同期データセットを表すビューのオブジェクト ID。|  
|**view_type**|**tinyint**|ビューの種類。<br /><br /> **0** = ビュー以外はすべてのベース オブジェクトを使用しています。<br /><br /> **1** = パーマネント ビュー。<br /><br /> **2** = 一時ビュー。|  
|**artid**|**uniqueidentifier**|指定したアーティクルの一意な ID 番号です。|  
|**description**|**nvarchar (255)**|アーティクルの簡単な説明。|  
|**pre_creation_command**|**tinyint**|サブスクリプション データベースにアーティクルが作成されるときに実行される既定の操作。<br /><br /> **0** = なし - サブスクライバーでテーブルが既に存在する場合のアクションは実行されません。<br /><br /> **1** = drop - テーブルを再作成する前に削除します。<br /><br /> **2** = 削除 - サブセット フィルターの WHERE 句に基づいて削除します。<br /><br /> **3** = 切り捨て - 同じが、行ではなくページを削除します。 ただし、WHERE 句は使用しません。|  
|**pubid**|**uniqueidentifier**|現在のアーティクルが属するパブリケーションの ID。|  
|**nickname**|**int**|アーティクル識別用のニックネーム マップ。|  
|**column_tracking**|**int**|アーティクルの列の追跡が実装されているかどうかを示します。|  
|**status**|**tinyint**|アーティクルの状態。次のいずれかになります。<br /><br /> **1** = Unsynced - テーブルをパブリッシュする初期処理スクリプトは、次回、スナップショット エージェントの実行を実行します。<br /><br /> **2** = active - テーブルをパブリッシュする初期処理スクリプトが実行されています。|  
|**conflict_table**|**sysname**|現在のアーティクルに関する競合レコードが含まれているローカル テーブルの名前。 このテーブルは情報用のみとして提供されており、その内容は、カスタム競合回避ルーチンを使用して変更や削除ができます。または、管理者が直接変更したり、削除することもできます。|  
|**creation_script**|**nvarchar (255)**|アーティクルの作成スクリプト。|  
|**conflict_script**|**nvarchar (255)**|アーティクルの競合スクリプト。|  
|**article_resolver**|**nvarchar (255)**|このアーティクルの競合回避モジュールです。|  
|**ins_conflict_proc**|**sysname**|競合テーブルへの競合情報の書き込みに使用するプロシージャです。|  
|**insert_proc**|**sysname**|同期時に行の挿入に使用するプロシージャです。|  
|**update_proc**|**sysname**|同期時に行の更新に使用するプロシージャです。|  
|**select_proc**|**sysname**|マージ エージェントがロックやアーティクルの列と行の検索に使用する、自動生成ストアド プロシージャの名前です。|  
|**metadata_select_proc**|**sysname**|マージ レプリケーション システム テーブル内のメタデータへのアクセスに使用する、自動生成ストアド プロシージャの名前です。|  
|**delete_proc**|**sysname**|同期時に行の削除に使用するプロシージャです。|  
|**schema_option**|**binary(8)**|指定されたアーティクルに対するスキーマ生成オプションのビットマップです。 サポートされるは*schema_option*値を参照してください[sp_addmergearticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)します。|  
|**destination_object**|**sysname**|サブスクライバーで作成されるテーブルの名前。|  
|**destination_owner**|**sysname**|目的のオブジェクトの所有者名。|  
|**resolver_clsid**|**nvarchar (50)**|カスタム競合回避モジュールの ID。 ビジネス ロジック ハンドラーの場合、この値は NULL です。|  
|**subset_filterclause**|**nvarchar(1000)**|アーティクルのフィルター句。|  
|**missing_col_count**|**int**|アーティクルにない、パブリッシュされた列の数です。|  
|**missing_cols**|**varbinary (128)**|アーティクルにない列を示すビットマップです。|  
|**excluded_cols**|**varbinary (128)**|アーティクルから除外された列のビットマップです。|  
|**excluded_col_count**|**int**|アーティクルから除外された列の数です。|  
|**columns**|**varbinary (128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deleted_cols**|**varbinary (128)**|アーティクルから削除された列を示すビットマップです。|  
|**resolver_info**|**nvarchar (255)**|カスタム競合回避モジュールによって必要な追加情報の記憶域。|  
|**view_sel_proc**|**nvarchar(290)**|マージ エージェントが、動的にフィルター選択されたパブリケーションでアーティクルを最初に作成するとき、およびフィルター選択された任意のパブリケーションで変更された行を列挙するときに使用するストアド プロシージャの名前です。|  
|**gen_cur**|**bigint**|アーティクルのベース テーブルに対するローカルの変更の generates 値です。|  
|**vertical_partition**|**int**|列のフィルター選択がテーブル アーティクルで有効かどうかを示します。 **0**垂直方向のフィルター処理がないことを示します、すべての列をパブリッシュします。|  
|**identity_support**|**int**|ID 範囲の自動処理が有効かどうかを示します。 **1** id 範囲処理が有効になっていることを意味し、 **0**サポートの範囲は id がないことを意味します。|  
|**before_image_objid**|**int**|追跡テーブルのオブジェクト ID。 追跡テーブルには、パブリケーションに対するパーティションの変更の最適化が有効な場合、特定のキー列の値が含まれます。|  
|**before_view_objid**|**int**|ビュー テーブルのオブジェクト ID。 ビューが存在するテーブルでは、行の削除または更新前に、その行が特定のサブスクライバーに属していたかどうかが追跡されます。 パブリケーションに対するパーティションの変更の最適化が有効な場合にのみ適用されます。|  
|**verify_resolver_signature**|**int**|マージ レプリケーションで競合回避モジュールを使用する前に、デジタル署名を確認するかどうかを示します。<br /><br /> **0** = 署名がないことを確認します。<br /><br /> **1** = 署名が信頼できる発行元があるかどうかを確認することを確認します。|  
|**allow_interactive_resolver**|**bit**|アーティクルに対する対話型の競合回避モジュールの使用が有効かどうかを示します。 **1**はアーティクルに対するインタラクティブ競合回避モジュールを使用できることを意味します。|  
|**fast_multicol_updateproc**|**bit**|1 つの UPDATE ステートメントで同じ行の複数の列に対して変更を適用するように、マージ エージェントが有効になっているかどうかを示します。<br /><br /> **0**列ごとに個別の更新の変更の問題を = です。<br /><br /> **1** 1 つのステートメントで複数の列を更新する UPDATE ステートメントの発行を = です。|  
|**check_permissions**|**int**|テーブル レベルの権限のビットマップは、マージ エージェントがパブリッシャーに変更を適用するときにことを確認します。 *check_permissions*これらの値のいずれかの。<br /><br /> **0x00** = 権限は確認されません。<br /><br /> **0x10** = チェックの挿入がサブスクライバー側で行われる前に、パブリッシャー側で権限をアップロードすることができます。<br /><br /> **0x20**サブスクライバーで行われた更新プログラムをアップロードする前に、パブリッシャー側で権限をチェックしますを = です。<br /><br /> **0x40** = では、サブスクライバー側で Delete をアップロードする前に、パブリッシャー側で権限をチェックします。|  
|**maxversion_at_cleanup**|**int**|マージ エージェントの次回実行時にクリーンアップされる generation の最大値です。|  
|**processing_order**|**int**|マージ パブリケーション内のアーティクルの処理順序を示します値が**0**アーティクルが順序付けられたがないことと、最低から最高値の順序でアーティクルが処理を示します。 2 つのアーティクルの値が同じ場合、それらは同時に処理されます。 詳細については、「[Specify Merge Replication properties](../../relational-databases/replication/merge/specify-merge-replication-properties.md)」 (マージ レプリケーションのプロパティの指定) を参照してください。|  
|**upload_options**|**tinyint**|変更がサブスクライバーで許可されるか、サブスクライバーからアップロードされるかを示します。次の値のいずれかになります。<br /><br /> **0** = サブスクライバー側で行われる更新に制限はありません。 すべての変更がパブリッシャーにアップロードされます。<br /><br /> **1** = 変更が、サブスクライバーで許可されますが、パブリッシャーにはアップロードされません。<br /><br /> **2** = 変更はサブスクライバーで許可されません。|  
|**published_in_tran_pub**|**bit**|マージ パブリケーション内のアーティクルが、トランザクション パブリケーションでもパブリッシュされるかどうかを示します。<br /><br /> **0** = アーティクルはトランザクション アーティクルでパブリッシュされません。<br /><br /> **1** = アーティクルはトランザクション アーティクルでもパブリッシュされます。|  
|**lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**procname_postfix**|**nchar(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**well_partitioned_lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**before_upd_view_objid**|**int**|更新前のテーブルのビューの ID です。|  
|**delete_tracking**|**bit**|削除がレプリケートされるかどうかを示します。<br /><br /> **0** = 削除はレプリケートされません。<br /><br /> **1** = マージ レプリケーションの既定の動作は、削除がレプリケートされます。<br /><br /> ときに、値の*delete_tracking*は**0**、パブリッシャー、サブスクライバーで削除された行を手動で削除する必要があり、パブリッシャー側で削除された行はサブスクライバー側で手動で削除する必要があります。<br /><br /> 注:値**0**未集約になります。|  
|**compensate_for_errors**|**bit**|同期中にエラーが検出されたときに補正アクションが行われるかどうかを示します。<br /><br /> **0** = 補正アクションが無効になります。<br /><br /> **1**に補正アクションは、マージ レプリケーションの既定の動作は、これらの変更を元に戻す、サブスクライバーまたはパブリッシャーが常に適用できない変更を = です。<br /><br /> 注:値**0**未集約になります。|  
|**pub_range**|**bigint**|パブリッシャーの ID 範囲の大きさ。|  
|**range**|**bigint**|調整の際にサブスクライバーに割り当てられる、連続する ID 値の大きさ。|  
|**threshold**|**int**|ID 範囲のしきい値のパーセンテージ。|  
|**stream_blob_columns**|**bit**|バイナリ ラージ オブジェクトの列にストリームの最適化を使用するかどうかを示します。 **1**最適化が試行されたことを意味します。|  
|**preserve_rowguidcol**|**bit**|レプリケーションが既存の rowguid 列を使用するかどうかを示します。 値**1**既存の ROWGUIDCOL 列が使用されることを意味します。 **0**レプリケーション ROWGUIDCOL 列を追加することを意味します。|  
|**partition_view_id**|**int**|サブスクライバー パーティションを定義するビューを指定します。|  
|**repl_view_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**partition_deleted_view_rule**|**sysname**|マージ レプリケーション トリガー内で、列の古い値に基づいて削除または更新された各行のパーティション ID を取得するために使用されるステートメントです。|  
|**partition_inserted_view_rule**|**sysname**|マージ レプリケーション トリガー内で、列の新しい値に基づいて挿入または更新された各行のパーティション ID を取得するために使用されるステートメントです。|  
|**membership_eval_proc_name**|**sysname**|内の行の現在のパーティション Id を評価するプロシージャの名前[MSmerge_contents &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)します。|  
|**column_list**|**sysname**|アーティクル内でパブリッシュされた列のコンマ区切りの一覧です。|  
|**column_list_blob**|**sysname**|バイナリ ラージ オブジェクトの列を含む、アーティクル内でパブリッシュされた列のコンマ区切りの一覧です。|  
|**expand_proc**|**sysname**|新たに挿入された親行のすべての子行、パーティションを変更された親行、および削除された親行のパーティション ID を再評価するプロシージャの名前です。|  
|**logical_record_parent_nickname**|**int**|論理レコード内の、指定されたアーティクルのトップレベルにある親のニックネームです。|  
|**logical_record_view**|**int**|それぞれの子の rowguid に対応する、トップレベルにある親アーティクルの rowguid を出力するビューです。|  
|**logical_record_deleted_view_rule**|**sysname**|ような**logical_record_view**で"deleted"テーブル内の子行の update および delete トリガーが表示される点を除き、します。|  
|**logical_record_level_conflict_detection**|**bit**|競合を、論理レコード レベルと、行または列レベルのどちらで検出するかを示します。<br /><br /> **0** = 行レベルまたは列レベルの競合検出を使用します。<br /><br /> **1** = 論理レコードの競合検出を使用すると、パブリッシャーでの行の変更と、別の変更の同じ論理行レコードはサブスクライバー側では、競合として処理します。<br /><br /> この値が 1 の場合には、論理レコード レベルでの競合解決だけを使用できます。|  
|**logical_record_level_conflict_resolution**|**bit**|競合はで、行レベルまたは列レベル、または論理レコード レベルで解決するかどうかを示します。<br /><br /> **0** = 行レベルまたは列レベルの解決が使用されます。<br /><br /> **1** = 場合に、競合を優先されなかった論理レコード全体に優先されなかった論理レコード全体が上書きされます。<br /><br /> 値 1 は、論理レコード レベルでの検出でも、行または列レベルの検出でも使用することができます。|  
|**partition_options**|**tinyint**|アーティクル内のデータをパーティション分割する方法を定義します。パーティション分割することにより、すべての行が 1 つのパーティションまたは 1 つのサブスクリプションに属している場合に、パフォーマンスを最適化できます。 *Partition_options*値は次のいずれかを指定できます。<br /><br /> **0** =「重複する」のパーティションが静的か、または各パーティションのデータの一意なサブセットが、生成されません、アーティクルのフィルターします。<br /><br /> **1** = パーティションが重複していると、サブスクライバーで実行された DML 更新は、行が属するパーティションを変更できません。<br /><br /> **2**記事、重複しないパーティションが得られますが、複数のサブスクライバーが同じパーティションを受け取ることができます = フィルター選択します。<br /><br /> **3** =、フィルタ リング、情報の記事には、サブスクリプションごとに固有の重複しないパーティションが得られます。|  
|**name**|**sysname**|パーティションの名前。|  
  
## <a name="see-also"></a>参照  
 [パラメーター化されたフィルターによるマージ パブリケーションのパーティションの管理](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [sp_helpmergepartition &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md)  
  
  
