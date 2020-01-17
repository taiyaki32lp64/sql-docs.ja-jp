---
title: 概要 (SMO) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: e988f9e8-6801-41d1-8069-726f487244d5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b66a0c9efc94d648eba2f4d4f8cff779def413fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63131799"
---
# <a name="overview-smo"></a>概要 (SMO)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) はオブジェクトのプログラムによる管理用に設計された[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 SMO を使用すると、カスタマイズされた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理アプリケーションを作成することができます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を管理するための強力で高度なアプリケーションですが、SMO アプリケーションの方が適している場合もあります。  
  
 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理タスクを制御するユーザー アプリケーションでは、新規ユーザーのニーズを満たし、トレーニング コストを削減するために、単純化を必要とする場合があります。 カスタマイズされた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの作成や、インデックスの効率を高めて、効率性を監視するためのアプリケーション作成が必要になることもあります。 また、サード パーティ製のハードウェアやソフトウェアをデータベース管理アプリケーションにシームレスに含めるために、SMO アプリケーションを使用する場合もあります。  
  
 SMO オブジェクト モデルは、分散管理オブジェクト (SQL-DMO) のオブジェクト モデルを拡張し、その代わりとなるものです。 SQL-DMO と比較して、SMO はパフォーマンス、制御性、および使いやすさの点で向上しています。 ほとんどの SQL-DMO 機能は SMO にも含まれており、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新機能をサポートするさまざまな新しいクラスがあります。 SMO オブジェクト モデルは直感的であり、これまでの技術や知識を引き続き使用するために、可能な限り SQL-DMO 用語が使用されています。  
  
 SMO と互換性が[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]以降のバージョンでは、複数のバージョンの環境を簡単に管理できます。  
  
 SMO には次の新機能が含まれています。  
  
-   キャッシュされたオブジェクト モデルおよび最適化されたオブジェクト インスタンスの作成。 オブジェクトは、参照が指定される場合にのみ読み込まれます。 オブジェクト プロパティは、オブジェクトが作成された場合にのみ部分的に読み込まれます。 残りのオブジェクトおよびプロパティは、直接参照される場合に読み込まれます。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのバッチ実行。 ステートメントがバッチ化されて、ネットワーク パフォーマンスが向上します。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのキャプチャ。 任意の操作をキャプチャしてスクリプトを作成できるようになります。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] では、操作を直ちに実行する代わりに、この機能を使用してスクリプト化を行います。  
  
-   WMI プロバイダーを使用した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL サービスの管理。 プログラムを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの起動、停止および一時停止を行うことができます。  
  
-   高度なスクリプティング。 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを生成して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス上のその他のオブジェクトに対するリレーションシップを記述する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトを再作成することができます。  
  
-   URN (Unique Resource Name) の使用。 URN を使用すると、SMO オブジェクトのインスタンスを作成して、それを参照することができます。  
  
 また、SMO では、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で導入されたいくつかの機能およびコンポーネントが、新しいオブジェクトやプロパティとして表現されています。 これらの新しい機能およびコンポーネントには次のものがあります。  
  
-   パーティション構成にデータを格納するためのテーブルおよびインデックスのパーティション分割。 詳細については、「 [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md)」を参照してください。  
  
-   SOAP 要求を管理するための HTTP エンドポイント。 詳細については、次を参照してください。[を実装するエンドポイント](tasks/implementing-endpoints.md)します。  
  
-   コンカレンシーを高めるためのスナップショット分離と行レベルのバージョニング。 詳細については、「[スナップショット分離を使用した作業](../native-client/features/working-with-snapshot-isolation.md)」を参照してください。  
  
