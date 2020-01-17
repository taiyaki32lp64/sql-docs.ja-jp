---
title: レプリケートされたデータの検証 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Subscribers [SQL Server replication], data validation
- replication [SQL Server], validating data
- transactional replication, validating data
- validating data
- merge replication data validation [SQL Server replication], SQL Server Management Studio
ms.assetid: 215b4c9a-0ce9-4c00-ac0b-43b54151dfa3
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 354afb535abb1efab76e005d88b3bdfd464a299c
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710762"
---
# <a name="validate-replicated-data"></a>レプリケートされたデータの検証
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、サブスクライバーでデータを検証する方法について説明します。  
  
トランザクション レプリケーションとマージ レプリケーションを使用すると、サブスクライバーのデータがパブリッシャーのデータと一致するかどうかを検証できます。 検証は、1 つのパブリケーションの特定のサブスクリプション、またはすべてのサブスクリプションに対して行うことができます。 次のいずれかの種類の検証を指定すると、ディストリビューション エージェントまたはマージ エージェントは次回の実行時にデータを検証します。  
  
-   **行数のみ。** サブスクライバーのテーブルにパブリッシャーのテーブルと同じ数の行があるかどうかを検証しますが、行の内容が一致するかどうかについては検証しません。 行数の確認は、データに問題があるかどうかを調べる手軽な検証方法です。   
-   **行数とバイナリ チェックサム**。 パブリッシャーとサブスクライバーの行数に加え、チェックサム アルゴリズムを使用して、すべてのデータのチェックサムが計算されます。 行数の検証で失敗となった場合、チェックサムは実行されません。  
  
 サブスクライバーとパブリッシャーのデータが一致するかどうかの検証に加え、マージ レプリケーションでは、各サブスクライバーに対してデータが正しくパーティション分割されているかどうかを検証する機能も用意されています。 詳細については、「[Validate Partition Information for a Merge Subscriber](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md)」 (マージ サブスクライバーのパーティション情報の検証) を参照してください。  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
   
## <a name="how-data-validation-works"></a>データ検証の動作  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、パブリッシャー側の行数やチェックサムを計算し、それらの値をサブスクライバー側で計算された行数やチェックサムと比較することで、データの検証を行います。 一方の値はパブリケーション テーブル全体に対して計算され、もう一方の値はサブスクリプション テーブル全体に対して計算されます。ただし、 **text**列、 **ntext**列、または **image** 列にあるデータはその計算には含まれません。  
  
 計算が行われている間は、行数またはチェックサムの計算が行われているテーブルに共有ロックが一時的にかかりますが、計算はすぐに終了し、通常、数秒で共有ロックは解除されます。  
  
 バイナリ チェックサムを使用する場合は、32 ビット CRC (冗長性検査) がデータ ページの物理的な行ではなく、列ごとに実行されます。 これにより、テーブルの列がデータ ページで物理的にどのような順序であっても、行については同じ CRC 値が計算されます。 バイナリ チェックサムを使用した検証は、パブリケーション上に行フィルターまたは列フィルターがある場合に使用できます。  

 データの検証は、3 つの部分で構成されるプロセスです。  
  
1.  パブリケーションの単一のサブスクリプションまたはすべてのサブスクリプションが検証対象として *マーク* されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の **[ローカル パブリケーション]** フォルダーと **[ローカル サブスクリプション]** フォルダーから使用できる、 **[サブスクリプションの検証]** 、 **[サブスクリプションの検証]** および **[すべてのサブスクリプションの検証]** の各ダイアログ ボックスで検証対象のサブスクリプションにマークを付けます。 また、 **[すべてのサブスクリプション]** タブ、 **[サブスクリプション ウォッチ リスト]** タブ、およびレプリケーション モニターのパブリケーション ノードでもサブスクリプションにマークを付けることができます。 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)」 (レプリケーション モニターの開始) を参照してください。  
  
