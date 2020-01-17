---
title: データの競合の表示および解決 (マージ)
description: SQL Server のマージ パブリケーションでデータの競合を表示および解決する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 79dc4b26ee543aa99b9fc90e29f7bb6c7d571555
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321889"
---
# <a name="conflict-resolution-for-merge-replication"></a>マージ レプリケーションの競合の解決
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  マージ レプリケーションの競合は、各アーティクルに対して指定された競合回避モジュールに基づいて解決されます。 既定では、競合はユーザーの介入を必要とせずに解決されます。 ただし、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] レプリケーション競合表示モジュールで競合を表示したり、解決の結果を変更したりすることができます。  
  
 競合データは、競合の保有期間に指定した期間内 (既定では 14 日間) はレプリケーション競合表示モジュールで利用できます。 競合の保有期間を設定するには、次のいずれかを実行します。  
  
-   [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) の `@conflict_retention` パラメーターに保有期間の値を指定します。  
  
-   [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) の `@property` パラメーターに **conflict_retention** を、`@value` パラメーターに保有期間の値を指定します。  
  
 競合情報の既定の保存先は次のとおりです。    
-   パブリケーションの互換性レベルが 90 RTM 以上の場合は、パブリッシャーおよびサブスクライバーに保存されます。   
-   パブリケーションの互換性レベルが 80 RTM 未満の場合は、パブリッシャーに保存されます。   
-   サブスクライバーが [!INCLUDE[ssEW](../../includes/ssew-md.md)]を実行している場合は、パブリッシャーに保存されます。 競合データを [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバーに保存することはできません。  
  
 競合情報を格納する領域は、 **conflict_logging** パブリケーション プロパティによって制御されます。 詳細については、「[sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)」と「[sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)」をご覧ください。  
  
 競合は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] のインタラクティブ競合回避モジュールを使用して、同期実行時に対話的に解決することもできます。 インタラクティブ競合回避モジュールは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 同期マネージャーで利用できます。 詳細については、「[Windows 同期マネージャーを使用したサブスクリプションの同期 &#40;Windows 同期マネージャー&#41;](../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)」をご覧ください。  
  
## <a name="resolve-conflicts"></a>競合の解決  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のパブリッシャー (または必要に応じてサブスクライバー) に接続して、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  競合を表示するパブリケーションを右クリックしてから、 **[競合の表示]** をクリックします。  
  
    > [!NOTE]  
    >  **conflict_logging** プロパティの値として **'subscriber'** を指定した場合は、 **[競合の表示]** メニュー オプションを利用できません。 競合を表示するには、コマンド プロンプトで ConflictViewer.exe を起動します。 既定では、ConflictViewer.exe は Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE のディレクトリにあります。 有効な起動時のパラメーターの一覧を表示するには、ConflictViewer.exe -? を実行します。  
  
4.  **[競合テーブルの選択]** ダイアログ ボックスで、競合を表示するデータベース、パブリケーション、およびテーブルを選択します。  
  
5.  レプリケーション競合表示モジュールでは、以下を実行できます。  
  
    -   上のグリッドの右側のボタンで行をフィルター選択する。  
  
    -   上のグリッドで行を選択して、下のグリッドにその行の情報を表示する。  
  
    -   上のグリッドで 1 つ以上の行を選択し、 **[削除]** をクリックする。これは、データに変更を加えずに **[優先されたデータの送信]** をクリックするのと同じです。  
  
    -   プロパティ ボタン **[...]** をクリックし、競合に関係のある列の詳細情報を表示する。  
  
    -   データを送信する前に、 **[競合で優先されたデータ]** 列または **[競合で優先されなかったデータ]** 列でデータを編集する (列が灰色の場合、データは読み取り専用です)。  
  
    -   **[優先されたデータの送信]** をクリックし、競合で優先するデータとして指定された行を受け入れる。  
  
    -   **[優先されなかったデータの送信]** をクリックして解決をオーバーライドし、競合で優先されないデータとして指定された値をトポロジのすべてのノードに反映する。  
  
    -   **[この競合の詳細をログに記録する]** を選択して、競合のデータをログ ファイルに記録する。 ファイルの場所を指定するには、 **[表示]** メニューをポイントし、 **[オプション]** をクリックします。 値を入力するか、または参照ボタン ( **[...]** ) をクリックして適切なファイルに移動します。 **[OK]** をクリックして、 **[オプション]** ダイアログ ボックスを終了します。  
  
6.  レプリケーション競合表示モジュールを閉じます。  

## <a name="view-conflict-information"></a>競合情報の表示
マージ レプリケーションの競合を解決すると、優先されなかった行のデータが競合テーブルに書き込まれます。 この競合データは、レプリケーション ストアド プロシージャを使用してプログラムから表示できます。 詳細については、「 [マージ レプリケーションの競合検出および解決の詳細](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)」を参照してください。  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)を実行します。 結果セットで、次の列の値を確認します。  
  
    -   **centralized_conflicts** - 1 は競合する行がパブリッシャーに格納されていることを示し、0 は競合する行がパブリッシャーに格納されていないことを示します。  
  
    -   **decentralized_conflicts** - 1 は競合する行がサブスクライバーに格納されていることを示し、0 は競合する行がサブスクライバーに格納されていないことを示します。  
  
        > [!NOTE]  
        >  マージ パブリケーションの競合ログの動作は、[sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) の `@conflict_logging` パラメーターを使用して設定します。 `@centralized_conflicts` パラメータの使用は非推奨です。  
  
     次の表では、`@conflict_logging` に対して指定された値に基づくこれらの列の値について説明します。  
  
    |@conflict_logging 値|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**publisher**|1|0|  
    |**サブスクライバー**|0|1|  
    |**両方**|1|1|  
  
