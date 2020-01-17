---
title: 競合の高度な検出と解決 (マージ)
description: マージ レプリケーションを使用した、競合の検出と解決の高度な方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], about conflict resolution
- default conflict resolver
- column-level conflict tracking
- row-level conflict tracking
- viewing merge replication conflicts
- resolving merge replication conflicts
- logical record-level conflict tracking [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 063d3d9c-ccb5-4fab-9d0c-c675997428b4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f90625c1aa123cf72b93ce815b02cccd7cedc78a
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321602"
---
# <a name="advanced-merge-replication---conflict-detection-and-resolution"></a>マージ レプリケーションの詳細 - 競合の検出および解決
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  パブリッシャーとサブスクライバーが接続され、同期が発生すると、マージ エージェントによって競合の検出が行われます。 競合が検出された場合、マージ エージェントは競合回避モジュール (アーティクルをパブリケーションに追加するときに指定) を使用して、他のサイトに反映する許容データを決定します。  

 マージ レプリケーションでは、競合を検出して解決するためのさまざまなメソッドが用意されています。 ほとんどのアプリケーションの場合、次の既定のメソッドが適切です。  
  
-   競合がパブリッシャーとサブスクライバーの間で発生した場合、パブリッシャーの変更は保存され、サブスクライバーの変更は破棄されます。   
-   クライアント サブスクリプション (プル サブスクリプションの既定の種類) を使用している 2 つのサブスクライバー間で競合が発生した場合は、パブリッシャーと同期する最初のサブスクライバーからの変更が保存され、2 番目のサブスクライバーからの変更は破棄されます。 クライアントとサーバーのサブスクリプションの指定の詳細については、「[Specify a Merge Subscription Type and Conflict Resolution Priority (SQL Server Management Studio)](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md)」 (マージ サブスクリプションの種類と競合解決プロパティの指定 (SQL Server Management Studio)) を参照してください。   
-   サーバー サブスクリプション (プッシュ サブスクリプションの既定の種類) を使用している 2 つのサブスクライバー間で競合が発生した場合は、優先度が高い方のサブスクライバーからの変更が保存され、2 番目のサブスクライバーからの変更は破棄されます。 優先度値が同じである場合は、パブリッシャーと同期する最初のサブスクライバーからの変更が保存されます。  
  
> [!NOTE]  
>  サブスクライバーとパブリッシャーの同期が取られていても、異なるサブスクライバーで行われた更新の間に競合が発生する場合があります。これに比べ、サブスクライバーとパブリッシャーにおける更新では、競合はあまり発生しません。  
  
 競合検出および解決の動作は、次のオプションによって異なります。これらのオプションについては、このトピックで解説します。    
-   列レベルの追跡、行レベルの追跡、または論理レコードレベルの追跡のいずれかを指定しているかどうか。    
-   優先度に基づく解決メカニズムを指定しているかどうか、またはアーティクル競合回避モジュールを指定しているかどうか。 アーティクル競合回避モジュールは次のいずれかになります。  
  
    -   マネージド コードで記述された *ビジネス ロジック ハンドラー*   
    -   COM ベースの *カスタム競合回避モジュール*    
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)]によって提供される COM ベースの競合回避モジュール  
  
     既定の解決メカニズムを使用する場合、クライアントまたはサーバーのどちらのサブスクリプションが使用されるかによっても動作が異なります。  
  
## <a name="conflict-detection"></a>競合検出  
 データの変更が競合と見なされるかどうかは、アーティクルに対して設定した競合の追跡の種類によって異なります。  
  
-   列レベルの追跡を選択している場合、複数のレプリケーション ノードで行われた同一行の同一列に対する変更が競合と見なされます。    
-   行レベルの追跡を選択している場合、複数のレプリケーション ノードで行われた同一行の任意の列に対する変更が競合と見なされます (該当する行で影響を受ける列が同一である必要はありません)。    
-   論理レコードレベルの追跡を選択している場合、複数のレプリケーション ノードで行われた同一論理レコードの任意の行に対する変更が競合と見なされます (該当する行で影響を受ける列が同一である必要はありません)。  
  
 詳しくは、「 [論理レコードの競合の検出および解決](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)」をご覧ください。  
  
 アーティクルに対して競合の追跡と競合解決のレベルを指定するには、「[マージ レプリケーションのプロパティの指定](../../../relational-databases/replication/merge/specify-merge-replication-properties.md)」をご覧ください。  
  
## <a name="conflict-resolution"></a>競合解決  
 競合が検出されると、選択した競合回避モジュールがマージ エージェントによって起動され、この競合回避モジュールを使用して、競合で優先するデータを決定します。 競合で優先された行がパブリッシャーおよびサブスクライバーで適用され、優先されなかった行のデータは競合テーブルに書き込まれます。 対話型操作による競合解決を選択しなかった場合、競合はモジュールの実行直後に解決されます。  

