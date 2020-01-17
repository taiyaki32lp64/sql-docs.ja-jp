---
title: ピア ツー ピア レプリケーションにおける競合検出 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, peer-to-peer replication
- peer-to-peer transactional replication, conflict detection
ms.assetid: 754a1070-59bc-438d-998b-97fdd77d45ca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9db326ac27a7137f03f34e242c3c5c3931637f36
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68198991"
---
# <a name="conflict-detection-in-peer-to-peer-replication"></a>ピア ツー ピア レプリケーションにおける競合検出
  ピア ツー ピア トランザクション レプリケーションを使用すると、トポロジ内の任意のノードでデータの挿入、更新、または削除を実行し、データ変更をその他のノードに反映させることができます。 どのノードでもデータを変更できるので、さまざまなノードで行われたデータ変更が相互に競合する場合があります。 行が複数のノードで変更されると、他のノードに反映される際に競合が発生したり、場合によっては更新データが失われたりする可能性があります。  
  
 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 以降のバージョンのピア ツー ピア レプリケーションには、ピア ツー ピア トポロジの競合の検出を有効にするオプションが導入されています。 このオプションは、検出されない競合によって引き起こされる問題 (アプリケーションの動作の矛盾や更新データの喪失など) の防止に役立ちます。 このオプションが有効になっている場合は、競合する変更が、ディストリビューション エージェントの障害を引き起こす重大なエラーとして既定で扱われるようになります。 競合が発生した場合は、その競合が解決されて、トポロジでデータの一貫性が確保されるまで、トポロジが一貫性のない状態のままになります。  
  
> [!NOTE]  
>  データの不整合が生じないようにするため、競合の検出を有効にしている場合でも、ピア ツー ピア トポロジで競合を発生させないようにしてください。 特定の行の書き込み操作が 1 つのノードだけで行われるようにするには、データにアクセスしてそのデータを変更するアプリケーションで、挿入、更新、および削除の各操作をパーティション分割する必要があります。 これにより、1 つのノードの特定の行に対する変更は、トポロジ内の他のすべてのノードと同期されてから、別のノードでその行が変更されるようになります。 競合の検出と解決のための高度な機能がアプリケーションに必要な場合は、マージ レプリケーションを使用します。 詳細については、「[Merge Replication](../merge/merge-replication.md)」 (マージ レプリケーション) と「[Detect and Resolve Merge Replication Conflicts](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)」 (マージ レプリケーションの競合の検出と解決) を参照してください。  
  
## <a name="understanding-conflicts-and-conflict-detection"></a>競合と競合検出について  
 1 つのデータベース内では、異なるアプリケーションによって同じ行が変更されても、競合は発生しません。 これは、トランザクションがシリアル化され、同時変更はロックを使用して処理されるためです。 ピア ツー ピア レプリケーションなどの非同期の分散システムでは、トランザクションが各ノードで独立して実行されます。つまり、複数のノード間でトランザクションをシリアル化するメカニズムはありません。 2 フェーズ コミットのようなプロトコルを使用することはできますが、これはパフォーマンスに重大な影響を及ぼします。  
  
 ピア ツー ピア レプリケーションなどのシステムでは、各ピアで変更がコミットされた場合、競合が検出されません。 競合が検出されるのは、こうした変更が他のピアにレプリケートされて適用された場合です。 ピア ツー ピア レプリケーションでは、各ノードに変更を適用するストアド プロシージャが、パブリッシュされた各テーブルの非表示の列に基づいて、競合を検出します。 この非表示の列には、各ノードに指定する *発信元 ID* と行のバージョンを組み合わせた ID が格納されます。 同期中、ディストリビューション エージェントは各テーブルに対してストアド プロシージャを実行します。 これらのストアド プロシージャは、他のピアからの挿入操作、更新操作、および削除操作を適用します。 プロシージャの 1 つが非表示列の値を読み取る際に競合を検出すると、次に示す、重大度レベル 16 のエラー 22815 が発生します。  
  
 `A conflict of type '%s' was detected at peer %d between peer %d (incoming), transaction id %s  and peer %d (on disk), transaction id %s`  
  
 既定では、このエラーにより、ディストリビューション エージェントがそのノードへの変更の適用を中止します。 検出される競合の処理方法の詳細については、このトピックの「競合の処理」を参照してください。  
  
> [!NOTE]  
>  非表示の列にアクセスできるのは、専用管理者接続 (DAC) を使用してログインしているユーザーのみです。 DAC の詳細については、「[Diagnostic Connection for Database Administrators](../../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)」 (データベース管理者用の診断接続) を参照してください。  
  
 ピア ツー ピア レプリケーションでは、次の種類の競合が検出されます。  
  
