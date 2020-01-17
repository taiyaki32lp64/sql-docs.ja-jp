---
title: 包含データベース | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- contained database
- database_uncontained_usage event
- partially contained database
- contained database, understanding
ms.assetid: 36af59d7-ce96-4a02-8598-ffdd78cdc948
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e42d7dbfe00ff957511d9853e39febd29b7aab66
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137325"
---
# <a name="contained-databases"></a>包含データベース
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  " *包含データベース* " は、他のデータベース、およびデータベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスから分離されたデータベースです。  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、ユーザーは 4 つの方法でインスタンスからデータベースを分離できます。  
  
-   データベースを表すメタデータの多くはデータベースに保持されます (master データベースのメタデータを保持する代わりに、またはそれに加えて保持されます)。  
  
-   すべてのメタデータは、同じ照合順序を使用して定義されます。  
  
-   ユーザー認証をデータベースで実行して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスのログインに対するデータベースの依存を軽減できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境 (DMV の XEvents など) は、包含情報をレポートおよび操作できます。  
  
 データベースへのメタデータの格納など、部分的包含データベースの一部の機能はすべての [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] データベースに適用されます。 データベース レベル認証やカタログ照合順序など、部分的包含データベースの一部の利点を使用可能にするには、あらかじめこれらを有効にしておく必要があります。 部分的包含は、 **CREATE DATABASE** ステートメントと **ALTER DATABASE** ステートメントを使用するか、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して有効にします。 部分的データベース包含を有効にする方法の詳細については、「 [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)」をご覧ください。  
  
