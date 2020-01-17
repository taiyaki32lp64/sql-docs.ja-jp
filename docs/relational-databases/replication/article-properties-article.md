---
title: アーティクルのプロパティ - &lt;Article&gt; | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.articleproperties.f1
helpviewer_keywords:
- Article Properties dialog box
ms.assetid: 6dd601a4-1233-43d9-a9f0-bc8d84e5d188
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 081802afb9f66380da93f46bf75011b0f4ddb811
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768200"
---
# <a name="article-properties---ltarticlegt"></a>アーティクルのプロパティ - &lt;Article&gt;
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[アーティクルのプロパティ]** ダイアログ ボックスは、パブリケーションの新規作成ウィザードおよび **[パブリケーションのプロパティ]** ダイアログ ボックスから開くことができます。 このダイアログ ボックスでは、すべての種類のアーティクルのプロパティを表示し、設定できます。 パブリケーションを作成するときにのみ設定できるプロパティや、パブリケーションにアクティブなサブスクリプションがない場合にのみ設定できるプロパティがあります。 設定できないプロパティは読み取り専用として表示されます。  
  
> [!NOTE]  
>  パブリケーションの作成後、プロパティの変更によっては新しいスナップショットが必要となります。 パブリケーションにサブスクリプションが含まれている場合、変更によっては、すべてのサブスクリプションを再初期化する必要もあります。 詳細については、「[Change Publication and Article Properties](../../relational-databases/replication/publish/change-publication-and-article-properties.md)」 (パブリケーションおよびアーティクルのプロパティの変更) を参照してください。  
  
 **[アーティクルのプロパティ]** ダイアログ ボックスの各プロパティには、説明が表示されます。 プロパティをクリックすると、その説明がダイアログ ボックスの下部に表示されます。 このトピックでは、いくつかのプロパティについて追加情報を示します。 プロパティは次のように分類されます。  
  
-   すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パブリケーションに適用されるプロパティ。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からのトランザクション パブリケーションに適用されるプロパティ。  
  
-   マージ パブリケーションに適用されるプロパティ。  
  
-   Oracle パブリッシャーからのトランザクション パブリケーションとスナップショット パブリケーションに適用されるプロパティ。  
  
## <a name="options-for-all-publications"></a>すべてのパブリケーションのオプション  
 **[テーブル分割構成のコピー]** と **[インデックス分割構成のコピー]**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] では、テーブル分割とインデックス分割の機能が導入されました。これは、レプリケーションによって行フィルターと列フィルターを使用して実現される分割とは関係ありません。 **[テーブル分割構成のコピー]** オプションと **[インデックス分割構成のコピー]** オプションでは、パーティション分割構成をサブスクライバーにコピーするかどうかを指定します。 パーティション分割の詳細については、「 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)」を参照してください。  
  
 **[データ型の変換]**  
 サブスクライバーにオブジェクトを作成する際に、ユーザー定義のデータ型を基本データ型に変換するかどうかを指定します。 ユーザー定義のデータ型には、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]で導入されたユーザー定義 CLR 型が含まれます。 このようなデータ型を古いバージョンの **にレプリケートする場合には、** [True] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を指定します。これにより、このデータ型をサブスクライバーで適切に処理できるようになります。  
  
 **[サブスクライバーでスキーマを作成]**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で導入されたスキーマは、CREATE SCHEMA ステートメントを使用して定義します。 スキーマとは、オブジェクトの所有者です。スキーマは、\<Database>.\<Schema>.\<Object> など、マルチパート名で使用されます。 DBO 以外のスキーマで所有されるデータベースにオブジェクトがある場合、パブリッシュされるオブジェクトが作成されるように、このようなスキーマをサブスクライバーに作成することができます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] より古いバージョンの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]にデータをレプリケートする場合、次の手順に従います。  
  
-   古いバージョンでは CREATE SCHEMA がサポートされないため、このオプションを **[False]** に設定します。  
  