-   XML データの検証と格納を可能にする、XML スキーマ コレクション、XML インデックス、および XML データ型。 詳細については、次を参照してください。 [XML スキーマ コレクション&#40;SQL Server&#41; ](../xml/xml-schema-collections-sql-server.md)と[を使用して XML スキーマ](tasks/using-xml-schemas.md)します。  
  
-   データベースの読み取り専用コピーを作成するためのスナップショット データベース。  
  
-   メッセージ ベースの通信に対する [!INCLUDE[ssSB](../../includes/sssb-md.md)] サポート。 詳細については、次を参照してください。 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース オブジェクトの複数の名前に対するシノニム サポート。 詳細については、次を参照してください。[シノニム&#40;データベース エンジン&#41;](../synonyms/synonyms-database-engine.md)します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] での電子メール サービス、電子メール プロファイル、および電子メール アカウントの作成を可能にするデータベース メールの管理。 詳細については、「 [Database Mail](../database-mail/database-mail.md)」を参照してください。  
  
-   接続情報登録のための登録サーバーのサポート。 詳細については、次を参照してください。[サーバーの登録](../../ssms/register-servers/register-servers.md)します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントのトレースおよび再生。 詳細については、次を参照してください。 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)、 [SQL トレース](../sql-trace/sql-trace.md)、 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)、および[拡張イベント](../extended-events/extended-events.md)します。  
  
-   セキュリティ コントロールのための証明書およびキーのサポート。 詳細については、次を参照してください。[暗号化階層](../security/encryption/encryption-hierarchy.md)します。  
  
-   DDL イベント発生時に機能を追加するための DDL トリガー。 詳細については、「 [DDL トリガー](../triggers/ddl-triggers.md)」を参照してください。  
  
 SMO の名前空間は、<xref:Microsoft.SqlServer.Management.Smo> です。 SMO は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]アセンブリ。 つまり、共通言語ランタイムが、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SMO オブジェクトを使用する前に version 2.0 をインストールする必要があります。 SMO アセンブリは、既定では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SDK オプションを使用してグローバル アセンブリ キャッシュ (GAC) にインストールされています。 アセンブリは [!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)] にあります。 詳細については、次を参照してください。、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]ドキュメント。  
  
## <a name="smo-classes"></a>SMO クラス  
 SMO クラスには、インスタンス クラスおよびユーティリティ クラスの 2 つのカテゴリがあります。  
  
 **インスタンス クラス**  
  
 インスタンス クラスは、サーバー、データベース、テーブル、トリガー、およびストアド プロシージャなどの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトを表現します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへの接続を確立し、これに送信されたコマンドのキャプチャ モードを制御するには、<xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスが使用されます。  
  
 SMO インスタンス オブジェクトは、データベース サーバーの階層を表す階層を形成しています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが最上位にあり、その下にデータベース、さらにテーブル、列、トリガーなどが続きます。 1 つまたは複数の列を持つテーブルなど、1 つの親から複数の子へのリレーションシップが論理的に存在している場合、子はオブジェクトのコレクションによって表されます。 それ以外の場合、子は 1 つのオブジェクトによってのみ表されます。  
  
 **ユーティリティ クラス**  
  
 ユーティリティ クラスとは、特定のタスクを実行するために明示的に作成されたオブジェクトのグループです。 これらは、関数に基づいて、次のように異なるオブジェクト階層に分割されています。  
  
-   転送クラス。 スキーマおよびデータをその他のデータベースに転送するために使用されます。  
  
-   バックアップおよび復元クラス。 データベースのバックアップおよび復元のために使用されます。  
  
-   スクリプター クラス。 オブジェクトとオブジェクトの依存関係を再生成するためのスクリプト ファイルを作成するために使用されます。  
  
