---
title: スナップショットのプロパティの構成 (レプリケーション SP)
description: レプリケーション ストアド プロシージャを使用して、スナップショット パブリケーションまたはトランザクション パブリケーションのスナップショットのプロパティを構成します。
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server replication], properties
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 0152abb24a1bb94f02ebc3f5a4bc6a7c1092acfa
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321269"
---
# <a name="configure-snapshot-properties-replication-transact-sql-programming"></a>スナップショットのプロパティの構成 (レプリケーション Transact-SQL プログラミング)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  スナップショットのプロパティは、レプリケーションのストアド プロシージャを使用し、プログラムから定義および変更できます。使用するストアド プロシージャは、パブリケーションの種類によって異なります。  
  
### <a name="to-configure-snapshot-properties-when-creating-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションを作成するときにスナップショットのプロパティを構成するには  
  
1.  パブリッシャーで [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)を実行します。 `@publication` にパブリケーション名を、`@repl_freq` に **snapshot** と **continuous** のいずれかの値を指定し、次のスナップショット関連のパラメーターを少なくとも 1 つ指定します。  
  
    -   `@alt_snapshot_folder` - このパブリケーションのスナップショットが、既定のスナップショット フォルダー以外の場所、または既定のスナップショット フォルダーに追加された場所からアクセスされる場合のパスを指定します。    
    -   `@compress_snapshot` - 代替スナップショット フォルダー内のスナップショット ファイルを [!INCLUDE[msCoName](../../../includes/msconame-md.md)] CAB ファイル形式で圧縮する場合は、値に **true** を指定します。    
    -   `@pre_snapshot_script` - 初期化時、初期スナップショットが適用される前にサブスクライバーで実行される **.sql** ファイルのファイル名と完全パスを指定します。    
    -   `@post_snapshot_script` - 初期化時、初期スナップショットが適用される後にサブスクライバーで実行される **.sql** ファイルのファイル名と完全パスを指定します。    
    -   `@snapshot_in_defaultfolder` - スナップショットが既定以外の場所でのみ使用できる場合は、値に **false** を指定します。  
  
     パブリケーションの作成の詳細については、「 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)」を参照してください。  
  
### <a name="to-configure-snapshot-properties-when-creating-a-merge-publication"></a>マージ パブリケーションを作成するときにスナップショットのプロパティを構成するには  
  
1.  パブリッシャーで [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)を実行します。 `@publication` にパブリケーション名を、`@repl_freq` に **snapshot** と **continuous** のいずれかの値を指定し、次のスナップショット関連のパラメーターを少なくとも 1 つ指定します。  
  
    -   **alt_snapshot_folder** - このパブリケーションのスナップショットが、既定のスナップショット フォルダー以外の場所、または既定のスナップショット フォルダーに追加された場所からアクセスされる場合のパスを指定します。    
    -   `@compress_snapshot` - 代替スナップショット フォルダー内のスナップショット ファイルを CAB ファイル形式で圧縮する場合は **true** を指定します。   
    -   `@pre_snapshot_script` - 初期化時、初期スナップショットが適用される前にサブスクライバーで実行される **.sql** ファイルのファイル名と完全パスを指定します。    
    -   `@post_snapshot_script` - 初期化時、初期スナップショットが適用される後にサブスクライバーで実行される **.sql** ファイルのファイル名と完全パスを指定します。    
    -   `@snapshot_in_defaultfolder` - スナップショットが既定以外の場所でのみ使用できる場合は、値に **false** を指定します。  
  
2.  パブリケーションの作成の詳細については、「 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)」を参照してください。  
  
### <a name="to-modify-snapshot-properties-of-an-existing-snapshot-or-transactional-publication"></a>既存のスナップショット パブリケーションまたはトランザクション パブリケーションに対してスナップショットのプロパティを変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)を実行します。 `@force_invalidate_snapshot` の値に **1** および `@property` に次のいずれかの値を指定します。  
  
    -   **alt_snapshot_folder** - `@value` に代替スナップショットへの新しいパスも指定します。    
    -   **compress_snapshot** - 代替スナップショット フォルダー内のスナップショット ファイルを CAB ファイル形式で圧縮するかどうかを示すには、`@value` に **true** または **false** も指定します。    
    -   **pre_snapshot_script** - 初期化時、初期スナップショットが適用される前にサブスクライバーで実行される **.sql** ファイルのファイル名と完全パスも `@value` に指定します。    
    -   **post_snapshot_script** - 初期化時、初期スナップショットが適用される後にサブスクライバーで実行される **.sql** ファイルのファイル名と完全パスも `@value` に指定します。    
    -   **snapshot_in_defaultfolder** - スナップショットを既定の場所に格納するかどうかを **true** または **false** で指定します。  
  
2.  (省略可) パブリッシャーのパブリケーション データベースで [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)を実行します。 `@publication` を指定し、変更の対象となる、スケジュールまたはセキュリティ資格情報関連のパラメーターを少なくとも 1 つ指定します。  
  
    > [!IMPORTANT]  
    >  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
3.  コマンド プロンプトから [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) を実行するか、スナップショット エージェント ジョブを起動して新しいスナップショットを生成します。 詳しくは、「 [初期スナップショットの作成および適用](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」をご覧ください。  
  
### <a name="to-modify-snapshot-properties-of-an-existing-merge-publication"></a>既存のマージ パブリケーションに対してスナップショットのプロパティを変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)を実行します。 `@force_invalidate_snapshot` の値に **1** および `@property**` に次のいずれかの値を指定します。  
  
    -   **alt_snapshot_folder** - `@value` に代替スナップショットへの新しいパスも指定します。    
    -   **compress_snapshot** - 代替スナップショット フォルダー内のスナップショット ファイルを CAB ファイル形式で圧縮するかどうかを示すには、`@value` に **true** または **false** も指定します。    
    -   **pre_snapshot_script** - 初期化時、初期スナップショットが適用される前にサブスクライバーで実行される **.sql** ファイルのファイル名と完全パスも `@value` に指定します。    
    -   **post_snapshot_script** - 初期化時、初期スナップショットが適用される後にサブスクライバーで実行される **.sql** ファイルのファイル名と完全パスも `@value` に指定します。    
    -   **snapshot_in_defaultfolder** - スナップショットを既定の場所に格納するかどうかを **true** または **false** で指定します。  
  
2.  コマンド プロンプトから [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) を実行するか、スナップショット エージェント ジョブを起動して新しいスナップショットを生成します。 詳しくは、「 [初期スナップショットの作成および適用](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」をご覧ください。  
  
## <a name="example"></a>例  
 次の例では、代替スナップショット フォルダーと圧縮スナップショットを使用したパブリケーションを作成します。  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../relational-databases/replication/codesnippet/tsql/configure-snapshot-prope_1.sql)]  
  
## <a name="see-also"></a>参照  
 [スナップショット オプションの変更](../../../relational-databases/replication/snapshot-options.md)   
 [スナップショットが適用される前および後のスクリプトの実行](../../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [FTP によるスナップショットの転送](../../../relational-databases/replication//publish/deliver-a-snapshot-through-ftp.md)   
 [パブリケーションおよびアーティクルのプロパティの変更](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)  
  
  
