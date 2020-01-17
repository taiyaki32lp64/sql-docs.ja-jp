---
title: '[パブリケーションのプロパティ]、[サブスクリプション オプション] | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.subscriptionoptions.f1
ms.assetid: 31abd605-b273-419d-86df-d0ecf539a507
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9c630646aa81ebaeccf49f729299394419b7099a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63021701"
---
# <a name="publication-properties-subscription-options"></a>[パブリケーションのプロパティ]、[サブスクリプション オプション]
  **[パブリケーション プロパティ]** ダイアログ ボックスの **[サブスクリプション オプション]** ページを使用すると、サブスクリプションに関連付けられたパブリケーション レベルのプロパティを表示したり設定したりできます。 プロパティは次のように分類されます。  
  
-   すべてのパブリケーションに適用されるプロパティ。  
  
-   スナップショット パブリケーションおよびトランザクション パブリケーション (サブスクリプションの更新を許可するパブリケーションを含む) に適用されるプロパティ。  
  
-   マージ パブリケーションに適用されるプロパティ。  
  
> [!NOTE]  
>  一部のプロパティは読み取り専用です。理由については、このトピックのプロパティの解説で説明します。 プロパティの変更に応じて、新しいスナップショットが必要になる場合や、すべてのサブスクリプションの再初期化が必要になる場合があります。 詳細については、「[Change Publication and Article Properties](publish/change-publication-and-article-properties.md)」 (パブリケーションおよびアーティクルのプロパティの変更) を参照してください。  
  
## <a name="options-for-all-publications"></a>すべてのパブリケーションのオプション  
  
