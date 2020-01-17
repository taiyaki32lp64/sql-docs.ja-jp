---
title: パブリケーションおよびアーティクルのプロパティの変更 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying article properties
- modifying publication properties
- administering replication, properties
- publications [SQL Server replication], changing properties
- articles [SQL Server replication], properties
ms.assetid: f7df51ef-c088-4efc-b247-f91fb2c6ff32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c43c81612ffd851d7ea0e0679f79f3c8fec91037
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882347"
---
# <a name="change-publication-and-article-properties"></a>パブリケーションおよびアーティクルのプロパティの変更
  パブリケーションが作成された後は、ほとんどのパブリケーションおよびアーティクルのプロパティを変更できますが、スナップショットの再生成およびサブスクリプションの再初期化、またはそのいずれかが必要になる場合もあります。 このトピックでは、変更された場合に、これらの操作のいずれかまたは両方を必要とするすべてのプロパティについて説明します。  
  
## <a name="publication-properties-for-snapshot-and-transactional-replication"></a>スナップショット レプリケーションおよびトランザクション レプリケーションのパブリケーションのプロパティ  
  
|[説明]|ストアド プロシージャ|プロパティ|の要件|  
|-----------------|----------------------|----------------|------------------|  
|スナップショットの形式を変更します。|**sp_changepublication**|**sync_method**|新しいスナップショット。|  
|スナップショットの場所を変更します。|**sp_changepublication**|**alt_snapshot_folder**<br /><br /> **snapshot_in_defaultfolder**|新しいスナップショット。|  
|スナップショットの場所を変更します。|**sp_changedistpublisher**|**working_directory**|新しいスナップショット。|  
|スナップショット圧縮を変更します。|**sp_changepublication**|**compress_snapshot**|新しいスナップショット。|  
|任意のファイル転送プロトコル (FTP) スナップショット オプションを変更します。|**sp_changepublication**|**enabled_for_internet**<br /><br /> **ftp_address**<br /><br /> **ftp_login**<br /><br /> **ftp_password**<br /><br /> **ftp_port**<br /><br /> **ftp_subdirectory**|新しいスナップショット。|  
|プリスナップショット スクリプトまたはポストスナップショット スクリプトの場所を変更します。|**sp_changepublication**|**pre_snapshot_script**<br /><br /> **post_snapshot_script**|新しいスナップショット (スクリプトの内容を変更した場合にも必要です)。<br /><br /> 新しいスクリプトをサブスクライバーに適用するには、再初期化が必要です。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーに対するサポートを有効または無効にします。|**sp_changepublication**|**is_enabled_for_het_sub**|新しいスナップショット。|  
|キュー更新サブスクリプションに対する競合レポートを変更します。|**sp_changepublication**|**centralized_conflicts**|アクティブなサブスクリプションがない場合にのみ、変更できます。|  
|キュー更新サブスクリプションに対する競合解決方法を変更します。|**sp_changepublication**|**conflict_policy**|アクティブなサブスクリプションがない場合にのみ、変更できます。|  
  
## <a name="article-properties-for-snapshot-and-transactional-replication"></a>スナップショット レプリケーションおよびトランザクション レプリケーションのアーティクルのプロパティ  
  