2.  パブリッシャー側のパブリケーション データベースまたはサブスクライバー側のサブスクリプション データベースに対して、 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)を実行します。 特定のパブリケーションに属するアーティクルの競合情報のみが返されるようにするには、`@publication` に値を指定します。 これにより、競合を持つアーティクルに対応する競合テーブル情報が返されます。 目的のアーティクルに対応する **conflict_table** の値を確認します。 アーティクルに対応する **conflict_table** の値が NULL の場合、そのアーティクル内では削除競合のみが発生しています。  
  
3.  (省略可) 目的のアーティクルで競合する行を確認します。 手順 1. の **centralized_conflicts** および **decentralized_conflicts** の値に応じて、次のいずれかの操作を実行します。  
  
    -   パブリッシャー側のパブリケーション データベースに対して、 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)を実行します。 手順 1 で確認したアーティクルの競合テーブルを `@conflict_table` に指定します。 (省略可) 特定のパブリケーションの競合情報が返されるように制限するには、`@publication` の値を指定します。 これにより、優先されなかった行の行データとその他の情報が返されます。  
  
    -   サブスクライバー側のサブスクリプション データベースに対して、 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)を実行します。 手順 1 で確認したアーティクルの競合テーブルを `@conflict_table` に指定します。 これにより、優先されなかった行の行データとその他の情報が返されます。  
  
## <a name="conflict-where-delete-failed"></a>削除が失敗した場合の競合   
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)を実行します。 結果セットで、次の列の値を確認します。  
  
    -   **centralized_conflicts** - 1 は競合する行がパブリッシャーに格納されていることを示し、0 は競合する行がパブリッシャーに格納されていないことを示します。  
  
    -   **decentralized_conflicts** - 1 は競合する行がサブスクライバーに格納されていることを示し、0 は競合する行がサブスクライバーに格納されていないことを示します。  
  
        > [!NOTE]  
        >  マージ パブリケーションの競合ログの動作は、[sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) の `@conflict_logging` パラメーターを使用して設定します。 `@centralized_conflicts` パラメータの使用は非推奨です。  
  
2.  パブリッシャー側のパブリケーション データベースまたはサブスクライバー側のサブスクリプション データベースに対して、 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)を実行します。 特定のパブリケーションに属するアーティクルの競合テーブル情報のみが返されるようにするには、`@publication` に値を指定します。 これにより、競合を持つアーティクルに対応する競合テーブル情報が返されます。 目的のアーティクルに対応する **source_object** の値を確認します。 アーティクルに対応する **conflict_table** の値が NULL の場合、そのアーティクル内では削除競合のみが発生しています。  
  
3.  (省略可) 削除競合の競合情報を確認します。 手順 1. の **centralized_conflicts** および **decentralized_conflicts** の値に応じて、次のいずれかの操作を実行します。  
  
    -   パブリッシャー側のパブリケーション データベースに対して、 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)を実行します。 手順 1 で確認した、競合が発生しているソース テーブルの名前を、`@source_object` に指定します。 (省略可) 特定のパブリケーションの競合情報が返されるように制限するには、`@publication` の値を指定します。 これにより、パブリッシャーに格納されている削除競合の情報が返されます。  
  
    -   サブスクライバー側のサブスクリプション データベースに対して、 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)を実行します。 手順 1 で確認した、競合が発生しているソース テーブルの名前を、`@source_object` に指定します。 (省略可) 特定のパブリケーションの競合情報が返されるように制限するには、`@publication` の値を指定します。 これにより、サブスクライバーに格納されている削除競合の情報が返されます。  
  
## <a name="see-also"></a>参照  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [マージ アーティクル競合回避モジュールの指定](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
  