2.  サブスクリプションは、ディストリビューション エージェント (トランザクション レプリケーションの場合) またはマージ エージェント (マージ レプリケーションの場合) による次回の同期時に検証されます。 ディストリビューション エージェントは、通常は連続して実行されるので、検証はすぐに実行されます。マージ エージェントは、通常は要求時に実行されるので、エージェントを実行した後で検証が実行されます。  
  
3.  検証結果は次の場所で表示できます。   
    -   レプリケーション モニターの詳細ウィンドウ : トランザクション レプリケーションの場合は **[ディストリビューターからサブスクライバーまでの履歴]** タブ、およびマージ レプリケーションの場合は **[同期の履歴]** タブ    
    -   **の** [同期の状態の表示] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]ダイアログ ボックス  
 
## <a name="considerations-and-restrictions"></a>注意点と制約  
 データの検証に際しては、次の点に注意してください。  
  
-   データを検証する前にサブスクライバー側のすべての更新操作を停止する必要があります (検証実行時にパブリッシャー側の操作を停止する必要はありません)。  
-   チェックサムおよびバイナリ チェックサムを使用した検証を大規模なデータセットに対して行う場合には、大量のプロセッサ リソースが必要になるので、レプリケーションで使用するサーバーの利用状況が最小のときに検証を行うようにスケジュールする必要があります。   
-   レプリケーションはテーブルのみを検証します。スキーマのみのアーティクル (ストアド プロシージャなど) がパブリッシャーとサブスクライバーで同じであるかどうかは検証しません。   
-   バイナリ チェックサムは、パブリッシュされたどのテーブルでも使用できます。 チェックサムは、列フィルターの設定されたテーブル、または列オフセットが異なる論理テーブル構造 (列を削除または追加する ALTER TABLE ステートメントの結果) は検証できません。   
-   レプリケーション検証には、 **checksum** 関数および **binary_checksum** 関数を使用します。 各関数の動作については、「[CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)」と「[BINARY_CHECKSUM  &#40;Transact-SQL&#41;](../../t-sql/functions/binary-checksum-transact-sql.md)」を参照してください。   
-   バイナリ チェックサムまたはチェックサムを使用した検証では、データ型がサブスクライバー側とパブリッシャー側とで異なる場合には、誤ってエラーを報告することがあります。 これは、次のいずれかの場合に発生する可能性があります。    
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の以前のバージョンのデータ型をマップするスキーマ オプションを明示的に設定している場合。  
    -   マージ パブリケーションのパブリケーションの互換性レベルを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の以前のバージョンに設定し、パブリッシュされたテーブルに、このバージョンに対してマップする必要がある 1 つ以上のデータ型が含まれている場合。    
    -   サブスクリプションを手動で初期化し、サブスクライバーで異なるデータ型を使用している場合。   
-   バイナリ チェックサムおよびチェックサムによる検証は、トランザクション レプリケーションの変換可能なサブスクリプションではサポートされていません。   
-   検証は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーにレプリケートされたデータに対してはサポートされていません。    
-   レプリケーション モニターの手順は、プッシュ サブスクリプションにのみ適用されます。プル サブスクリプションはレプリケーション モニターでは同期できないからです。 ただし、レプリケーション モニターで、サブスクリプションに検証対象のマークを付けたり、プル サブスクリプションの検証結果を表示することはできます。    
-   検証結果には、検証が成功したかどうかが示されますが、失敗した場合、検証に失敗した行は示されません。 パブリッシャーとサブスクライバーのデータを比較するには、 [tablediff Utility](../../tools/tablediff-utility.md)を使用します。 レプリケートされたデータでのこのユーティリティの使用の詳細については、「[Compare Replicated Tables for Differences &#40;Replication Programming&#41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)」 (レプリケートされたテーブルを比較して相違があるかどうかを確認する &#40;レプリケーション プログラミング&#41;) を参照してください。  


## <a name="data-validation-results"></a>データ検証の結果  
 検証が完了すると、ディストリビューション エージェントまたはマージ エージェントは成功または失敗に関するメッセージをログに記録します (レプリケーションでは失敗した行については報告されません)。 これらのメッセージは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、レプリケーション モニター、およびレプリケーション システム テーブルで参照できます。 操作方法に関する上記のトピックは、検証の実行方法と結果を表示する方法を示しています。  
  
 データ検証の問題に対処するために、次の点を検討してください。  
  
-   レプリケーション警告を **[レプリケーション: サブスクライバーでデータ検証の問題が見つかりました]** というレプリケーション警告が通知されるようにします。 詳細については、「[Configure Predefined Replication Alerts &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md)」 (定義済みのレプリケーションの警告の構成 &#40;SQL Server Management Studio&#41;) を参照してください。  
  
-   検証の失敗はアプリケーションにとって問題となりますか? 検証の失敗が問題となる場合、データを手動で更新して同期するか、サブスクリプションを再初期化してください。  
  
    -   データを更新するには [tablediff ユーティリティ](../../tools/tablediff-utility.md)を使用します。 このユーティリティの使用方法の詳細については、「[Compare Replicated Tables for Differences &#40;Replication Programming&#41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)」 (レプリケートされたテーブルを比較して相違があるかどうかを確認する &#40;レプリケーション プログラミング&#41;) を参照してください。  
  
    -   再初期化の詳細については、「[Reinitialize Subscriptions](../../relational-databases/replication/reinitialize-subscriptions.md)」 (サブスクリプションの再初期化) を参照してください。  

  
  
## <a name="articles-in-transactional-replication"></a>トランザクション レプリケーションのアーティクル 

### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio の使用
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。    
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。    
3.  サブスクリプションを検証するパブリケーションを右クリックし、 **[サブスクリプションの検証]** をクリックします。    
4.  **[サブスクリプションの検証]** ダイアログ ボックスで、次のように検証するサブスクリプションを選択します。   
    -   **[すべての SQL Server サブスクリプションを検証する]** を選択する。    
    -   **[以下のサブスクリプションを検証する]** を選択し、1 つ以上のサブスクリプションを選択する。    
5.  実行する検証の種類 (行数、または行数とチェックサム) を指定するには、 **[検証オプション]** をクリックし、 **[サブスクリプションの検証オプション]** ダイアログ ボックスでオプションを指定します。  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]   
7.  レプリケーション モニターまたは **[同期の状態の表示]** ダイアログ ボックスで検証結果を表示します。 サブスクリプションごとに、次の手順を実行します。   
    1.  パブリケーションを展開し、サブスクリプションを右クリックして、 **[同期の状態の表示]** をクリックします。    
    2.  エージェントが実行されていない場合は、 **[同期の状態の表示]** ダイアログ ボックスの **[開始]** をクリックします。 ダイアログ ボックスには、検証に関する情報メッセージが表示されます。    
     検証に関するメッセージが表示されない場合、エージェントは既にその後のメッセージを記録しています。 この場合は、検証結果をレプリケーション モニターに表示します。 詳細については、このトピックのレプリケーション モニターの実行手順を参照してください。  

### <a name="using-transact-sql"></a>Transact-SQL の使用

#### <a name="all-articles"></a>すべてのアーティクル 
  
1.  パブリッシャー側のパブリケーション データベースに対して [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md) を実行します。 `@publication` を指定し、`@rowcount_only` には次のいずれかの値を指定します。  
  
    -   **1** - 行数チェックのみ (既定値)    
    -   **2** - 行数とバイナリ チェックサム  
  
    > [!NOTE]  
    >  [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md) を実行する場合、[sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) がパブリケーション内の各アーティクルに対して実行されます。 [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md) を正常に実行するためには、パブリッシュされたベース テーブルのすべての列に対して SELECT 権限が必要です。    
2.  (省略可) ディストリビューション エージェントがまだ実行されていない場合は、各サブスクリプションについてディストリビューション エージェントを開始します。 詳細については、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 」および「 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)」を参照してください。    
3.  エージェントの出力で検証結果を確認します。 
  
#### <a name="single-article"></a>単一のアーティクル  
  
1.  パブリッシャー側のパブリケーション データベースに対して [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) を実行します。 `@publication` を指定し、`@article` にはアーティクルの名前、`@rowcount_only` には次のいずれかの値を指定します。  
  
    -   **1** - 行数チェックのみ (既定値)    
    -   **2** - 行数とバイナリ チェックサム  
  
    > [!NOTE]  
    >  [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) を正常に実行するためには、パブリッシュされたベース テーブルのすべての列に対して SELECT 権限が必要です。  
  
2.  (省略可) ディストリビューション エージェントがまだ実行されていない場合は、各サブスクリプションについてディストリビューション エージェントを開始します。 詳細については、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 」および「 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)」を参照してください。    
3.  エージェントの出力で検証結果を確認します。
  
#### <a name="single-subscriber"></a>単一のサブスクライバー 
  
1.  パブリッシャーのパブリケーション データベースで、[BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md) を使用して明示的なトランザクションを開始します。    
2.  パブリッシャー側のパブリケーション データベースに対して、[sp_marksubscriptionvalidation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md) を実行します。 `@publication` にはパブリケーション、`@subscriber` にはサブスクライバーの名前、`@destination_db` にはサブスクリプション データベースの名前を指定します。    
3.  (省略可) 検証の対象となる各サブスクリプションについて、手順 2. を繰り返します。    
4.  パブリッシャー側のパブリケーション データベースに対して [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) を実行します。 `@publication` を指定し、`@article` にはアーティクルの名前、`@rowcount_only` には次のいずれかの値を指定します。    
    -   **1** - 行数チェックのみ (既定値)    
    -   **2** - 行数とバイナリ チェックサム  
  
    > [!NOTE]  
    >  [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) を正常に実行するためには、パブリッシュされたベース テーブルのすべての列に対して SELECT 権限が必要です。  
  
5.  パブリッシャー側のパブリケーション データベースに対して、[COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md) を使用してトランザクションをコミットします。    
6.  (省略可) 検証の対象となる各アーティクルについて、手順 1. から手順 5. を繰り返します。   
7.  (省略可) ディストリビューション エージェントがまだ実行されていない場合は、開始します。 詳細については、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 」および「 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)」を参照してください。    
8.  エージェントの出力で検証結果を確認します。 詳しくは、「 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)」をご覧ください。  