|[説明]|ストアド プロシージャ|プロパティ|の要件|  
|-----------------|----------------------|----------------|------------------|  
|アーティクルを削除します。|**sp_droparticle**|すべてのパラメーター。|アーティクルは、サブスクリプションを作成する前に削除できます。 ストアド プロシージャを使用して、アーティクルに対するサブスクリプションを削除できます。 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]を使用して、サブスクリプション全体を削除、再作成、および同期する必要があります。 詳細については、「[既存のパブリケーションでのアーティクルの追加および削除](add-articles-to-and-drop-articles-from-existing-publications.md)」を参照してください。|  
|列フィルターを変更します。|**sp_articlecolumn**|**\@列**<br /><br /> **\@操作**|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|行フィルターを追加します。|**sp_articlefilter**|すべてのパラメーター。|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|行フィルターを削除します。|**sp_articlefilter**|**\@の記事**|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|行フィルターを変更します。|**sp_articlefilter**|**\@filter_clause**|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|行フィルターを変更します。|**sp_changearticle**|**フィルター (filter)**|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|スキーマ オプションを変更します。|**sp_changearticle**|**schema_option**|新しいスナップショット。|  
|スナップショットを適用する前に、サブスクライバーでテーブルをどのように処理するかを変更します。|**sp_changearticle**|**pre_creation_cmd**|新しいスナップショット。|  
|アーティクルの状態を変更します。|**sp_changearticle**|**ステータス**|新しいスナップショット。|  
|INSERT、UPDATE、または DELETE コマンドを変更します。|**sp_changearticle**|**ins_cmd**<br /><br /> **upd_cmd**<br /><br /> **del_cmd**|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|対象となるテーブルの名前を変更します。|**sp_changearticle**|**dest_table**|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|対象となるテーブルの所有者 (スキーマ) を変更します。|**sp_changearticle**|**destination_owner**|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|データ型マッピングを変更します (Oracle パブリッシングにのみ適用されます)。|**sp_changearticlecolumndatatype**|**\@の種類**<br /><br /> **\@の長さ**<br /><br /> **\@の精度**<br /><br /> **\@のスケール**|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
  
## <a name="publication-properties-for-merge-replication"></a>マージ レプリケーションのパブリケーションのプロパティ  
  
|[説明]|ストアド プロシージャ|プロパティ|の要件|  
|-----------------|----------------------|----------------|------------------|  
|スナップショットの形式を変更します。|**sp_changemergepublication**|**sync_mode**|新しいスナップショット。|  
|スナップショットの場所を変更します。|**sp_changemergepublication**|**alt_snapshot_folder**<br /><br /> **snapshot_in_defaultfolder**|新しいスナップショット。|  
|スナップショットの場所を変更します。|**sp_changedistpublisher**|**working_directory**|新しいスナップショット。|  
|スナップショット圧縮を変更します。|**sp_changemergepublication**|**compress_snapshot**|新しいスナップショット。|  
|任意の FTP スナップショット オプションを変更します。|**sp_changemergepublication**|**enabled_for_internet**<br /><br /> **ftp_address**<br /><br /> **ftp_login**<br /><br /> **ftp_password**<br /><br /> **ftp_port**<br /><br /> **ftp_subdirectory**|新しいスナップショット。|  
|プリスナップショット スクリプトまたはポストスナップショット スクリプトを変更します。|**sp_changemergepublication**|**pre_snapshot_script**<br /><br /> **post_snapshot_script**|新しいスナップショット (スクリプトの内容を変更した場合にも必要です)。<br /><br /> 新しいスクリプトをサブスクライバーに適用するには、再初期化が必要です。|  
|結合フィルターまたは論理レコードを追加します。|**sp_addmergefilter**|すべてのパラメーター。|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|結合フィルターまたは論理レコードを削除します。|**sp_dropmergefilter**|すべてのパラメーター。|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|結合フィルターまたは論理レコードを変更します。|**sp_changemergefilter**|**\@プロパティ**<br /><br /> **\@value**|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|パラメーター化されたフィルターの使用を無効にします (パラメーター化されたフィルターを有効にする場合は、特別な操作は不要です)。|**sp_changemergepublication**|**false** の値を **false**に設定。|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|事前計算済みパーティションの使用を有効または無効にします。|**sp_changemergepublication**|**use_partition_groups**|新しいスナップショット。|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] のパーティションの最適化を有効または無効にします。|**sp_changemergepublication**|**keep_partition_changes**|サブスクリプションを再初期化します。|  
|サブスクライバーのパーティションの検証を有効または無効にします。|**sp_changemergepublication**|**validate_subscriber_info**|サブスクリプションを再初期化します。|  
|パブリケーションの互換性レベルを 80sp3 以下に変更します。|**sp_changemergepublication**|**publication_compatibility_level**|新しいスナップショット。|  
  