マージ レプリケーションの競合の解決  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]  
  パブリッシャーとサブスクライバーが接続され、同期が発生すると、マージ エージェントによって競合の検出が行われます。 競合が検出された場合、マージ エージェントは競合回避モジュールを使用して、どのデータを受け入れて他のサイトに反映するかを決定します。  
  
> [!NOTE]  
>  サブスクライバーがパブリッシャーと同期している場合でも、サブスクライバーとパブリッシャーでの更新よりも、別のサブスクライバーの更新で競合が発生することがよくあります。  
  
 マージ レプリケーションでは、競合を検出して解決するためのさまざまなメソッドが用意されています。 ほとんどのアプリケーションの場合、次の既定のメソッドが適切です。  
  
-   競合がパブリッシャーとサブスクライバーの間で発生した場合、パブリッシャーの変更は保存され、サブスクライバーの変更は破棄されます。  
  
-   クライアント サブスクリプション (プル サブスクリプションの既定の種類) を使用している 2 つのサブスクライバー間で競合が発生した場合は、パブリッシャーと同期する最初のサブスクライバーからの変更が保存され、2 番目のサブスクライバーからの変更は破棄されます。 クライアントとサーバーのサブスクリプションの指定の詳細については、「[Specify a Merge Subscription Type and Conflict Resolution Priority (SQL Server Management Studio)](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md)」 (マージ サブスクリプションの種類と競合解決プロパティの指定 (SQL Server Management Studio)) を参照してください。  
  
-   サーバー サブスクリプション (プッシュ サブスクリプションの既定の種類) を使用している 2 つのサブスクライバー間で競合が発生した場合は、優先度が高い方のサブスクライバーからの変更が保存され、2 番目のサブスクライバーからの変更は破棄されます。 優先度値が同じである場合は、パブリッシャーと同期する最初のサブスクライバーからの変更が保存されます。  
  
 マージ レプリケーションにおける競合の検出と解決の詳細については、「 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)」を参照してください。  
  
### <a name="resolver-types"></a>競合回避モジュールの種類  
 マージ レプリケーションでは、アーティクル レベルで競合解決が行われます。 複数のアーティクルで構成されているパブリケーションの場合、複数の競合回避モジュールで各アーティクルに対応するか、1 つの競合回避モジュールで 1 つのアーティクル、複数のアーティクル、またはパブリケーションを構成するすべてのアーティクルに対応できます。  
  
 既定の優先度に基づく競合回避モジュールを使用する場合、アーティクルに対して競合回避モジュール プロパティを設定する必要はありません。 既定の競合回避モジュールではなくアーティクル競合回避モジュールを使用する場合、パブリッシャーで使用できる競合回避モジュールを選択し、アーティクルに対して競合回避モジュールのプロパティを設定する必要があります。 競合回避モジュールに渡す必要がある特定の情報を、競合回避モジュール情報のプロパティに指定することもできます。  
  
 マージ レプリケーションでは、次に示す 4 つの競合回避モジュールを使用できます。  
  
-   既定の優先度に基づく競合回避モジュール  
  
     既定の解決メカニズムの動作は、クライアント サブスクリプションまたはサーバー サブスクリプションのどちらが使用されているかによって異なります。 サーバー サブスクリプションを使用する個々のサブスクライバーに優先度値を割り当てると、最も優先度の高いノードで行われた変更が競合で最優先されます。 クライアント サブスクリプションの場合は、パブリッシャーに書き込まれた最初の変更が優先されます。  
  
     サブスクリプションの作成後にその種類を変更することはできません。  
  
-   ビジネス ロジック ハンドラー  
  
     ビジネス ロジック ハンドラー フレームワークを使用すると、マネージド コードのアセンブリを記述して、マージ同期処理中に呼び出すことができます。 このアセンブリには、競合など同期中に発生するさまざまな状況に対処するためのビジネス ロジックを記述できます。 詳細については、「[Execute Business Logic During Merge Synchronization](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)」(マージ同期中のビジネス ロジックの実行) をご覧ください。  
  