## <a name="all-push-subscriptions-to-a-transactional-publication"></a>トランザクション パブリケーションのすべてのプッシュ サブスクリプション 

### <a name="using-replication-monitor"></a>レプリケーション モニターの使用
  
1.  レプリケーション モニターの左ペインでパブリッシャー グループを展開し、パブリッシャーを展開します。   
2.  サブスクリプションを検証するパブリケーションを右クリックし、 **[サブスクリプションの検証]** をクリックします。   
3.  **[サブスクリプションの検証]** ダイアログ ボックスで、次のように検証するサブスクリプションを選択します。  
  
    -   **[すべての SQL Server サブスクリプションを検証する]** を選択する。    
    -   **[以下のサブスクリプションを検証する]** を選択し、1 つ以上のサブスクリプションを選択する。    
4.  実行する検証の種類 (行数、または行数とチェックサム) を指定するには、 **[検証オプション]** をクリックし、 **[サブスクリプションの検証オプション]** ダイアログ ボックスでオプションを指定します。    
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]    
6.  **[すべてのサブスクリプション]** タブをクリックします。  
7.  検証結果を表示します。 プッシュ サブスクリプションごとに、次の手順を実行します。    
    1.  エージェントが実行されていない場合、サブスクリプションを右クリックし、 **[同期の開始]** をクリックします。    
    2.  サブスクリプションを右クリックし、 **[詳細表示]** をクリックします。   
    3.  **[ディストリビューターからサブスクライバーまでの履歴]** タブの **[選択されたセッションのアクション]** テキスト領域に情報が表示されます。  
  