### <a name="creation-and-synchronization"></a>[作成と同期]  
 **[匿名サブスクリプションを許可]**  
 匿名プル サブスクリプションを許可するかどうかを決定します。 匿名サブスクリプションは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEWEd2005](../../includes/ssewed2005-md.md)], [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssMobileEd2005](../../includes/ssmobileed2005-md.md)]、および [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for Windows CE でサポートされています。 このオプションをスナップショット パブリケーションおよびトランザクション パブリケーションに使用するには、 **[スナップショットが常に利用可能]** を **[True]** に設定する必要があります。  
  
 **[アタッチ可能なサブスクリプション データベース]**  
 サブスクリプション データベースのコピーをアタッチすることによって、サブスクリプションを作成できるかどうかを決定します (スナップショット パブリケーションおよびトランザクション パブリケーションに対して **[スナップショットが常に利用可能]** を **[True]** に設定することが必要)。  
  
> [!IMPORTANT]  
>  アタッチ可能なサブスクリプションは、将来のリリースでは使用できません。 この機能は非推奨とされます。  
  
 **[プル サブスクリプションを許可]**  
 サブスクライバーでこのパブリケーションのプル サブスクリプションを作成できるようにするかどうかを決定します。 詳細については、「[パブリケーションのサブスクライブ](subscribe-to-publications.md)」を参照してください。  
  
### <a name="schema-replication"></a>[スキーマ レプリケーション]  
 **[スキーマ変更のレプリケート]**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンのみです。 パブリッシュされたオブジェクトに対して、テーブルへの列の追加や列のデータ型の変更などのスキーマ変更をレプリケートするかどうかを決定します。 詳細については、「[パブリケーション データベースでのスキーマの変更](publish/make-schema-changes-on-publication-databases.md)」を参照してください。  
  
## <a name="options-for-snapshot-and-transactional-publications"></a>スナップショット パブリケーションとトランザクション パブリケーションのオプション  
  
### <a name="creation-and-synchronization"></a>[作成と同期]  
 **[独立したディストリビューション エージェント]**  
 このデータベースの他のパブリケーションから独立したエージェントを使用するかどうかを決定します。 このオプションは読み取り専用であり、パブリケーションの新規作成ウィザードで作成されたパブリケーションに対して既定で **[True]** に設定され、パブリケーション作成後は変更できません。 詳細については、「[Replication Agent Administration](agents/replication-agent-administration.md)」 (レプリケーション エージェントの管理) を参照してください。  
  
 **[スナップショットが常に利用可能]**  
 スナップショット エージェントが実行されるたびにスナップショット ファイルを作成するかどうかを決定します ( **[独立したディストリビューション エージェント]** が有効な場合のみ)。 このオプションは読み取り専用であり、パブリケーションの新規作成ウィザードの **[スナップショット エージェント]** ページで **[スナップショットをすぐに作成し、サブスクリプションを初期化できるようにそのスナップショットを保持する]** を選択した場合は **[True]** に設定されます (既定)。 詳細については、「[スナップショットの作成および適用](create-and-apply-the-snapshot.md)」を参照してください。  
  
 **[バックアップ ファイルからの初期化を許可]**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンのみです。 サブスクリプションの初期化でバックアップ ファイルを使用できるようにするかどうかを決定します。 詳細については、「[スナップショットを使用しないトランザクション サブスクリプションの初期化](initialize-a-transactional-subscription-without-a-snapshot.md)」を参照してください。  
  
 **[SQL Server 以外のサブスクライバーを許可]**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンのみです。 パブリケーションで[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーをサポートするかどうかを決定します。 このオプションを **[True]** にすると、他のパブリケーション プロパティで[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーをサポートするように設定されます。 サブスクリプションが存在する場合、このオプションは読み取り専用です。 **[即時更新サブスクリプションを許可]** 、 **[キュー更新サブスクリプションを許可]** 、または **[ピア ツー ピア サブスクリプションを許可]** が **[True]** に設定されている場合、このオプションは **[True]** に設定できません。 詳細については、「 [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md)」を参照してください。  
  
### <a name="data-transformation"></a>[データの変換]  
 **[データ変換を許可]**  
 データをサブスクライバーに配布する前に、データ変換サービス (DTS) を使用してデータを変換するかどうかを決定します。 このオプションは読み取り専用であり、データの変換を有効にできるのは、ストアド プロシージャを使用してパブリケーションが作成された場合のみです。  
  
> [!IMPORTANT]  
>  変換可能なサブスクリプションは、将来のリリースでは使用できません。 この機能は非推奨とされます。  
  
### <a name="peer-to-peer-replication"></a>[ピア ツー ピア レプリケーション]  
 **[True]**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンにのみ適用されます。 パブリケーションでピア ツー ピア レプリケーションをサポートするかどうかを決定します。 このオプションを **[True]** にすると、他のパブリケーション プロパティでピア ツー ピア レプリケーションをサポートするように設定されます。 サブスクリプションが存在する場合、このオプションは読み取り専用です。 **[即時更新サブスクリプションを許可]** 、 **[キュー更新サブスクリプションを許可]** 、または **[SQL Server 以外のサブスクライバーを許可]** が **[True]** に設定されている場合、このオプションは **[True]** に設定できません。 詳細については、「 [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md)」を参照してください。  
  
 **[ピア ツー ピア競合検出を許可]**  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンにのみ適用されます。 このパブリケーションで競合検出を有効にするかどうかを指定します。 競合検出を使用するには、すべてのノードが [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンを実行しており、すべてのノードで検出が有効になっている必要があります。 競合検出を使用するには、 **[ピア実行者 ID]** の値も指定する必要があります。詳細については、「 [Conflict Detection in Peer-to-Peer Replication](transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」を参照してください。  
  
 **[ピア実行者 ID]**  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンにのみ適用されます。 ピア ツー ピア トポロジ内のノードの ID を指定します。 **[ピア ツー ピア競合検出を許可]** が **[True]** に設定されている場合、この ID は競合検出で使用されます。 トポロジで使用されていないゼロ以外の正の ID を指定してください。 既に使用されている ID を確認するには、 [Mspeer_originatorid_history](/sql/relational-databases/system-tables/mspeer-originatorid-history-transact-sql) システム テーブルに対してクエリを実行します。  
  
### <a name="updatable-subscriptions"></a>[更新可能なサブスクリプション]  
 **[キュー更新サブスクリプションを許可]**  
 サブスクライバーのデータ変更をパブリッシャーに即時にレプリケートできるかどうかを決定します。 このオプションは読み取り専用であり、更新サブスクリプションを有効にできるのは、パブリケーションが作成された場合のみです。 詳細については、「 [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)」を参照してください。  
  
 **[ピア ツー ピア サブスクリプションを許可]**  
 サブスクライバーのデータ変更をキューに登録しておき、後からパブリッシャーにレプリケートできるかどうかを決定します。 このオプションは読み取り専用であり、更新サブスクリプションを有効にできるのは、パブリケーションが作成された場合のみです。 詳細については、「 [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)」を参照してください。  
  
 **[競合を一元的にレポート]**  
 パブリッシャーのみで、またはパブリッシャーとサブスクライバーの両方で、競合するデータ変更をレポートするかどうかを決定します ( **[キュー更新サブスクリプションを許可]** が有効な場合のみ)。 このオプションは読み取り専用であり、パブリケーションの新規作成ウィザードで作成されたパブリケーションに対して既定で **[True]** に設定され、パブリケーション作成後は変更できません。 値 **[True]** は、競合がパブリッシャーでのみレポートされることを示します。 競合は、レポートされた場所でのみ参照できます。  
  
 **[競合の解決方法]**  
 サブスクライバーの変更がパブリッシャーの変更と競合している場合に実行する操作を指定します ( **[キュー更新サブスクリプションを許可]** が有効な場合のみ)。 詳細については、「 [Queued Updating Conflict Detection and Resolution](transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)」を参照してください。  
  
 **[キューの種類]**  
 サブスクライバーでの変更がパブリッシャーに対して適用可能になるまでの間、その変更を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] キューまたは [!INCLUDE[msCoName](../../includes/msconame-md.md)] メッセージ キュー (MSMQ) のどちらを使用してキューに登録するかを決定します ( **[キュー更新サブスクリプションを許可]** が有効な場合のみ)。 このオプションは [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]に対してのみ適用されます。それ以降のバージョンでは、キューイングに常に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルを使用します。  
  
## <a name="options-for-merge-publications"></a>マージ パブリケーションのオプション  
  
### <a name="conflict-reporting"></a>[競合に関するレポートの作成]  
 **[競合を一元的にレポート]**  
 パブリッシャーのみで、またはパブリッシャーとサブスクライバーの両方で、競合するデータ変更をレポートするかどうかを決定します このオプションは読み取り専用であり、パブリケーションの新規作成ウィザードで作成されたパブリケーションに対して既定で **[True]** に設定され、パブリケーション作成後は変更できません。 値 **[True]** は、競合がパブリッシャーでのみレポートされることを示します。 競合は、レポートされた場所でのみ参照できます。 詳細については、「 [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md)」の「競合の表示」を参照してください。  
  
### <a name="filtering"></a>フィルター  
 **[パラメーター化されたフィルターの許可]**  
 パラメーター化されたフィルターを、パブリケーションで使用するかどうかに基づいて設定します。 このオプションは常に読み取り専用です。 詳細については、「 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)」を参照してください。  
  
 **[サブスクライバーの検証]**  
 サブスクライバーで、正しいデータのパーティションが保持されているかどうかを検証する場合に使用する関数を決定します。 複数の値がある場合はコンマで区切ります。 詳細については、「[マージ サブスクライバーのパーティション情報の検証](validate-partition-information-for-a-merge-subscriber.md)」を参照してください。  
  
 **[パーティションの事前計算]**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンのみです。 どのデータがどのパーティションに属しているかを事前に計算することによって、同期を最適化するかどうかを決定します。 この設定は、パブリケーションが事前計算済みパーティションの基準を満たしている場合、既定で **[True]** になっています。 詳細については、「[事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンス最適化](merge/parameterized-filters-optimize-for-precomputed-partitions.md)」を参照してください。  
  
 **[同期の最適化]**  
 各サブスクライバーで追加メタデータを格納することによって、マージ プロセスを最適化するかどうかを決定します。 この最適化よりも事前計算済みパーティションが優先されます。 **[同期の最適化]** オプションは、 **[パーティションの事前計算]** が **[False]** に設定された場合のみ適用されます。 詳しくは、「 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)」をご覧ください。  
  
### <a name="merge-processes"></a>[マージ プロセス]  
 **[同時実行プロセスの制限]**  
 同時に実行できるマージ エージェントの数を制限するかどうかを決定します。 通常は、パブリケーションが持つプッシュ サブスクリプションの中で、同時に同期する可能性のあるものが多い場合に使用されます。  
  
 **[最大同時プロセス数]**  
 同時に実行できるマージ エージェントの最大数です ( **[同時実行プロセスの制限]** が有効な場合のみ)。 同期するエージェントの数が最大数を超えた場合は、数が最大数未満になるまでエージェントはキューに入れられます。  
  
## <a name="see-also"></a>関連項目  
 [Create a Publication](publish/create-a-publication.md)   
 [パブリケーション プロパティの表示および変更](publish/view-and-modify-publication-properties.md)   
 [データとデータベース オブジェクトのパブリッシュ](publish/publish-data-and-database-objects.md)  
  
  