## <a name="article-properties-for-merge-replication"></a>マージ レプリケーションのアーティクルのプロパティ  
  
|[説明]|ストアド プロシージャ|プロパティ|の要件|  
|-----------------|----------------------|----------------|------------------|  
|アーティクルがパブリケーション内に最新のパラメーター化されたフィルターを持つ場合に、そのアーティクルを削除します。|**sp_dropmergearticle**|すべてのパラメーター。|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|アーティクルが結合フィルターまたは論理レコード内で親である場合に、そのアーティクルを削除します (この操作の副作用として、結合が削除されます)。|**sp_dropmergearticle**|すべてのパラメーター。|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|その他のすべての場合に、アーティクルを削除します。|**sp_dropmergearticle**|すべてのパラメーター。|新しいスナップショット。|  
|それまでにパブリッシュされていなかった列フィルターを含めます。|**sp_mergearticlecolumn**|**\@列**<br /><br /> **\@操作**|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|行フィルターを追加、削除、または変更します。|**sp_changemergearticle**|**subset_filterclause**|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。<br /><br /> パラメーター化フィルターを追加、削除、変更する場合は、再初期化の際、サブスクライバーで保留中の変更をパブリッシャーにアップロードできません。 保留中の変更をアップロードしたい場合は、フィルターを変更する前にすべてのサブスクリプションを同期してください。<br /><br /> アーティクルがどの結合フィルターにも含まれていない場合は、そのアーティクルを削除し、別の行フィルターと共に追加することができます。この場合、サブスクリプション全体を再初期化する必要はありません。 アーティクルの追加と削除の詳細については、「[既存のパブリケーションでのアーティクルの追加および削除](add-articles-to-and-drop-articles-from-existing-publications.md)」を参照してください。|  
|スキーマ オプションを変更します。|**sp_changemergearticle**|**schema_option**|新しいスナップショット。|  
|追跡を列レベルから行レベルに変更します (行レベルの追跡から列レベルの追跡に変更する場合は、特別な操作は不要です)。|**sp_changemergearticle**|**false** の値を **false**に設定。|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|サブスクライバーで作成されたステートメントをパブリッシャーで適用する前に権限を確認するかどうかについて変更を行います。|**sp_changemergearticle**|**check_permissions**|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
|ダウンロード専用サブスクリプションを有効または無効にします (その他のアップロード オプションへの変更、またはその他のアップロード オプションからの変更を行う場合は、特別な操作は不要です)。|**sp_changemergearticle**|**2** の値を **2**に設定、または別の値に変更。|サブスクリプションを再初期化します。|  
|レプリケーション先のテーブルの所有者を変更します。|**sp_changemergearticle**|**destination_owner**|新しいスナップショット。<br /><br /> サブスクリプションを再初期化します。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション管理に関する FAQ](../administration/frequently-asked-questions-for-replication-administrators.md)   
 [スナップショットの作成および適用](../create-and-apply-the-snapshot.md)   
 [サブスクリプションの再初期化](../reinitialize-subscriptions.md)   
 [sp_addmergefilter (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql)   
 [sp_articlecolumn (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql)   
 [sp_articlefilter (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql)   
 [sp_changearticle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)   
 [sp_changearticlecolumndatatype (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql)   
 [sp_changedistpublisher (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql)   
 [sp_changemergearticle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)   
 [sp_changemergefilter (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql)   
 [sp_changemergepublication (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)   
 [sp_changepublication (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)   
 [sp_droparticle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-droparticle-transact-sql)   
 [sp_dropmergearticle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql)   
 [sp_dropmergefilter (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql)   
 [sp_mergearticlecolumn (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql)  
  
  
