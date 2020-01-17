---
title: アーティクルの追加および削除 (既存のパブリケーション)
description: SQL Server の既存のパブリケーションでアーティクルを追加およびアーティクルを削除する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- removing articles
- dropping articles
- adding articles
- administering replication, articles
- publications [SQL Server replication], adding and dropping articles
- articles [SQL Server replication], adding
ms.assetid: b148e907-e1f2-483b-bdb2-59ea596efceb
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: e996ccfd6f6930b4741f15b3da82c1f2856bd4db
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321332"
---
# <a name="add-articles-to-and-drop-articles-from-existing-publications"></a>既存のパブリケーションでのアーティクルの追加および削除
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  パブリケーションを作成したら、アーティクルを追加および削除できます。 アーティクルはいつでも追加できますが、アーティクルを削除するために必要な操作は、レプリケーションの種類と、アーティクルを削除するタイミングによって異なります。  
  
## <a name="adding-articles"></a>アーティクルの追加  
 アーティクルを追加するには、アーティクルへのパブリケーションの追加、パブリケーションの新しいスナップショットの作成、サブスクリプションの同期による新しいアーティクルのスキーマとデータの適用を行います。  
  
> [!NOTE]
>  マージ パブリケーションにアーティクルを追加する際に、その新しいアーティクルに既存のアーティクルが依存している場合は、[sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) および [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) の **\@processing_order** パラメーターを使用して、両方のアーティクルの処理順序を指定する必要があります。 たとえば、テーブルをパブリッシュし、テーブルが参照している関数はパブリッシュしない場合を考えます。 この関数をパブリッシュしないと、サブスクライバー側でテーブルを作成できないとします。 この場合は、この関数をパブリケーションに追加するときに、**sp_addmergearticle** の **\@processing_order** パラメーターに値 **1** を指定し、**sp_changemergearticle** の **\@processing_order** パラメーターに値 **2** を指定します。パラメーター **\@article** にはテーブル名を指定します。 この処理順序により、サブスクライバー側で関数に依存するテーブルを作成する前に、関数の作成が求められるようになります。 各アーティクルに使用する値は、関数の値がテーブルの値より小さければ、別の値でもかまいません。  
  
1.  次のいずれかの方法を使用して、1 つ以上のアーティクルを追加します。  
  
    -   [パブリケーションでのアーティクルの追加または削除 (SQL Server Management Studio)](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md)  
  
    -   [アーティクルの定義](../../../relational-databases/replication/publish/define-an-article.md)  
  