## <a name="for-a-single-subscription-to-a-merge-publication"></a>マージ パブリケーションの単一のサブスクリプション

### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio の使用
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。    
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。   
3.  サブスクリプションを検証するパブリケーションを展開し、サブスクリプションを右クリックして、 **[サブスクリプションの検証]** をクリックします。    
4.  **[サブスクリプションの検証]** ダイアログ ボックスで、 **[このサブスクリプションを検証する]** を選択します。    
5.  実行する検証の種類 (行数、または行数とチェックサム) を指定するには、 **[オプション]** をクリックし、 **[サブスクリプションの検証オプション]** ダイアログ ボックスでオプションを指定します。    
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]    
7.  レプリケーション モニターまたは **[同期の状態の表示]** ダイアログ ボックスで検証結果を表示します。  
  
    1.  パブリケーションを展開し、サブスクリプションを右クリックして、 **[同期の状態の表示]** をクリックします。    
    2.  エージェントが実行されていない場合は、 **[同期の状態の表示]** ダイアログ ボックスの **[開始]** をクリックします。 ダイアログ ボックスには、検証に関する情報メッセージが表示されます。  
  
     検証に関するメッセージが表示されない場合、エージェントは既にその後のメッセージを記録しています。 この場合は、検証結果をレプリケーション モニターに表示します。 詳細については、このトピックのレプリケーション モニターの実行手順を参照してください。  
  