-   各スキーマについて、そのスキーマと同じ名前を持つユーザーをサブスクリプション データベースに追加します。  
  
 **[XML を NTEXT に変換]** 、 **[MAX データ型を NTEXT と IMAGE に変換]** 、 **[新しい datetime を NVARCHAR に変換]** 、 **[FILESTREAM を MAX データ型に変換]** 、 **[大きな CLR を MAX データ型に変換]** 、 **[hierarchyId を MAX データ型に変換]** 、および **[spatial を MAX データ型に変換]**  
 名前に示されているようにデータ型と属性を変換するかどうかを指定します。 このようなデータ型を以前のバージョンの **にレプリケートする場合には、** [True] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を指定します。 これにより、このデータ型をサブスクライバーで適切に処理できるようになります。  
  
 **[対象オブジェクト名]**  
 サブスクリプション データベースに作成されるオブジェクトの名前です。 ピア ツー ピア トランザクション レプリケーションが有効なパブリケーションでは、アーティクルに関するこのオプションは変更できません。  
  
 **対象オブジェクトの所有者**  
 サブスクリプション データベースにオブジェクトを作成する際に使用されるスキーマです。 既定では、パブリケーション データベースでオブジェクトが属しているスキーマになりますが、次の例外があります。  
  
-   互換性レベルが 90 未満のマージ パブリケーションのアーティクルの場合。既定では、所有者名は空白のままなり、サブスクライバーにオブジェクトを作成する際に **dbo** と指定されます。  
  
-   Oracle パブリケーションのアーティクルの場合。既定では、所有者名が **dbo**と指定されます。  
  
-   キャラクター モードのスナップショット ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のバージョンのサブスクライバーや [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバーで使用されます) を使用するパブリケーションのアーティクルの場合。既定では、所有者は空白のままになります。 既定の所有者は、サブスクライバーに接続しているディストリビューション エージェントまたはマージ エージェントで使用されるアカウントに関連付けられている所有者になります。  
  
 ピア ツー ピア トランザクション レプリケーションが有効なパブリケーションでは、アーティクルに関するこのオプションは変更できません。  
  
 **[ID 範囲を自動的に管理します]**  
 既定で、パブリッシャーおよび各サブスクライバーの ID 列はすべてレプリケーションによって管理されます。 特定の ID 値が 1 つのノードでのみ使用されるように、各レプリケーション ノードには幅広い ID 値 ( **[パブリッシャーの範囲サイズ]** および **[サブスクライバーの範囲サイズ]** で指定) が割り当てられています。 詳細については、「[ID 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)」を参照してください。  
  
## <a name="options-for-transactional-publications"></a>トランザクション パブリケーションのオプション  
 **[INSERT、UPDATE、DELETE ストアド プロシージャのコピー]**  
 このダイアログ ボックスの **[ステートメントの配信]** セクションで、ストアド プロシージャを使用して変更をサブスクライバーに伝達するように指定した場合 (既定)、そのプロシージャを各サブスクライバーにコピーするかどうかを選択します。 **[False]** を選択した場合、プロシージャを手作業でコピーしなければ、ディストリビューション エージェントが変更を伝達しようとしても失敗します。  
  
 **Statement delivery**  
 このセクションのオプションは、テーブルとしてレプリケートされるインデックス付きビューを含め、すべてのテーブルに適用されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、アプリケーションで別の機能が必要にならない限り、既定のオプションを使用することをお勧めします。 既定では、トランザクション レプリケーションが、各サブスクライバーにインストールされているストアド プロシージャのセットを使用して、変更をサブスクライバーに伝達します。 パブリッシャー上のテーブルに対して挿入、更新、または削除が実行されると、その操作はサブスクライバー上のストアド プロシージャに対する呼び出しに変換されます。  
  
 **[ステートメントの配信]** オプションでは、ストアド プロシージャを使用するかどうか、そして使用する場合にはプロシージャに渡されるパラメーターの形式を指定します。 **[ストアド プロシージャ]** オプションでは、レプリケーションによって自動的に作成されるプロシージャか、自分で作成した代用のカスタム プロシージャを使用できます。  
  
 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
 **[レプリケート]**  
 このオプションは、ストアド プロシージャにのみ適用されます。 ストアド プロシージャの定義 (CREATE PROCEDURE ステートメント) またはその実行をレプリケートするかどうかを指定します。 プロシージャの実行をレプリケートする場合、サブスクリプションが開始されたときにプロシージャの定義がサブスクライバーにレプリケートされます。プロシージャがパブリッシャー上で実行されると、サブスクライバー上の対応するプロシージャが実行されます。 これにより、大規模なバッチ操作を実行する場合のパフォーマンスが大幅に向上します。 詳細については、「 [Publishing Stored Procedure Execution in Transactional Replication](../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)」を参照してください。  
  
## <a name="options-for-merge-publications"></a>マージ パブリケーションのオプション  
 マージ パブリケーションの **[アーティクルのプロパティ]** ダイアログ ボックスには、2 つのタブがあります。 **[プロパティ]** と **[競合回避モジュール]** です。  
  