2.  パブリケーションにアーティクルを追加したら、パブリケーションの新しいスナップショット (およびパラメーター化されたフィルターを使用したマージ パブリケーションの場合は、すべてのパーティション) を作成する必要があります。 その後、ディストリビューション エージェントまたはマージ エージェントによって、新しいアーティクルのスキーマおよびデータがサブスクライバーにコピーされます (パブリケーション全体が再初期化されるわけではありません)。  
  
    -   新しいスナップショットを作成するには、「 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」を参照してください。  
  
    -   パラメーター化されたフィルターを使用してマージ パブリケーションに新しいスナップショットを作成するには、「[パラメーター化されたフィルターを使用したパブリケーションのスナップショットの作成](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」 (パラメーター化されたフィルターを使用してマージ パブリケーションのスナップショットを作成する) を参照してください。  
  
3.  スナップショットを作成したら、サブスクリプションを同期し、新しいアーティクルのスキーマおよびデータをコピーします。  

    -   プッシュ サブスクリプションを同期するには、「[Synchronize a Push Subscription](../../../relational-databases/replication/synchronize-a-push-subscription.md)」 (プッシュ サブスクリプションの同期) を参照してください。  
  
    -   プル サブスクリプションを同期するには、「[Synchronize a Pull Subscription](../../../relational-databases/replication/synchronize-a-pull-subscription.md)」 (プル サブスクリプションの同期) を参照してください。  
  
## <a name="dropping-articles"></a>アーティクルのドロップ  
 アーティクルはパブリケーションからいつでも削除できます。ただし、次の動作について考慮する必要があります。  
  
-   パブリケーションからアーティクルを削除しても、パブリケーション データベースからオブジェクトが削除されたり、サブスクリプション データベースから対応するオブジェクトが削除されるわけではありません。 必要に応じて、DROP \<Object> を使用し、これらのオブジェクトを削除します。 パブリッシュされた他のアーティクルに外部キー制約を通じて関連付けられているアーティクルを削除するときは、手動またはオンデマンド スクリプトの実行により、サブスクライバーでテーブルを削除することをお勧めします。適切な DROP \<Object> ステートメントを含むスクリプトを指定してください。 詳細については、「[同期中のスクリプトの実行 (レプリケーション Transact-SQL プログラミング)](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)」を参照してください。  
  
-   互換性レベル 90RTM 以上のマージ パブリケーションの場合、アーティクルはいつでも削除できますが、新しいスナップショットが必要です。 追加として:  
  
    -   アーティクルが結合フィルター リレーションシップまたは論理レコード リレーションシップの親アーティクルの場合、最初にリレーションシップの削除が必要ですが、これには再初期化が必要になります。  
  
    -   アーティクルにパブリケーションの最後のパラメーター化されたフィルターが含まれる場合、サブスクリプションを再初期化する必要があります。  
  
-   互換性レベルが 90RTM 未満のマージ パブリケーションの場合、アーティクルは特別な注意をせずに、サブスクリプションの初期同期の前に削除できます。 1 つ以上のサブスクリプションが同期された後にアーティクルが削除された場合、サブスクリプションの削除、再作成、および同期が必要です。  
  
-   スナップショット パブリケーションまたはトランザクション パブリケーションの場合、アーティクルはサブスクリプションを作成する前に、特別な事項を考慮せずに削除できます。 1 つ以上のサブスクリプションが作成された後にアーティクルが削除された場合、サブスクリプションの削除、再作成、および同期が必要です。 サブスクリプションの削除の詳細については、「[パブリケーションのサブスクライブ](../../../relational-databases/replication/subscribe-to-publications.md)」と「[sp_dropsubscription (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)」を参照してください。 **sp_dropsubscription** を使用すると、サブスクリプション全体ではなく、サブスクリプションの 1 つのアーティクルを削除できます。  
  
1.  パブリケーションからアーティクルを削除するには、アーティクルを削除し、パブリケーションの新しいスナップショットを作成します。 アーティクルを削除すると、現在のスナップショットは無効になります。したがって新しいスナップショットを作成する必要があります。  
  
    -   パブリケーションからアーティクルを削除するには、「[パブリケーションでのアーティクルの追加または削除 (SQL Server Management Studio)](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md)」または「[Delete an Article](../../../relational-databases/replication/publish/delete-an-article.md)」 (アーティクルの削除) を参照してください。  
  
2.  パブリケーションからアーティクルを削除したら、パブリケーションの新しいスナップショット (およびパラメーター化されたフィルターを使用したマージ パブリケーションの場合は、すべてのパーティション) を作成する必要があります。  
  
    -   新しいスナップショットを作成するには、「 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」を参照してください。  
  
    -   パラメーター化されたフィルターを使用してマージ パブリケーションに新しいスナップショットを作成するには、「[パラメーター化されたフィルターを使用したパブリケーションのスナップショットの作成](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」 (パラメーター化されたフィルターを使用してマージ パブリケーションのスナップショットを作成する) を参照してください。  
  
 前述のように、場合によっては、アーティクルを削除するために、サブスクリプションの削除、再作成、および同期が必要になる場合があります。 詳細については、「[パブリケーションのサブスクライブ](../../../relational-databases/replication/subscribe-to-publications.md)」と「[データの同期](../../../relational-databases/replication/synchronize-data.md)」を参照してください。  
 
 > [!NOTE]
 > **[!INCLUDE[ssSQL15](../../../includes/sssql14-md.md)] Service Pack 2** 以降、および **[!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] Service Pack 1** 以降では、トランザクション レプリケーションに参加しているアーティクルに **DROP TABLE** DLL コマンドを使用する、テーブルの削除をサポートします。 DROP TABLE DDL がパブリケーションでサポートされる場合、DROP TABLE 操作ではパブリケーションとデータベースからテーブルが削除されます。 ログ リーダー エージェントでは、削除されたテーブルのディストリビューション データベースのクリーンアップ コマンドをポストし、パブリッシャーのメタデータのクリーンアップを実行します。 ログ リーダーで削除されたテーブルを参照しているすべてのログ レコードを処理していない場合、削除されたテーブルに関連付けられている新しいコマンドは無視されます。 既に処理されているレコードは、ディストリビューション データベースに配信されます。 ログ リーダーが廃止 (削除) されたアーティクルをクリーンアップする前に、ディストリビューション エージェントがレコードを処理する場合、これらのレコードはサブスクライバー データベースに適用される可能性があります。 すべてのトランザクション レプリケーション パブリケーションに対する**既定**の設定では、DROP TABLE DLL をサポートしません。 [KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactional-replication-in-sql-server-2014-or-in-sql-server-2016-sp1) には、この改善機能に関する詳細が含まれます。

  
## <a name="see-also"></a>参照  
 [データとデータベース オブジェクトのパブリッシュ](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [サブスクリプションの再初期化](../../../relational-databases/replication/reinitialize-subscriptions.md)   
 [パブリケーション データベースでのスキーマの変更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