##  <a name="Concepts"></a> 部分的包含データベースの概念  
 完全包含データベースには、すべての設定と、データベースを定義するために必要なメタデータが含まれており、データベースがインストールされている [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに対する構成上の依存関係がありません。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、データベースを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスから分離するのには時間がかかる場合があり、データベースと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス間の関係に関する詳細な知識が必要でした。 部分的包含データベースを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスと他のデータベースからデータベースを簡単に分離できるようになります。  
  
 包含データベースでは、機能を包含という観点から考えます。 データベース内の機能だけに依存しているすべてのユーザー定義エンティティは、完全に包含されていると見なされます。 データベースの外部の機能に依存しているすべてのユーザー定義エンティティは、包含されていないと見なされます (詳細については、後の「 [包含](#containment) 」を参照してください)。  
  
 以下の用語は、包含データベース モデルに適用されます。  
  
 データベース境界  
 データベースと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスとの境界。 データベースと他のデータベースとの境界。  
  
 包含  
 完全にデータベース境界内に存在する要素。  
  
 非包含  
 データベース境界を越える要素。  
  
 非包含データベース  
 包含が **NONE**に設定されているデータベース。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] より前のバージョンのすべてのデータベースは、非包含です。 既定では、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降のすべてのデータベースの包含は **NONE**に設定されています。  
  
 部分的包含データベース  
 部分的包含データベースは、データベース境界を越えることが許可される包含データベースです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、包含の境界をいつ超えるかを判断する機能が含まれています。  
  
 包含ユーザー  
 包含データベースには、2 種類のユーザーがあります。  
  
-   **パスワードを持つ包含データベース ユーザー**  
  
     パスワードを持つ包含データベース ユーザーは、データベースによって認証されます。 詳細については、「 [包含データベース ユーザー - データベースの可搬性を確保する](../../relational-databases/security/contained-database-users-making-your-database-portable.md)」を参照してください。  
  
-   **Windows プリンシパル**  
  
     承認済みの Windows ユーザーと、承認済みの Windows グループのメンバーは、データベースに直接接続でき、 **master** データベース内のログインを必要としません。 データベースは、Windows による認証を信頼します。  
  
 **master** データベースへのログインに基づくユーザーには、包含データベースに対するアクセス許可を付与できますが、それによって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスとの依存関係が生成されます。 そのため、ログインに基づくユーザーを作成するには、部分的包含が必要です。
  
> [!IMPORTANT]  
>  部分的包含データベースを有効にすると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへのアクセス制御がデータベースの所有者にデリゲートされます。 詳しくは、「 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)」をご覧ください。  
  
 データベース境界  
 部分的包含データベースはデータベースの機能をインスタンスの機能から分離するので、これらの 2 つの要素間には " *データベース境界*" と呼ばれる、明確に定義された区分線があります。  
  
 データベース境界の内側は *データベース モデル*で、ここではデータベースが開発および管理されます。 データベース内にあるエンティティの例としては、 **sys.tables**のようなシステム テーブル、パスワードを持つ包含データベース ユーザー、2 部構成の名前で参照されている現在のデータベース内のユーザー テーブルなどがあります。  
  
 データベース境界の外側は " *管理モデル*" で、ここではインスタンスレベルの機能と管理が扱われます。 データベース境界の外にあるエンティティの例としては、 **sys.endpoints**のようなシステム テーブル、ログインにマップされているユーザー、3 部構成の名前で参照されている他のデータベース内のユーザー テーブルなどがあります。  
  
##  <a name="containment"></a> 包含  
 全体がデータベース内に存在しているユーザー エンティティは、 *包含*であると見なされます。 データベースの外部に存在していたり、データベースの外部の機能とのやり取りに依存しているすべてのエンティティは、 *非包含*と見なされます。  
  
 一般に、ユーザー エンティティは、以下の包含のカテゴリのいずれかに分類されます。  
  
-   完全包含ユーザー エンティティ (データベース境界を越えることがないもの)。たとえば、sys.indexes。 これらの機能を使用するコードや、これらのエンティティのみを参照するオブジェクトも完全包含です。  
  
-   非包含ユーザー エンティティ (データベース境界を越えるもの)。たとえば、sys.server_principals やサーバー プリンシパル (ログイン) 自体。 これらのエンティティを使用するコードや、これらのエンティティを参照する機能は包含ではありません。  
  
###  <a name="partial"></a> Partially Contained Database  
 包含データベースの機能は、現在、部分的包含状態のみで利用可能です。 部分的包含データベースは、非包含機能の使用が許される包含データベースです。  
  
 非包含オブジェクトまたは機能に関する情報を取得するには、[sys.dm_db_uncontained_entities](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md) ビューおよび [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) ビューを使用します。 データベースの要素の包含状態を確認することにより、包含を昇格させるためにどのオブジェクトまたは機能を置き換えたり変更したりする必要があるかを判断できます。  
  
> [!IMPORTANT]  
>  一部のオブジェクトでは、既定の包含設定が **NONE**であるため、このビューは偽陽性の結果を返す場合があります。  
  
 部分的包含データベースの動作と非包含データベースの動作の違いが最も明らかなのが、照合順序の場合です。 照合順序の問題の詳細については、「 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)」をご覧ください。  
  
##  <a name="benefits"></a> 部分的包含データベースを使用する利点  
 非包含データベースに関連している問題や複雑さの一部は、部分的包含データベースを使用することで解決できます。  
  
### <a name="database-movement"></a>データベースの移動  
 データベースの移動時に発生する問題の 1 つは、データベースがあるインスタンスから別のインスタンスに移動されたときに、一部の重要情報が使用不能になる場合があることです。 たとえば、ログイン情報がデータベースではなくインスタンスに保存されます。 非包含データベースを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスから別のインスタンスに移動すると、この情報は後に残されます。 欠落情報を特定し、データベースと一緒に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の新しいインスタンスに移動する必要があります。 この処理は、困難で時間がかかる場合があります。  
  
 部分包含データベースには、データベース内の重要情報を格納できるため、移動後もデータベースには情報が含まれます。  
  
> [!NOTE]  
>  部分包含データベースでは、インスタンスから分離できないデータベースで使用される機能を記述するドキュメントを提供できます。 これには、他の相互関連データベースの一覧や、データベースに必要だが含めることのできないシステム設定などが含まれます。  
  