-   COM ベースのカスタム競合回避モジュール  
  
     マージ レプリケーションには、競合回避モジュールを COM オブジェクトとして作成するための API が用意されています。この COM オブジェクトは、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vcprvc](../../../includes/vcprvc-md.md)] や [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] などの言語で記述します。 詳細については、「 [COM-Based Custom Resolvers](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)」を参照してください。  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)]  
  
     [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、COM ベースの競合回避モジュールが各種用意されています。 詳細については、「 [Microsoft COM ベースの競合回避モジュール](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)」を参照してください。  
  
 適切な競合回避モジュールの種類の選択方法は、「[競合回避モジュールの選択](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-choose-a-resolver.md)」を参照してください。  
  
> [!NOTE]  
>  アーティクル競合回避モジュールの中には、特定の操作が行われた場合のみ競合を処理するように作成されているものもあります。 たとえば、更新については処理するが、挿入や削除については処理しない競合回避モジュールがあります。 既定の優先度に基づく競合回避モジュールでは、アーティクル競合回避モジュールで処理されない競合が処理されます。  
  
 マージ サブスクリプションの種類と競合解決の優先度を指定するには、「  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]:[マージ サブスクリプションの種類と競合解決の優先度の指定 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md)  
  
-   レプリケーション [!INCLUDE[tsql](../../../includes/tsql-md.md)] プログラミングおよびレプリケーション管理オブジェクト (RMO) プログラミング:「[プル サブスクリプションの作成](../../../relational-databases/replication/create-a-pull-subscription.md)」と「[プッシュ サブスクリプションの作成](../../../relational-databases/replication/create-a-push-subscription.md)」  
  
### <a name="interactive-resolver"></a>インタラクティブ競合回避モジュール  
 レプリケーションにはインタラクティブ競合回避モジュールのユーザー インターフェイスが用意されており、既定の優先度に基づく競合回避モジュールやアーティクル競合回避モジュールと併用できます。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 同期マネージャーを使用して要求時同期を実行すると、インタラクティブ競合回避モジュールに実行時の競合データが表示され、競合の解決方法を選択できます。 対話型解決を有効にする方法およびインタラクティブ競合回避モジュールの起動方法の詳細については、「 [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)」を参照してください。  
  
## <a name="viewing-conflicts"></a>競合の表示  
 競合を表示する最も簡単な方法はレプリケーション競合表示モジュールを使用することです。このモジュールは [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] から使用できます ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、競合テーブルに対してクエリを実行するためのストアド プロシージャも用意されています)。 競合表示モジュールはインタラクティブ競合回避モジュールに似たツールです。ただし、インタラクティブ競合回避モジュールが同期実行時の競合の解決に使用されるのに対し、競合表示モジュールは解決後の競合の表示を目的として設計されています。 競合メタデータがシステム テーブルでまだ利用可能な場合 (競合メタデータの既定の保持期間は 14 日間)、競合表示モジュールを使用して競合の解決結果をオーバーライドできます。ただし、直接的な介入が定期的に必要となる場合は、インタラクティブ競合回避モジュールの使用を検討してください。  
  
> [!NOTE]  
>  論理レコードに関連する競合は、競合表示モジュールに表示されません。 これらの競合に関する情報を表示するには、レプリケーション ストアド プロシージャを使用します。 詳細については、「[マージ パブリケーションの競合情報の表示 (レプリケーション Transact-SQL プログラミング)](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)」を参照してください。  
  
 競合表示モジュールには、次に示す 3 つのシステム テーブルの情報が表示されます。  
  
-   レプリケーションは、マージ アーティクルの各テーブルに対して競合テーブルを作成し、そのテーブルに **MSmerge_conflict_\<PublicationName>_\<ArticleName>** という形式の名前を付けます。  
  
     競合テーブルには、基になるテーブルと同じ構造があります。 これらのテーブルの行は競合で優先されなかった行で構成されています (競合で優先された行は実際のユーザー テーブルにあります)。  
  
-   **MSmerge_conflicts_info** テーブルは、競合の種類など各競合に関する情報を提供します。  
  
-   **sysmergearticles** テーブルは、競合テーブルを持つユーザー テーブルを示し、競合テーブルに関する情報を提供します。  
  
 競合情報の既定の保存先は次のとおりです。  
  
-   パブリケーションの互換性レベルが 90 RTM 以上の場合は、パブリッシャーおよびサブスクライバーに保存されます。  
  
-   パブリケーションの互換性レベルが 80 RTM 未満の場合は、パブリッシャーに保存されます。  
  
-   サブスクライバーが [!INCLUDE[ssEW](../../../includes/ssew-md.md)]を実行している場合は、パブリッシャーに保存されます。 競合データを [!INCLUDE[ssEW](../../../includes/ssew-md.md)] サブスクライバーに保存することはできません。  
  
 **競合を表示するには**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]:[マージ パブリケーションでのデータの競合の表示および解決 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   レプリケーション [!INCLUDE[tsql](../../../includes/tsql-md.md)] プログラミング:[マージ パブリケーションの競合情報の表示 (レプリケーション Transact-SQL プログラミング)](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)  
  
## <a name="see-also"></a>参照  
 [データの同期](../../../relational-databases/replication/synchronize-data.md)  
  
  
