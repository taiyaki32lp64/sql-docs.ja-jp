---
title: スナップショットのプロパティの構成 (レプリケーション Transact-SQL プログラミング) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: b03dd7f886cee5816d591034d1be63ece45d8d1d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63021335"
---
# <a name="configure-snapshot-properties-replication-transact-sql-programming"></a>スナップショットのプロパティの構成 (レプリケーション Transact-SQL プログラミング)
  スナップショットのプロパティは、レプリケーションのストアド プロシージャを使用し、プログラムから定義および変更できます。使用するストアド プロシージャは、パブリケーションの種類によって異なります。  
  
### <a name="to-configure-snapshot-properties-when-creating-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションを作成するときにスナップショットのプロパティを構成するには  
  
1.  パブリッシャーで [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)を実行します。 このとき、 **@publication** にパブリケーション名を、 **@repl_freq** に **snapshot** と **@repl_freq** のいずれかの値を指定し、次のスナップショット関連のパラメーターを少なくとも 1 つ指定します。  
  
    -   **@alt_snapshot_folder** - このパブリケーションのスナップショットが既定のスナップショット フォルダー以外の場所 (または既定のスナップショット フォルダーに追加された場所) に保存されている場合のパスを指定します。  
  
    -   **@compress_snapshot** - 代替スナップショット フォルダー内のスナップショット ファイルを **CAB ファイル形式で圧縮する場合は** true [!INCLUDE[msCoName](../../../includes/msconame-md.md)] を指定します。  
  
    -   **@pre_snapshot_script** - 初期化時、初期スナップショットが適用される前にサブスクライバー側で実行される **.sql** ファイルのファイル名と完全パスを指定します。  
  
    -   **@post_snapshot_script** - 初期化時、初期スナップショットが適用される前にサブスクライバー側で実行される **.sql** ファイルのファイル名と完全パスを指定します。  
  
    -   **@snapshot_in_defaultfolder** - 代替スナップショット フォルダー内のスナップショット ファイルを **false** を指定します。  
  
     パブリケーションの作成の詳細については、「 [Create a Publication](create-a-publication.md)」を参照してください。  
  
### <a name="to-configure-snapshot-properties-when-creating-a-merge-publication"></a>マージ パブリケーションを作成するときにスナップショットのプロパティを構成するには  
  
1.  パブリッシャーで [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)を実行します。 このとき、 **@publication** にパブリケーション名を、 **@repl_freq** に **snapshot** と **@repl_freq** のいずれかの値を指定し、次のスナップショット関連のパラメーターを少なくとも 1 つ指定します。  
  
    -   **@alt_snapshot_folder** - このパブリケーションのスナップショットが既定のスナップショット フォルダー以外の場所 (または既定のスナップショット フォルダーに追加された場所) に保存されている場合のパスを指定します。  
  
    -   **@compress_snapshot** - 代替スナップショット フォルダー内のスナップショット ファイルを **CAB ファイル形式で圧縮する場合は** を指定します。  
  
    -   **@pre_snapshot_script** - 初期化時、初期スナップショットが適用される前にサブスクライバー側で実行される **.sql** ファイルのファイル名と完全パスを指定します。  
  
    -   **@post_snapshot_script** - 初期化時、初期スナップショットが適用される前にサブスクライバー側で実行される **.sql** ファイルのファイル名と完全パスを指定します。  
  
    -   **@snapshot_in_defaultfolder** - 代替スナップショット フォルダー内のスナップショット ファイルを **false** を指定します。  
  
2.  パブリケーションの作成の詳細については、「 [Create a Publication](create-a-publication.md)」を参照してください。  
  
### <a name="to-modify-snapshot-properties-of-an-existing-snapshot-or-transactional-publication"></a>既存のスナップショット パブリケーションまたはトランザクション パブリケーションに対してスナップショットのプロパティを変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)を実行します。 このとき、 **@force_invalidate_snapshot** と **@force_invalidate_snapshot** を指定し、次のいずれかの値を **@property** に指定します。  
  
    -   **alt_snapshot_folder** - **@value** を実行します。  
  
    -   **compress_snapshot** - 代替スナップショット フォルダー内のスナップショット ファイルを CAB ファイル形式で圧縮するかを示す **CAB ファイル形式で圧縮する場合は** に **false** と **@value** に指定します。  
  
    -   **pre_snapshot_script** - 初期化時、初期スナップショットが適用される前にサブスクライバー側で実行される **@value** ファイルのファイル名と完全パスを **.sql** ファイルのファイル名と完全パスを指定します。  
  
    -   **post_snapshot_script** - 初期化時、初期スナップショットが適用される前にサブスクライバー側で実行される **@value** ファイルのファイル名と完全パスを **.sql** ファイルのファイル名と完全パスを指定します。  
  
    -   **snapshot_in_defaultfolder** - スナップショットを既定の場所に格納するかどうかを **true** または **false** で指定します。  
  
2.  (省略可) パブリッシャーのパブリケーション データベースで [sp_changepublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql)を実行します。 このとき、 **@publication** を指定し、変更の対象となる、スケジュールまたはセキュリティ資格情報関連のパラメーターを少なくとも 1 つ指定します。  
  
    > [!IMPORTANT]  
    >  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
3.  コマンド プロンプトから [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) を実行するか、スナップショット エージェント ジョブを起動して新しいスナップショットを生成します。 詳細については、「 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)」を参照してください。  
  
### <a name="to-modify-snapshot-properties-of-an-existing-merge-publication"></a>既存のマージ パブリケーションに対してスナップショットのプロパティを変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)を実行します。 このとき、 **@force_invalidate_snapshot** と **@force_invalidate_snapshot** を指定し、次のいずれかの値を **@property** に指定します。  
  
    -   **alt_snapshot_folder** - **@value** を実行します。  
  
    -   **compress_snapshot** - 代替スナップショット フォルダー内のスナップショット ファイルを CAB ファイル形式で圧縮するかを示す **CAB ファイル形式で圧縮する場合は** に **false** と **@value** に指定します。  
  
    -   **pre_snapshot_script** - 初期化時、初期スナップショットが適用される前にサブスクライバー側で実行される **@value** ファイルのファイル名と完全パスを **.sql** ファイルのファイル名と完全パスを指定します。  
  
    -   **post_snapshot_script** - 初期化時、初期スナップショットが適用される前にサブスクライバー側で実行される **@value** ファイルのファイル名と完全パスを **.sql** ファイルのファイル名と完全パスを指定します。  
  
    -   **snapshot_in_defaultfolder** - スナップショットを既定の場所に格納するかどうかを **true** または **false** で指定します。  
  
2.  コマンド プロンプトから [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) を実行するか、スナップショット エージェント ジョブを起動して新しいスナップショットを生成します。 詳しくは、「 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)」をご覧ください。  
  
## <a name="example"></a>例  
 次の例では、代替スナップショット フォルダーと圧縮スナップショットを使用したパブリケーションを作成します。  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubaltsnapshot.sql#sp_mergealtsnapshot)]  
  
## <a name="see-also"></a>関連項目  
 [スナップショット フォルダーの代替位置](../alternate-snapshot-folder-locations.md)   
 [圧縮スナップショット](../compressed-snapshots.md)   
 [スナップショットが適用される前および後のスクリプトの実行](../snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [FTP によるスナップショットの転送](../transfer-snapshots-through-ftp.md)   
 [パブリケーションおよびアーティクルのプロパティの変更](change-publication-and-article-properties.md)  
  
  