### <a name="benefit-of-contained-database-users-with-always-on"></a>AlwaysOn の包含データベース ユーザーの利点  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスとの結び付きを低減することで、部分的包含データベースは [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]を使用する場合のフェールオーバー時に役立つことがあります。  
  
 包含ユーザーを作成すると、そのユーザーは包含データベースに直接接続できます。 これは、AlwaysOn ソリューションなどの高可用性およびディザスター リカバリーのシナリオにおいて非常に重要な機能です。 ユーザーが包含ユーザーである場合は、フェールオーバーが発生したときに、セカンダリ データベースをホストするインスタンスのログインを作成せずに、セカンダリ データベースに接続できます。 これは直接的な利益をもたらします。 詳細については、「 [Always On 可用性グループの概要 (SQL Server)](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) 」およおび「 [Always On 可用性グループの前提条件、制限事項、推奨事項 (SQL Server)](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」をご覧ください。  
  
### <a name="initial-database-development"></a>初期のデータベース開発  
 開発者は新しいデータベースが配置される場所を把握していない場合があるため、配置先の環境がデータベースに及ぼす影響を少なくすることで、開発者の作業や懸案事項が軽減されます。 非包含モデルでは、開発者は新しいデータベースが環境から受ける影響の可能性を考慮して、それに応じたプログラミングをする必要があります。 しかし、部分的包含データベースを使用することによって、開発者はデータベースに対するインスタンス レベルの影響と、開発者のインスタンス レベルの懸案事項を検出できます。  
  
### <a name="database-administration"></a>データベースの管理  
 データベース設定を master データベースではなくデータベースに保持すると、データベース所有者に **sysadmin** 権限を付与しなくても、各データベース所有者は自身のデータベースをより高度に管理できます。  
  
##  <a name="Limitations"></a> 制限事項  
 部分的包含データベースでは、以下の機能は許可されません。  
  
-   部分的包含データベースは、レプリケーション、変更データ キャプチャ、または変更の追跡を使用できません。  
  
-   番号付きプロシージャ  
  
-   照合順序の変更を伴う、組み込み関数に依存するスキーマ バインド オブジェクト。  
  
-   オブジェクト、列、記号、または型への参照など、照合順序の変更によるバインドの変更。  
  
-   レプリケーション、変更データ キャプチャ、および変更の追跡。  
  
> [!WARNING]  
>  一時ストアド プロシージャは、現在許可されています。 一時ストアド プロシージャは包含関係に違反するので、将来のバージョンの包含データベースではサポートされない予定です。  
  
##  <a name="Identifying"></a> データベースの包含状態の識別  
 データベースの包含状態を識別するのに役立つ 2 つのツールがあります。 [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md) は、データベース内には含まれていない可能性があるすべてのエンティティを示すビューです。 実行時に、実際に含まれていないエンティティが識別されると、database_uncontained_usage イベントが発生します。  
  
### <a name="sysdmdbuncontainedentities"></a>sys.dm_db_uncontained_entities  
 このビューには、データベース内には含まれていない可能性があるエンティティ (データベース境界を越えるエンティティなど) が表示されます。 こうしたエンティティには、データベース モデル外部のオブジェクトを使用するユーザー エンティティが含まれます。 ただし、一部のエンティティ (たとえば、動的 SQL を使用するエンティティ) の包含は実行時まで識別できないため、このビューでは、実際に含まれていないエンティティ以外のエンティティが表示される場合があります。 詳細については、「[sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md)」を参照してください。  
  
### <a name="databaseuncontainedusage-event"></a>database_uncontained_usage イベント  
 この XEvent は、実行時に、含まれていないエンティティが識別されると発生します。 これには、クライアント コードで生成されたエンティティが含まれます。 この Xevent は、実際に含まれていないエンティティに対してのみ発生します。 ただし、このイベントが発生するのは実行時のみです。 したがって、まだ実行されていない場合、含まれていないユーザー エンティティはこの XEvent で識別されません。  
  
## <a name="see-also"></a>参照  
 [変更された機能 &#40;包含データベース&#41;](../../relational-databases/databases/modified-features-contained-database.md)   
 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)   
 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)   
 [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)   
 [包含データベース ユーザー - データベースの可搬性を確保する](../../relational-databases/security/contained-database-users-making-your-database-portable.md)  
  
  