## <a name="new-smo-features"></a>新しい SMO の機能  
 **パフォーマンスの最適化**  
  
 SQL-DMO では、オブジェクト列挙は、コレクション内の各オブジェクトが完全にインスタンス化されている必要がありました。 これは、ネットワークおよびメモリの使用量の観点からは効率的ではありません。 多くの場合、オブジェクトは、プロパティの多くが明示的に参照されずにインスタンス化されます。  
  
 SMO アーキテクチャでは、オブジェクトが最初は部分的にのみインスタンス化されて最小限のプロパティ情報がサーバーから要求されるため、この方がメモリの観点からはより効率的です。 オブジェクトの完全なインスタンス化は、オブジェクトが明示的に参照されるまで行われません。 最初に取得されるプロパティのセットにはないプロパティが要求されたり、そのようなプロパティを要求するメソッドが呼び出された場合に、オブジェクトの完全なインスタンス化が行われます。 部分的にインスタンス化されたオブジェクトと完全にインスタンス化されたオブジェクトの間での移行は、ユーザーに対して透過的です。 また、大量のメモリを使用するプロパティは、明示的に参照されない限り取得されません。 この例として、<xref:Microsoft.SqlServer.Management.Smo.Database.Size%2A> オブジェクト プロパティの <xref:Microsoft.SqlServer.Management.Smo.Database> プロパティがあります。 ただし、部分的なインスタンス化では、より多くのネットワーク ラウンド トリップが必要になるため、使用しているアプリケーションに対して最適なパフォーマンス オプションではない可能性もあります。  
  
 インスタンス化を制御すると、システム環境を最適化することができます。 プロパティの参照時に大量のサーバー要求がトリガーされる場合がありますが、遅延インスタンス化の手法を使用することで、アプリケーションが必要とするメモリ量が最小化されます。  
  
 実際のデータベース オブジェクトを表したオブジェクトであるインスタンス クラスには、インスタンス化の 3 つのレベルがあります。 最小インスタンス化 (必要な最小限のプロパティのみが 1 つのブロックに読み取られる)、部分的インスタンス化 (比較的大量のメモリを使用するすべてのプロパティが 1 つのブロックに読み取られる)、および完全インスタンス化の 3 つです。 従来、インスタンス化の状態は、インスタンスされていないか完全にインスタンス化されているかのいずれかでした。 部分的にインスタンス化されたオブジェクトには、オブジェクト プロパティの完全なセットに対する値が格納されていないため、部分的インスタンス化の状態は効率性の向上に役立ちます。 部分的インスタンス化は、直接参照されないオブジェクトの既定の状態です。 これらのプロパティの 1 つが参照されると、オブジェクトの完全インスタンス化を要求するフォールトが生成されます。  
  
 **キャプチャの実行**  
  
 直接実行は、通常の実行方法です。 ステートメントは、発生した時点で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに直接送信されます。 キャプチャ実行は、これに代わる方法です。  
  
 キャプチャ実行では、通常実行される [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチをキャプチャすることができます。 これにより、SMO プログラマは、スクリプトの保留、後で実行するための格納、エンドユーザーへのプレビューの提供を行うことができます。 たとえば、`create database` ステートメント、`create table` ステートメント、および `create index` ステートメントを 1 つのバッチで送信し、3 つの連続した手順として実行することができます。 この機能は、<xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> オブジェクトを使用して、ユーザーによって制御されます。  
  
 **WMI プロバイダー**  
  
 WMI プロバイダー オブジェクトは、SMO によってラップされます。 これによって SMO プログラマには、名前空間によって表されるプログラミング モデルおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI プロバイダーの詳細の理解を必要とせずに、SMO クラスと非常によく似た簡単なオブジェクト モデルが提供されます。 WMI プロバイダーでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス、別名、クライアントおよびサーバー ネットワーク ライブラリを構成することができます。  
  
 **スクリプトの作成**  
  
 SMO では、スクリプティングが拡張されて `Scripter` クラスに移動されました。 `Scripter`クラスの依存関係を検出、オブジェクト、および依存関係階層の操作を可能間のリレーションシップを理解することができます。 主なスクリプティング オブジェクトは、`Scripter` オブジェクトです。 また、依存関係を処理したり、進行中のイベントやエラー イベントに応答するサポート オブジェクトもいくつかあります。  
  
 `Scripter` オブジェクトは、次の高度なスクリプティング オプションをサポートします。  
  
-   簡単な 1 フェーズ スクリプティング (スクリプトを 1 つの手順で作成)  
  
-   高度な 3 フェーズ スクリプティング (従属関係検索、リスト生成、スクリプト生成の 3 つの手順でスクリプトを作成)  
  
-   2 方向の依存関係検索 (依存関係または依存の検索の許可)  
  
-   進行中イベントへの応答  
  
-   エラー イベントへの応答  
  
 **一意のリソース名**  
  
 SMO オブジェクト ライブラリを使用するうえでの鍵となる概念の 1 つが URN (Unique Resource Name) です。 URN は、XPath と同様の構文を使用します。 XPath は、各レベルで修飾子と関数を持つオブジェクトを指定するために使用される階層パスです。 SMO では、URN には、パス、および制限された機能を持つ属性名の 2 つの要素があります。 パスはオブジェクトの場所を指定するために使用され、属性名によってある程度のフィルター操作が可能になります。  
  
 データベースの URN の例は次のようになります。  
  
```  
/Server/Database[@Name='Adventureworks2012']  
```  
  
 オブジェクトの URN は、URN プロパティを参照することで取得することができます。 また、Scripter オブジェクトは URN を使用し、オブジェクト参照を `Scripter` オブジェクトのメソッドに渡します。 さらの URN を指定できます、 **GetSmoObject**のメソッド、`Server`オブジェクト。 これは、SMO オブジェクトのインスタンスを作成するために使用します。  
  
## <a name="new-sql-server-features-represented-in-smo"></a>SMO で表される SQL Server の新機能  
 **テーブルおよびインデックスがパーティション分割**  
  
 インデックス テーブル パーティション分割によって、ファイル グループにまたがるテーブルとインデックスのデータの分散を管理することができます。 SMO オブジェクトには、この新機能が反映されています。  
  
 **エンドポイント**  
  
 SOAP およびデータベース ミラーリング要求は、<xref:Microsoft.SqlServer.Management.Smo.Endpoint> オブジェクトを使用して、エンドポイントによって処理されます。  
  
 **スナップショット分離/行レベル バージョン**  
  
 スナップショット分離 (行レベル バージョン) は、新しい <xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクト プロパティで表現されます。  
  
 **XML スキーマの Namespace、XML インデックスおよび XML データ型**  
  
 XML スキーマ名前空間は、SMO ではオブジェクトのコレクションで表現されます。 XML インデックスは、SMO では `Index` オブジェクト プロパティで表現されます。  
  
 **フルテキスト検索の機能強化**  
  
 SMO には、フルテキスト検索の機能強化を反映した新しいオブジェクトが提供されています。  
  
 **[ページ確認]**  
  
 <xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions.PageVerify%2A> オブジェクトは、データベース ページ確認オプションを表します。  
  
 **スナップショット データベース**  
  
 スナップショット データベースは、特定の時点における、指定されたデータベースの読み取り専用のコピーです。 スナップショット データベースは、<xref:Microsoft.SqlServer.Management.Smo.Database.IsDatabaseSnapshot%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Database> プロパティを使用して指定することができます。  
  
 **Service Broker**  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] およびその機能は、オブジェクトのグループで表現されます。  
  
 **インデックスの機能強化**  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インデックスの機能強化は、<xref:Microsoft.SqlServer.Management.Smo.Index> オブジェクトの新しいプロパティに反映されています。  
  