## <a name="for-all-subscriptions-to-a-merge-publication"></a>マージ パブリケーションのすべてのサブスクリプション

### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio の使用  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。    
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。   
3.  サブスクリプションを検証するパブリケーションを右クリックし、 **[すべてのサブスクリプションの検証]** をクリックします。    
4.  **[すべてのサブスクリプションの検証]** ダイアログ ボックスで、実行する検証の種類 (行数、または行数とチェックサム) を指定します。   
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]    
6.  レプリケーション モニターまたは **[同期の状態の表示]** ダイアログ ボックスで検証結果を表示します。 サブスクリプションごとに、次の手順を実行します。    
    1.  パブリケーションを展開し、サブスクリプションを右クリックして、 **[同期の状態の表示]** をクリックします。    
    2.  エージェントが実行されていない場合は、 **[同期の状態の表示]** ダイアログ ボックスの **[開始]** をクリックします。 ダイアログ ボックスには、検証に関する情報メッセージが表示されます。  
  
     検証に関するメッセージが表示されない場合、エージェントは既にその後のメッセージを記録しています。 この場合は、検証結果をレプリケーション モニターに表示します。 詳細については、このトピックのレプリケーション モニターの実行手順を参照してください。  
  
 
## <a name="for-a-single-push-subscription-to-a-merge-publication"></a>マージ パブリケーションの単一のプッシュ サブスクリプション 

### <a name="using-replication-monitor"></a>レプリケーション モニターの使用  
1.  レプリケーション モニターで、左ペインのパブリッシャー グループを展開し、パブリッシャーを展開してパブリケーションをクリックします。    
2.  **[すべてのサブスクリプション]** タブをクリックします。    
3.  検証するサブスクリプションを右クリックし、 **[サブスクリプションの検証]** をクリックします。    
4.  **[サブスクリプションの検証]** ダイアログ ボックスで、 **[このサブスクリプションを検証する]** を選択します。    
5.  実行する検証の種類 (行数、または行数とチェックサム) を指定するには、 **[オプション]** をクリックし、 **[サブスクリプションの検証オプション]** ダイアログ ボックスでオプションを指定します。    
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]    
7.  **[すべてのサブスクリプション]** タブをクリックします。    
8.  検証結果を表示します。    
    1.  エージェントが実行されていない場合、サブスクリプションを右クリックし、 **[同期の開始]** をクリックします。    
    2.  サブスクリプションを右クリックし、 **[詳細表示]** をクリックします。    
    3.  **[同期の履歴]** タブの **[選択されたセッションの最終メッセージ]** テキスト領域に情報が表示されます。  