-   挿入と挿入  
  
     ピア ツー ピア レプリケーションに参加している各テーブルのすべての行は、主キー値を使用して一意に識別されます。 挿入と挿入の競合は、キー値の同じ行が複数のノードで挿入されたときに発生します。  
  
-   更新と更新  
  
     複数のノードで同じ行が更新されたときに発生します。  
  
-   挿入と更新  
  
     あるノードで行が更新され、別のノードで同じ行が削除された後に再挿入された場合に発生します。  
  
-   挿入と削除  
  
     あるノードで行が削除され、別のノードで同じ行が削除された後に再挿入された場合に発生します。  
  
-   更新と削除  
  
     あるノードで行が更新され、別のノードで同じ行が削除された場合に発生します。  
  
-   削除と削除  
  
     複数のノードで同じ行が削除された場合に発生します。  
  
## <a name="enabling-conflict-detection"></a>競合検出の有効化  
 競合検出を使用するには、すべてのノードが [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 以降のバージョンを実行しており、すべてのノードで検出が有効になっている必要があります。 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 以降のバージョンの [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]では、既定で、競合検出が有効になっています。 競合を想定していない場合でも、競合検出を有効にしておくことをお勧めします。 競合検出は、 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)] ストアド プロシージャを使用して有効または無効にできます。  
  
-   [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] では、 **[パブリケーションのプロパティ]** ダイアログ ボックスの **[サブスクリプション オプション]** ページまたはピア ツー ピア トポロジ構成ウィザードの **[トポロジの構成]** ページを使用して、検出を有効または無効にできます。  
  
     [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]を使用して競合検出を構成すると、ディストリビューション エージェントは、競合の検出時に変更の適用を停止するように構成されます。  
  
-   検出は、 [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) ストアド プロシージャまたは [sp_configure_peerconflictdetection](/sql/relational-databases/system-stored-procedures/sp-configure-peerconflictdetection-transact-sql)ストアド プロシージャを使用して有効または無効にすることもできます。  
  
     ストアド プロシージャを使用して競合検出を構成すると、競合の検出時にディストリビューション エージェントが変更の適用を停止するかどうかを指定できます。 既定では、ディストリビューション エージェントは変更の適用を停止します。 ここでは、既定の設定を使用することをお勧めします。  
  
## <a name="handling-conflicts"></a>競合の処理  
 ピア ツー ピア レプリケーションで競合が発生した場合、ピア ツー ピア競合検出の警告が発生します。 競合の発生時に通知されるように、この警告を構成することをお勧めします。 警告の詳細については、「[Use Alerts for Replication Agent Events](../agents/use-alerts-for-replication-agent-events.md)」 (レプリケーション エージェント イベントに対する警告の使用) を参照してください。  
  
 ディストリビューション エージェントが停止して警告が発生したら、次のいずれかの方法を使用して、発生した競合を処理します。  
  
-   競合が検出されたノードを、必要なデータが格納されているノードのバックアップから再初期化します (推奨)。 これにより、データの一貫性を確保します。  
  
-   ディストリビューション エージェントが引き続き変更を適用できるようにすることで、ノードの同期を再試行します。  
  
    1.  実行[sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql): 'p2p_continue_onconflict' を指定、@propertyパラメーターと`true`の@valueパラメーター。  
  
    2.  ディストリビューション エージェントを再起動します。  
  
    3.  競合表示モジュールを使用して検出された競合を確認し、関係する行、競合の種類、および優先されたデータを特定します。 競合は、構成時に指定した発信元 ID 値に基づいて解決されます。つまり、最も ID の大きいノードの行が競合で優先されます。 詳細については、「[View Data Conflicts for Transactional Publications &#40;SQL Server Management Studio&#41;](../view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)」 (トランザクション パブリケーションのデータの競合の表示 &#40;SQL Server Management Studio&#41;) を参照してください。  
  
    4.  検証を実行して、競合する行が正しく収束したことを確認します。 詳細については、「[Validate Replicated Data](../validate-data-at-the-subscriber.md)」 (レプリケートされたデータの検証) を参照してください。  
  
        > [!NOTE]  
        >  この手順の実行後にデータに一貫性がない場合は、最も優先度の高いノードの行を手動で更新して、そのノードから変更を反映する必要があります。 競合する変更がトポロジ内になくなると、すべてのノードが一貫性のある状態になります。  
  
    5.  実行[sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql): 'p2p_continue_onconflict' を指定、@propertyパラメーターと`false`の@valueパラメーター。  
  
## <a name="see-also"></a>関連項目  
 [@loopback_detection](peer-to-peer-transactional-replication.md)  
  
  