### <a name="properties-tab"></a>[プロパティ] タブ  
 **[同期の方向]**  
 クライアントのサブスクリプション タイプを使用するサブスクライバーから、変更をアップロードできるかどうかを指定します。  
  
-   **[双方向]** (既定) : 変更をサブスクライバーにダウンロードし、パブリッシャーにアップロードすることができます。  
  
-   **[サブスクライバーへのダウンロードのみを実行し、サブスクライバーの変更を禁止する]** : 変更をサブスクライバーにダウンロードできますが、パブリッシャーにアップロードすることはできません。 トリガーにより、サブスクライバーで変更が作成されなくなります。  
  
-   **[サブスクライバーへのダウンロードのみを実行し、サブスクライバーの変更を許可する]** : 変更をサブスクライバーにダウンロードできますが、パブリッシャーにアップロードすることはできません。  
  
 詳細については、「[ダウンロード専用アーティクルを使用したマージ レプリケーションのパフォーマンス最適化](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)」を参照してください。  
  
 **[パーティションのオプション]**  
 パラメーター化されたフィルターで作成されるパーティションの種類を指定します。 詳細については、「 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」の「[パーティションのオプション] の設定」を参照してください。  
  
 **[追跡レベル]**  
 同じ行または同じ列に対する変更を競合として扱うかどうかを指定します。  
  
 **[INSERT 権限の確認]** 、 **[UPDATE 権限の確認]** 、 **[DELETE 権限の確認]**  
 パブリケーション データベースにパブリッシュされたテーブルに対する INSERT 権限、UPDATE 権限、または DELETE 権限がサブスクライバーのログインにあるかどうか、同期中にチェックするかどうかを指定します。 マージ レプリケーションではこのような権限を許可する必要がないため、既定では **[False]** になっています。パブリッシュされたテーブルへのアクセスは、パブリケーション アクセス リスト (PAL) により制御されます。 PAL の詳細については、「[パブリッシャーのセキュリティ保護](../../relational-databases/replication/security/secure-the-publisher.md)」を参照してください。  
  
 パブリッシュされたデータに対する特定の変更だけをアップロードするように 1 つ以上のサブスクライバーに許可する場合、権限をチェックするように要求できます。 たとえば、あるサブスクライバーを PAL に追加しながら、パブリケーション データベース内のテーブルに対する権限をそのサブスクライバーに与えないことができます。 その後で [DELETE 権限の確認] を **[True]** に設定すると、そのサブスクライバーでは挿入と更新のアップロードができますが、削除はできなくなります。  
  
 **[複数列の UPDATE]**  
 マージ レプリケーションによって更新が実行されると、1 つの UPDATE ステートメントですべての列が更新され、変更のない列は元の値にリセットされます。 この操作の代わりに、変更された各列に対して 1 つの UPDATE ステートメントを使用し、複数の UPDATE ステートメントを実行することができます。 一般的に、複数列の UPDATE ステートメントを使用する方が効率的ですが、テーブルのトリガーが特定の列の更新に応答するように設定されており、更新が発生したときに列がリセットされることによって不適切な処理が行われる場合には、このオプションを **[False]** に設定するように検討してください。  
  
> [!IMPORTANT]  
>  このオプションは非推奨とされます。将来のリリースでは廃止される予定です。  
  
### <a name="resolver-tab"></a>[競合回避モジュール] タブ  
 **[既定の競合回避モジュールを使用する]**  
 既定の競合回避モジュールを選択した場合、使用されるサブスクリプションのタイプに応じて、各サブスクライバーに割り当てられている優先度、またはパブリッシャーに書き込まれた最初の変更に基づいて競合が回避されます。 詳細については、「[マージ レプリケーションの競合の検出および解決](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)」を参照してください。  
  
 **[ディストリビューターに登録されたカスタム競合回避モジュールを使用する]**  
 アーティクル競合回避モジュール ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] が提供しているモジュールまたは自作のモジュール) の使用を選択した場合、リスト ボックスから競合回避モジュールを選択する必要があります。 詳細については、「 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)」を参照してください。  
  
 競合回避モジュールに入力が必要な場合、 **[競合回避モジュールが必要とする情報の入力]** テキスト ボックスで指定してください。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] カスタム競合回避モジュールに必要な入力の詳細については、「[Microsoft COM ベースの競合回避モジュール](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)」を参照してください。  
  
 **[要求時同期中にサブスクライバーが対話的に競合を解決することを許可する]**  
 サブスクライバーでオン デマンド同期が使用されるとき (マージ レプリケーションの既定の動作)、競合を対話的に解決する場合に、このオプションを選択します。 オン デマンド同期は、サブスクリプションの新規作成ウィザードの **[同期スケジュール]** ページで指定します。 競合を対話的に解決するには、インタラクティブ競合回避モジュールのユーザー インターフェイスを使用します。 詳細については、「 [Interactive Conflict Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)」を参照してください。  
  
 **[マージ前にデジタル署名の確認を要求する]**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] の提供する COM ベース競合回避モジュールはすべて署名済みです。 このオプションを選択すると、同期の際に競合回避モジュールが有効かどうか確認されます。  
  