### <a name="using-transact-sql"></a>Transact-SQL の使用
1.  パブリッシャー側のパブリケーション データベースに対して、[sp_validatemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql.md) を実行します。 `@publication` を指定し、`@subscriber` にはサブスクライバーの名前、`@subscriber_db` にはサブスクリプション データベースの名前、`@level` には次のいずれかの値を指定します。   
    -   **1** - 行数の検証のみ    
    -   **3** - 行数とバイナリ チェックサムの検証  
  
     これにより、選択されたサブスクリプションが検証対象としてマークされます。  
  
2.  各サブスクリプションのマージ エージェントを開始します。 詳細については、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 」および「 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)」を参照してください。  
3.  エージェントの出力で検証結果を確認します。   
4.  検証の対象となる各サブスクリプションについて、手順 1. から手順 3. を繰り返します。  
  
> [!NOTE]  
>  **Replication Merge Agent** を実行するときに、 [-Validate](../../relational-databases/replication/agents/replication-merge-agent.md)パラメーターを指定することによって、マージ パブリケーションのサブスクリプションについても同期処理の最後に検証を実行できます。  
  
## <a name="for-all-push-subscriptions-to-a-merge-publication"></a>マージ パブリケーションのすべてのプッシュ サブスクリプション
  
### <a name="using-replication-monitor"></a>レプリケーション モニターの使用    
1.  レプリケーション モニターの左ペインでパブリッシャー グループを展開し、パブリッシャーを展開します。    
2.  サブスクリプションを検証するパブリケーションを右クリックし、 **[すべてのサブスクリプションの検証]** をクリックします。    
3.  **[すべてのサブスクリプションの検証]** ダイアログ ボックスで、実行する検証の種類 (行数、または行数とチェックサム) を指定します。    
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]    
5.  **[すべてのサブスクリプション]** タブをクリックします。    
6.  検証結果を表示します。 プッシュ サブスクリプションごとに、次の手順を実行します。    
    1.  エージェントが実行されていない場合、サブスクリプションを右クリックし、 **[同期の開始]** をクリックします。    
    2.  サブスクリプションを右クリックし、 **[詳細表示]** をクリックします。    
    3.  **[同期の履歴]** タブの **[選択されたセッションの最終メッセージ]** テキスト領域に情報が表示されます。 
  
### <a name="using-transact-sql"></a>Transact-SQL の使用
1.  パブリッシャー側のパブリケーション データベースに対して、[sp_validatemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql.md) を実行します。 `@publication` を指定し、`@level` には次のいずれかの値を指定します。    
    -   **1** - 行数の検証のみ   
    -   **3** - 行数とバイナリ チェックサムの検証  
  
     これにより、すべてのサブスクリプションが検証対象としてマークされます。   
2.  各サブスクリプションのマージ エージェントを開始します。 詳細については、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 」および「 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)」を参照してください。  
  
3.  エージェントの出力で検証結果を確認します。 詳しくは、「 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)」をご覧ください。  

  
## <a name="validate-data-using-merge-agent-parameters"></a>マージ エージェントのパラメーターを使用したデータの検証  
  
1.  サブスクライバー (プル サブスクリプションの場合) またはディストリビューター (プッシュ サブスクリプションの場合) で、次のいずれかの方法でコマンド プロンプトからマージ エージェントを開始します。   
    -   **-Validate** パラメーターの値に、 **1** (行数) または **3** (行数とバイナリ チェックサム) を指定します。    
    -   **-ProfileName** パラメーターに、 **rowcount validation** または **rowcount and checksum validation** を指定します。  
  
     詳細については、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 」または「 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)」を参照してください。  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 レプリケーションでは、サブスクライバーのデータがパブリッシャーのデータと一致するかどうかを、レプリケーション管理オブジェクト (RMO) を使用してプログラムから検証できます。 使用するオブジェクトは、レプリケーション トポロジの種類によって異なります。 トランザクション レプリケーションでは、パブリケーションのサブスクリプションをすべて検証する必要があります。  
  