## <a name="smo-and-sql-dmo"></a>SMO および SQL-DMO  
 SMO オブジェクト モデルは、SQL-DMO の代わりとなるものです。 SMO では、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンがサポートされます。 SMO では、より多くの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理タスクがサポートされ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の多くの新機能が含まれています。 SMO は、より効率的であり、より高度な制御を提供するようにデザインされています。  
  
 SMO が [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] アセンブリとして実装されるのに対し、DMO ライブラリは COM オブジェクト モデルです。 COM コンポーネントは、アプリケーションおよびアンマネージ アプリケーション プログラミングに対して、再利用可能な機能を提供するライブラリです。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] アセンブリは、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] に対して再利用可能な機能を提供して、マネージド コード アプリケーションを作成します。  
  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] テクノロジへの移行の際に、アプリケーションを部分的にマネージド コードで作成し、その他の部分をアンマネージド コードで作成することが可能です。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] では、COM コンポーネントとのやり取りが可能です。これには、プライマリ相互運用機能アセンブリが必要になります。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ベースのアプリケーションから SQL-DMO を呼び出すには、ランタイム ラッパーが必要です。  
  
## <a name="see-also"></a>参照  
 [レプリケーション管理オブジェクトの概念](../replication/concepts/replication-management-objects-concepts.md)  
  
  