## <a name="options-for-oracle-publications"></a>Oracle パブリケーションのオプション  
 Oracle パブリケーションの **[アーティクルのプロパティ]** ダイアログ ボックスには、2 つのタブがあります。 **[プロパティ]** と **[データのマッピング ]** です。 Oracle パブリケーションでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パブリケーションでサポートされるプロパティの一部がサポートされません。 詳細については、「 [Design Considerations and Limitations for Oracle Publishers](../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)」を参照してください。  
  
### <a name="properties-tab"></a>[プロパティ] タブ  
 **[INSERT、UPDATE、DELETE ストアド プロシージャのコピー]**  
 アーティクルがトランザクション パブリケーションに含まれているとき、このダイアログ ボックスの **[ステートメントの配信]** セクションで、ストアド プロシージャを使用して変更をサブスクライバーに伝達するように指定した場合 (既定)、そのプロシージャを各サブスクライバーにコピーするかどうかを選択します。 **[False]** を選択した場合、プロシージャを手作業でコピーしなければ、ディストリビューション エージェントが変更を伝達しようとしても失敗します。  
  
 **対象オブジェクトの所有者**  
 **dbo**以外の値を入力した場合、次の操作が行われます。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以上が動作しているサブスクライバーでは、入力した値と同じ名前のサブスクライバーでスキーマが作成されていることを確認する必要があります。 詳細については、「[CREATE SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/create-schema-transact-sql.md)」を参照してください。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]より前のバージョンが動作しているサブスクライバーでは、各スキーマについて、そのスキーマと同じ名前を持つユーザーをサブスクリプション データベースに追加します。  
  
 **[テーブルスペース名]**  
 レプリケーションの変更の追跡テーブルを作成する、Oracle サーバー インスタンスのテーブルスペースです。 詳細については、「[Manage Oracle Tablespaces](../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md)」 (Oracle テーブルスペースの管理) を参照してください。  
  
 **Statement delivery**  
 このセクションのオプションは、トランザクション パブリケーションのすべてのテーブルに適用されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、アプリケーションで別の機能が必要にならない限り、既定のオプションを使用することをお勧めします。 既定では、トランザクション レプリケーションが、各サブスクライバーにインストールされているストアド プロシージャのセットを使用して、変更をサブスクライバーに伝達します。 パブリッシャー上のテーブルに対して挿入、更新、または削除が実行されると、その操作はサブスクライバー上のストアド プロシージャに対する呼び出しに変換されます。  
  
 **[ステートメントの配信]** オプションでは、ストアド プロシージャを使用するかどうか、そして使用する場合にはプロシージャに渡されるパラメーターの形式を指定します。 **[ストアド プロシージャ]** オプションでは、レプリケーションによって自動的に作成されるプロシージャか、自分で作成した代用のカスタム プロシージャを使用できます。  
  
 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
### <a name="data-mapping-tab"></a>[データのマッピング] タブ  
 **列名**  
 パブリッシャーの列の名前です (読み取り専用)。  
  
 **[パブリッシャーのデータ型]**  
 パブリッシャーの列の Oracle データ型です (読み取り専用)。 このデータ型は、Oracle データベースでのみ直接変更できます。 詳細については Oracle のマニュアルを参照してください。  
  
 **[サブスクライバーのデータ型]**  
 データがレプリケートされるときに Oracle データ型がマップされる、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型です。  
  
-   データ型によっては、可能なマッピングが 1 つしかない場合があります。このような場合、プロパティ グリッドの列は読み取り専用になります。  
  
-   データ型によっては、複数のデータ型を選択できる場合があります。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、アプリケーションに別のマッピングが必要でない限り、既定のマッピングを使うことをお勧めします。 詳細については、「 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [パブリケーション プロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [初期スナップショットの作成および適用](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [サブスクリプションの再初期化](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [データとデータベース オブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