> [!NOTE]  
>  例については、このセクションの後半の「 [例 (RMO)](#RMOExample)」を参照してください。  
  
#### <a name="to-validate-data-for-all-articles-in-a-transactional-publication"></a>トランザクション パブリケーションのすべてのアーティクルについてデータを検証するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPublication> クラスのインスタンスを作成します。 パブリケーションの <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> プロパティおよび <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> プロパティを設定します。 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに、手順 1. の接続を設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトの残りのプロパティを取得します。 このメソッドが **false**を返す場合、手順 2. でパブリケーション プロパティを不適切に設定したか、パブリケーションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.TransPublication.ValidatePublication%2A> メソッドを呼び出します。 次のパラメーターを指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationOption>  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationMethod>  
  
    -   検証が終了した後、ディストリビューション エージェントを停止するかどうかを示すブール値  
  
     これにより、アーティクルが検証対象としてマークされます。  
  
5.  まだディストリビューション エージェントを実行していない場合は、ディストリビューション エージェントを起動して、各サブスクリプションを同期します。 詳細については、「 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) 」または「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)」を参照してください。 検証操作の結果は、エージェントの履歴に出力されます。 詳しくは、「 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication.md)」をご覧ください。  
  
#### <a name="to-validate-data-in-all-subscriptions-to-a-merge-publication"></a>マージ パブリケーションのすべてのサブスクリプションについてデータを検証するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを作成します。 パブリケーションの <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> プロパティおよび <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> プロパティを設定します。 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに、手順 1. の接続を設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトの残りのプロパティを取得します。 このメソッドが **false**を返す場合、手順 2. でパブリケーション プロパティを不適切に設定したか、パブリケーションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.MergePublication.ValidatePublication%2A> メソッドを呼び出します。 必要な <xref:Microsoft.SqlServer.Replication.ValidationOption>を指定します。  
  
5.  各サブスクリプションについてマージ エージェントを実行して検証を開始するか、次回予定されているエージェントの実行を待ちます。 詳細については、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 」および「 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)」を参照してください。 検証操作の結果は、エージェントの履歴に出力されます。この履歴は、レプリケーション モニターを使って表示できます。 詳しくは、「 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication.md)」をご覧ください。  
  
#### <a name="to-validate-data-in-a-single-subscription-to-a-merge-publication"></a>マージ パブリケーションの単一のサブスクリプションについてデータを検証するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを作成します。 パブリケーションの <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> プロパティおよび <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> プロパティを設定します。 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに、手順 1. の接続を設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトの残りのプロパティを取得します。 このメソッドが **false**を返す場合、手順 2. でパブリケーション プロパティを不適切に設定したか、パブリケーションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.MergePublication.ValidateSubscription%2A> メソッドを呼び出します。 サブスクライバーの名前、検証対象のサブスクリプション データベース、および、必要な <xref:Microsoft.SqlServer.Replication.ValidationOption>を指定します。  
  
5.  目的のサブスクリプションについてマージ エージェントを実行して検証を開始するか、次回予定されているエージェントの実行を待ちます。 詳細については、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 」および「 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)」を参照してください。 検証操作の結果は、エージェントの履歴に出力されます。この履歴は、レプリケーション モニターを使って表示できます。 詳しくは、「 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication.md)」をご覧ください。  
  
###  <a name="RMOExample"></a> 例 (RMO)  
 次の例では、トランザクション パブリケーションのすべてのサブスクリプションを、行数検証の対象としてマークします。  
  
 [!code-cs[HowTo#rmo_ValidateTranPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatetranpub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateTranPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatetranpub)]  
  
 次の例では、マージ パブリケーションの特定のサブスクリプションを、行数検証の対象としてマークします。  
  
 [!code-cs[HowTo#rmo_ValidateMergeSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatemergesub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateMergeSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatemergesub)]  
  
 ## <a name="see-also"></a>参照  
[Best Practices for Replication Administration](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  
