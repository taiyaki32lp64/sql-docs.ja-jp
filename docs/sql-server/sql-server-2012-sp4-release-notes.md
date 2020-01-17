---
title: SQL Server 2012 Service Pack のリリース ノート | Microsoft Docs
ms.prod: sql
ms.technology: install
ms.custom: ''
ms.date: 02/26/2018
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
author: craigg-msft
ms.author: craigg
monikerRange: = sql-server-2014 || = sqlallproducts-allversions
ms.openlocfilehash: 6fba15e73edf14b9bb794012c8fe56ec8264a5b2
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632950"
---
# <a name="sql-server-2012-service-pack-release-notes"></a>SQL Server 2012 Service Pack のリリース ノート
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
このトピックには、SQL Server 2012 の 4 つのサービス パックの集約したリリース ノートが含まれています。 各サービス パックは、前のサービス パックの累積です。

Service Pack は、インストール メディアではなくオンラインでのみ入手可能です。以下からダウンロードできます。
- [SQL Server 2012 SP4](https://go.microsoft.com/fwlink/?linkid=846937)
- [SQL Server 2012 SP3](https://support.microsoft.com/help/3072779/sql-server-2012-service-pack-3-release-information)
- [SQL Server 2012 SP2](https://support.microsoft.com/KB/2958429)
- [SQL Server 2012 SP1](https://go.microsoft.com/fwlink/p/?LinkID=268158)

## <a name="service-pack-4-release-notes"></a>Service Pack 4 リリース ノート

### <a name="download-pages"></a>ダウンロード ページ

- [SQL Server 2012 SP4 Feature Pack](https://www.microsoft.com/download/details.aspx?id=56041)
- [SQL Server 2012 SP4 の更新プログラムのインストール](https://www.microsoft.com/download/details.aspx?id=56040)
- [SQL Server 2012 SP4 Express](https://www.microsoft.com/download/details.aspx?id=56042)


### <a name="performance-and-scale-improvements"></a>パフォーマンスとスケーリングの改善
- **ディストリビューション エージェントのクリーンアップ プロシージャの向上**:サイズ超過のディストリビューション データベースが原因で、ブロックとデッドロックの状況が発生していました。 クリーンアップ プロシージャの向上は、これらのブロックまたはデッドロックのシナリオの一部を排除することを目的としています。 
- **動的メモリ オブジェクトのスケーリング**: 最新のハードウェア上でスケールするノードとコアの数に基づいて、動的にメモリ オブジェクトをパーティション分割します。 動的な昇格の目的は、潜在的なボトルネックを回避し、スレッド セーフ メモリ オブジェクトを自動的にパーティション分割することです。 パーティション分割されていないメモリ オブジェクトは、ノードによってパーティション分割されるように動的に昇格できます。 パーティションの数は、NUMA ノードの数と同じです。 ノードによってパーティション分割されたメモリ オブジェクトは、CPU によってパーティション分割されるようにさらに昇格することができます。この場合、パーティションの数は CPU の数と等しくなります。
- **8 TB を超えるバッファー プールの有効化**: バッファー プールの使用量に対し 128 TB の仮想アドレス空間を有効にします。
- **Change Tracking のクリーンアップ**: Change Tracking のクリーンアップのパフォーマンスと Change Tracking のサイド テーブルの効率性が向上しました。 

### <a name="supportability-and-diagnostics-improvements"></a>サポート性と診断の向上
- **レプリケーション エージェントの完全ダンプのサポート**: 現在は、レプリケーション エージェントがハンドルされない例外に遭遇すると、既定の動作では例外の現象のミニ ダンプが作成されます。 既定の動作では、ハンドルされない例外に対する複雑なトラブルシューティング手順が必要です。 SP4 では、レプリケーション エージェントの完全ダンプの作成をサポートする新しいレジストリ キーが導入されました。
- **プラン表示 XML での診断の拡張**: プラン表示 XML は、有効なトレース フラグ、最適化された入れ子になったループ結合のメモリ部分、CPU 時間、および経過時間に関する情報を公開するために拡張されています。 
- **診断 XE および DMV 間の相関関係の改善**: クエリを一意に識別するために Query_hash と query_plan_hash フィールドが使用されます。 DMV はこれらを varbinary(8) として定義するのに対し、XEvent は UINT64 として定義します。 SQL Server に "符号なし bigint" がないため、キャストが機能しない場合があります。 この機能強化では、新しい XEvent アクション/フィルター列が導入されています。これは XE と DMV 間の関連付けクエリに役立つ INT64 として定義されている点を除き、query_hash と query_plan_hash と同等です。 
- **メモリ許可/使用状況の診断の向上**: 新しい query_memory_grant_usage XEvent (サーバー 2016 SP1 から移植)。
- **SSL ネゴシエーション手順へのプロトコル トレースの追加**: ネゴシエーションの成功/失敗のビット トレース情報 (プロトコルなど) を追加します。たとえば TLS 1.2 の展開時に接続性のシナリオをトラブルシューティングするときに役に立ちます。
- **ディストリビューション データベースの正しい互換性レベルの設定**: サービス パックをインストールすると、ディストリビューション データベースの互換性レベルが 90 に変わります。 レベルが変更されたのは、sp_vupgrade_replication ストアド プロシージャの問題によるものです。 SP はディストリビューション データベースに正しい互換性レベルが設定されるように変更されています。 
- **データベースの複製を作成する新しい DBCC コマンド**: 複製データベースは、CSS などのパワー ユーザーがスキーマとメタデータをデータなしで複製することによって、既存の運用データベースをトラブルシューティングできるように追加された、新しい DBCC コマンドです。 呼び出しは、DBCC clonedatabase ('source_database_name', 'clone_database_name') で実行されます。 複製されたデータベースは、実稼働環境では使用できません。 データベースが複製データベースの呼び出しから生成されているかどうかを確認するには、次のコマンドを使用して、DATABASEPROPERTYEX('clonedb', 'isClone') を選択します。戻り値 1 が true、0 が false です。 
- **SQL エラー ログの TempDB ファイルとファイル サイズの情報**: スタートアップ時に、TempDB データ ファイルのサイズと自動拡張が異なる場合、ファイルの数を出力し、警告をトリガーします。
- **SQL Server エラー ログの IFI サポート メッセージ**: エラー ログにデータベース ファイルの瞬時初期化の有効/無効を示します。
- **DBCC INPUTBUFFER に置き換わる新しい DMF**: DBCC INPUTBUFFER を置き換えるため、session_id をパラメーターとして受け取る新しい動的管理関数 sys.dm_input_buffer が導入されました。
- **可用性グループの読み取りルーティングの障害に対する Xevent の機能強化**: 現在、read_only_rout_fail XEvent は、ルーティング リストがあるが、リスト内のどのサーバーも接続に使用できない場合にのみ起動されます。 この機能強化には、トラブルシューティングに役立つ追加情報と、XEvent が起動するコード ポイントの拡張も含まれます。 
- **可用性グループのフェールオーバーを使用した Service Broker の処理の向上**: 現在、可用性グループのデータベースで Service Broker が有効になっていると、プライマリ レプリカで開始されたすべての Service Broker の接続は、AG フェールオーバー中に開いたままになります。 この機能強化により、AG フェールオーバー中、これらの開いたままの接続がすべて閉じられます。
- **自動ソフト NUMA のパーティション分割**: サーバー レベルでトレース フラグ 8079 が有効になっている場合、SQL 2014 SP2 で自動[ソフト NUMA](../database-engine/configure-windows/soft-numa-sql-server.md) パーティション分割が導入されます。 スタートアップ時にトレース フラグ 8079 が有効になっていると、SQL Server 2014 SP2 はハードウェア レイアウトを問い合わせて、NUMA ノードあたり 8 個以上の CPU をレポートするシステムにソフト NUMA を自動的に構成します。 自動ソフト NUMA の動作は、ハイパースレッド (HT/論理プロセッサ) に対応しています。 パーティション分割と追加ノードの作成により、リスナーの数の増加、スケーリング、およびネットワークと暗号化機能の向上により、バックグラウンド処理が拡張されます。 自動ソフト NUMA を実稼働環境でオンにする前に、最初にワークロードのパフォーマンスをテストすることをお勧めします。

## <a name="service-pack-3-release-notes"></a>Service Pack 3 リリース ノート

### <a name="download-pages"></a>ダウンロード ページ
- [SQL Server 2012 SP3 Feature Pack](https://go.microsoft.com/fwlink/?linkid=615935)
- [SQL Server 2012 SP3 Express](https://go.microsoft.com/fwlink/?linkid=692144)

現在インストールされているバージョンに対応したダウンロードするファイルの場所と名前がわかる詳細情報については、「[SQL Server 2012 Service Pack 3 release information](https://support.microsoft.com/help/3072779/sql-server-2012-service-pack-3-release-information)」(SQL Server 2012 Service Pack 3 リリース情報) の「Select the correct file to download」(ダウンロードする正しいファイルの選択) セクションをご覧ください。

## <a name="service-pack-2-release-notes"></a>Service Pack 2 リリース ノート
  
### <a name="download-pages"></a>ダウンロード ページ 
- [SQL Server 2012 SP2 Feature Pack](https://go.microsoft.com/fwlink/?LinkID=401008)
- [SQL Server 2012 SP2 Express](https://go.microsoft.com/fwlink/?LinkID=401007)

次の表を使用して、現在インストールされているバージョンを基に、ダウンロードするファイルの場所と名前を確認します。 システム要件と基本的なインストール手順が含まれているページをダウンロードします。  

|現在インストールされているバージョン|目的|ダウンロードとインストール|  
|---|---|---|   
|32 ビット インストール:|||  
|SQL Server 2012 のいずれかのエディションの 32 ビット バージョン|SQL Server 2012 SP2 の 32 ビット バージョンにアップグレード|**SQLServer2012SP2-KB2958429-** <arch> **-** <lang id> **.exe** ( [SQL Server 2012 SP2 のダウンロード ページ](https://go.microsoft.com/fwlink/?LinkID=401006)|  
|SQL Server 2012 RTM Express の 32 ビット バージョン|SQL Server 2012 Express SP2 の 32 ビット バージョンにアップグレード|**SQLEXPR_** <arch> **_** <lang> **.msi** ( [SQL Server 2012 SP2 Express のダウンロード ページ](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|SQL Server 2012 のクライアントと管理ツールのみの 32 ビット バージョン (SQL Server 2012 Management Studio を含む)|SQL Server 2012 SP2 の 32 ビット バージョンにクライアントと管理ツールをアップグレード|**SQLEXPRWT_** <arch> **_** <lang> **.msi** ( [SQL Server 2012 SP2 Express のダウンロード ページ](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|SQL Server 2012 Management Studio Express の 32 ビット バージョン|SQL Server 2012 SP2 Management Studio Express の 32 ビット バージョンにアップグレード|**SQLManagementStudio_** <arch> **_** <lang> **.msi** ( [SQL Server 2012 SP2 Express のダウンロード ページ](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|SQL Server 2012 のいずれかのエディションの 32 ビット バージョンおよびクライアントと管理ツールの 32 ビット バージョン (SQL Server 2012 RTM Management Studio を含む)|SQL Server 2012 SP2 の 32 ビット バージョンにすべての製品をアップグレード|**SQLEXPRADV_** <arch> **_** <lang> **.msi** ( [SQL Server 2012 SP2 Express のダウンロード ページ](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|[Microsoft SQL Server 2012 RTM Feature Pack](https://www.microsoft.com/download/details.aspx?id=29065) または [Microsoft SQL Server 2012 SP1 Feature Pack](https://go.microsoft.com/fwlink/p/?LinkID=268266)の 1 つ以上のツールの 32 ビット バージョン|Microsoft SQL Server 2012 SP2 用 Feature Pack の 32 ビット バージョンにツールをアップグレード|Microsoft [SQL Server 2012 SP2 Feature Pack のダウンロード ページ](https://go.microsoft.com/fwlink/?LinkID=401008)の 1 つ以上のツール|  
|64 ビット インストール:|||  
|SQL Server 2012 のいずれかのエディションの 64 ビット バージョン|SQL Server 2012 SP2 の 64 ビット バージョンにアップグレード|SQLServer2012SP2-KB2958429-<arch>-<langid>.exe ( [SQL Server 2012 SP2 のダウンロード ページ](https://go.microsoft.com/fwlink/?LinkID=401006)から)|  
|SQL Server 2012 RTM Express の 64 ビット バージョン|SQL Server 2012 SP2 の 64 ビット バージョンにアップグレード|**SQLEXPR_** <arch> **_** <lang> **.msi** ( [SQL Server 2012 SP2 Express のダウンロード ページ](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|SQL Server 2012 のクライアントと管理ツールのみの 64 ビット バージョン (SQL Server 2012 Management Studio 含む)|SQL Server 2012 SP2 の 64 ビット バージョンにクライアントと管理ツールをアップグレード|**SQLEXPRWT_** <arch> **_** <lang> **.msi** ( [SQL Server 2012 SP2 Express のダウンロード ページ](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|SQL Server 2012 Management Studio Express の 64 ビット バージョン|SQL Server 2012 SP2 Management Studio Express の 64 ビット バージョンにアップグレード|**SQLManagementStudio_** <arch> **_** <lang> **.msi** ( [SQL Server 2012 SP2 Express のダウンロード ページ](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|[Microsoft SQL Server 2012 RTM Feature Pack](https://www.microsoft.com/download/details.aspx?id=29065) または [Microsoft SQL Server 2012 SP1 Feature Pack](https://go.microsoft.com/fwlink/p/?LinkID=268266)の 1 つ以上のツールの 64 ビット バージョン|Microsoft SQL Server 2012 SP2 用 Feature Pack の 64 ビット バージョンにツールをアップグレード|Microsoft [SQL Server 2012 SP2 Feature Pack のダウンロード ページ](https://go.microsoft.com/fwlink/?LinkID=401008)の 1 つ以上のツール|   


## <a name="service-pack-1-release-notes"></a>Service Pack 1 リリース ノート

### <a name="download-pages"></a>ダウンロード ページ  
- [SQL Server 2012 SP1 Feature Pack](https://go.microsoft.com/fwlink/p/?LinkID=268158)
- [SQL Server 2012 SP1 Express](https://www.microsoft.com/download/details.aspx?id=35579)


ダウンロードとインストールに使用するファイルを確認するには、次の表を参照してください。 サービス パックをインストールする前に、システム要件を正しく満たしていることを確認します。 システム要件は、この表にあるリンクされたダウンロード ページに記載されています。  

|現在インストールされているバージョン|目的|ダウンロードとインストール|  
|---|---|---|  
|**32 ビット インストール:**|||  
|SQL Server 2012 のいずれかのエディションの 32 ビット バージョン|SQL Server 2012 SP1 の 32 ビット バージョンにアップグレード|SQLServer2012SP1-KB2674319-x86-ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=268158)から)|  
|SQL Server 2012 RTM Express の 32 ビット バージョン|SQL Server 2012 Express SP1 の 32 ビット バージョンにアップグレード|SQLServer2012SP1-KB2674319-x86-ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=268158)から)|  
|SQL Server 2012 のクライアントと管理ツールのみの 32 ビット バージョン (SQL Server 2012 Management Studio を含む)|SQL Server 2012 SP1 の 32 ビット バージョンにクライアントと管理ツールをアップグレード|SQLManagementStudio_x86_ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=267905)から)|  
|SQL Server 2012 Management Studio Express の 32 ビット バージョン|SQL Server 2012 SP1 Management Studio Express の 32 ビット バージョンにアップグレード|SQLManagementStudio_x86_ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=267905)から)|  
|SQL Server 2012 のいずれかのエディションの 32 ビット バージョン **および** クライアントと管理ツールの 32 ビット バージョン (SQL Server 2012 RTM Management Studio 含む)|SQL Server 2012 SP1 の 32 ビット バージョンにすべての製品をアップグレード|SQLServer2012SP1-KB2674319-x86-ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=268158)から)|  
|[Microsoft SQL Server 2012 RTM Feature Pack](https://www.microsoft.com/download/details.aspx?id=16978)の 1 つ以上のツールの 32 ビット バージョン|Microsoft SQL Server 2012 SP1 用 Feature Pack の 32 ビット バージョンにツールをアップグレード|[Microsoft SQL Server 2012 SP1 Feature Pack](https://go.microsoft.com/fwlink/p/?LinkID=268266)の 1 つ以上のファイル|  
|SQL Server 2012 の 32 ビット インストールなし|SP1 を含む 32 ビット バージョンの SQL Server 2012 をインストール (SP1 がプレインストールされた新しいインスタンス)|SQLServer2012SP1-FullSlipstream-x86-ENU.exe **および** SQLServer2012SP1-FullSlipstream-x86-ENU.box ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=268158)から)|  
|SQL Server 2012 Management Studio の 32 ビット インストールなし|32 ビットの SQL Server 2012 Management Studio をインストール (SP1 を含む)|SQLManagementStudio_x86_ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkId=267905)から)|  
|SQL Server 2012 RTM Express の 32 ビット バージョンなし|32 ビットの SQL Server 2012 Express をインストール (SP1 を含む)|SQLEXPR32_x86_ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkId=267905)から)|  
|**SQL Server 2008** または **SQL Server 2008 R2**の 32 ビット インストール|32 ビットの SQL Server 2012 (SP1 含む) に**インプレース アップグレード**|SQLServer2012SP1-FullSlipstream-x86-ENU.exe **および** SQLServer2012SP1-FullSlipstream-x86-ENU.box ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=268158)から)|  
|**64 ビット インストール:**|||  
|SQL Server 2012 のいずれかのエディションの 64 ビット バージョン|SQL Server 2012 SP1 の 64 ビット バージョンにアップグレード|SQLServer2012SP1-KB2674319-x64-ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=268158)から)|  
|SQL Server 2012 RTM Express の 64 ビット バージョン|SQL Server 2012 SP1 の 64 ビット バージョンにアップグレード|SQLServer2012SP1-KB2674319-x64-ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=268158)から)|  
|SQL Server 2012 のクライアントと管理ツールのみの 64 ビット バージョン (SQL Server 2012 Management Studio 含む)|SQL Server 2012 SP1 の 64 ビット バージョンにクライアントと管理ツールをアップグレード|SQLManagementStudio_x64_ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=267905)から)|  
|SQL Server 2012 Management Studio Express の 64 ビット バージョン|SQL Server 2012 SP1 Management Studio Express の 64 ビット バージョンにアップグレード|SQLManagementStudio_x64_ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=267905)から)|  
|SQL Server 2012 のいずれかのエディションの 64 ビット バージョン **および** クライアントと管理ツールの 64 ビット バージョン (SQL Server 2012 RTM Management Studio を含む)|SQL Server 2012 SP1 の 64 ビット バージョンにすべての製品をアップグレード|SQLServer2012SP1-KB2674319-x64-ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=268158)から)|  
|[Microsoft SQL Server 2012 RTM Feature Pack](https://www.microsoft.com/download/en/details.aspx?id=16978)の 1 つ以上のツールの 64 ビット バージョン|Microsoft SQL Server 2012 SP1 用 Feature Pack の 64 ビット バージョンにツールをアップグレード|[Microsoft SQL Server 2012 SP1 Feature Pack](https://go.microsoft.com/fwlink/p/?LinkID=268266)の 1 つ以上のファイル|  
|SQL Server 2012 の 64 ビット インストールなし|SP1 を含む 64 ビット バージョンの SQL Server 2012 をインストール (SP1 がプレインストールされた新しいインスタンス)|SQLServer2012SP1-FullSlipstream-x64-ENU.exe **および** SQLServer2012SP1-FullSlipstream-x64-ENU.box ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=268158)から)|  
|SQL Server 2012 Management Studio の 64 ビット インストールなし|64 ビットの SQL Server 2012 Management Studio をインストール (SP1 含む)|SQLManagementStudio_x64_ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=267905)から)|  
|SQL Server 2012 RTM Express の 64 ビット バージョンなし|64 ビットの SQL Server 2012 Express をインストール (SP1 含む)|SQLEXPR_x64_ENU.exe ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=267905)から)|  
|**SQL Server 2008** または **SQL Server 2008 R2**の 64 ビット インストール|64 ビットの SQL Server 2012 (SP1 含む) に**インプレース アップグレード**|SQLServer2012SP1-FullSlipstream-x64-ENU.exe **および** SQLServer2012SP1-FullSlipstream-x64-ENU.box ( [こちら](https://go.microsoft.com/fwlink/p/?LinkID=268158)から)|  

### <a name="known-issues-fixed-in-this-service-pack"></a>この Service Pack で修正された既知の問題  
この Service Pack で修正されたすべてのバグと既知の問題については、 [サポート技術情報記事](https://support.microsoft.com/kb/2674319)を参照してください。   

### <a name="reinstalling--instances-of-sql-server-failover-cluster-fails-if-you-use-the-same-ip-address"></a>同じ IP アドレスを使用すると SQL Server フェールオーバー クラスターのインスタンスの再インストールに失敗する  
**問題点:** SQL Server フェールオーバー クラスター インスタンスのインストール中に不正な IP アドレスを指定すると、インストールは失敗します。 失敗したインスタンスをアンインストールした後に、同じインスタンス名と適切な IP アドレスを使用して SQL Server フェールオーバー クラスター インスタンスを再インストールしようとすると、インストールは失敗します。 このエラーは、前のインストールによって残されたリソース グループが重複するため発生します。  
  
**回避策:** この問題を解決するには、再インストール時に別のインスタンス名を使用するか、再インストール前にリソース グループを手動で削除してください。 詳細については、「 [SQL Server フェールオーバー クラスターでのノードの追加または削除](failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)」をご覧ください。 
  
### <a name="analysis-services-and-powerpivot"></a>Analysis Services と PowerPivot  
  
##### <a name="powerpivot-configuration-tool-does-not-create-the-powerpivot-gallery"></a>PowerPivot 構成ツールで PowerPivot ギャラリーが作成されない  
**問題点:** PowerPivot 構成ツールはチーム サイトを準備するため、PowerPivot ギャラリーは作成されません。  
  
**回避策:** 新しいアプリ (ライブラリ) を作成します。  
  
1.  サイト コレクション機能の **[サイト コレクションの PowerPivot 機能の統合]** がアクティブになっていることを確認します。  
  
2.  既存のサイトの **[サイト コンテンツ]** ページで、 **[アプリの追加]** をクリックします。  
  
3.  **[PowerPivot ギャラリー]** をクリックします。  
  
#### <a name="to-use-powerpivot-for-excel-with-excel-2013-you-must-use-the-add-in-that-is-installed-with-excel"></a>Excel 2013 で PowerPivot for Excel を使用する場合は Excel と一緒にインストールされたアドインを使用する必要がある  
**問題点:** Office 2010 では、PowerPivot for Excel は [https://www.microsoft.com/bi/powerpivot.aspx](https://www.microsoft.com/bi/powerpivot.aspx) からダウンロードできるスタンドアロンのアドインです。 このアドインは、 [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=29074)からもダウンロードできます。 PowerPivot アドインは 2 つのバージョンをダウンロードできることにご留意ください。SQL Server 2008 R2 と SQL Server 2012 にそれぞれ付属するバージョンです。 ただし、Office 2013 の場合、PowerPivot for Excel は Offce に付属していて、Excel のインストール時にインストールされます。 SQL Server 2008 R2 および SQL Server 2012 に付属の PowerPivot for Excel 2010 には Excel 2013 との互換性はありませんが、Excel 2010 と Excel 2013 をサイド バイ サイドで実行する場合は、クライアント コンピューターに PowerPivot for Excel 2010 をインストールできます。 つまり、2 つのバージョンの Excel が共存できるため、対応する PowerPivot アドインも共存できます。  
  
**回避策:** PowerPivot for Excel 2013 を使用するには、COM アドインを有効にする必要があります。 Excel 2013 で、 **[ファイル]**  |  **[オプション]**  |  **[アドイン]** の順にクリックします。 **[管理]** ドロップダウン ボックスの一覧で **[COM アドイン]** を選択し、 **[設定]** をクリックします。 **[COM アドイン]** で、 **[Microsoft Office PowerPivot for Excel 2013]** を選択し、 **[OK]** をクリックします。  
  
### <a name="reporting-services"></a>Reporting Services  
  
#### <a name="install-and-configure-sharepoint-server-2013-prior-to-installing-reporting-services"></a>Reporting Services をインストールする前に SharePoint Server 2013 をインストールおよび構成する  
**問題点:** SQL Server Reporting Services (SSRS) をインストールする**前に**、次の要件を完了します。  
  
1.  SharePoint 2013 製品準備ツールを実行します。  
  
2.  SharePoint Server 2013 をインストールします。  
  
3.  SharePoint 2013 製品構成ウィザードを実行するか、同等の構成手順を完了して SharePoint ファームを構成します。  
  
**回避策:** SharePoint ファームが構成される前に [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint モードをインストールした場合、必要な回避策は、インストールされている他のコンポーネントによって異なります。  
  
#### <a name="power-view-in-sharepoint-server-2013-requires-microsoftanalysisservicesspclientdll"></a>SharePoint Server 2013 の Power View には Microsoft.AnalysisServices.SPClient.dll が必要  
**問題点:** [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、必須コンポーネントの **Microsoft.AnalysisServices.SPClient.dll** がインストールされません。 SharePoint Server 2013 Preview と [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] を SharePoint モードでインストールしても、PowerPivot for SharePoint 2013 インストーラー パッケージ ( **spPowerPivot.msi** ) をダウンロードしてインストールしないと、Power View は動作せず、Power View では次の現象が発生します。  
  
**現象:** Power View レポートを作成しようとすると、次のようなエラー メッセージが表示されます。  
  
-   "データ ソースへの接続を作成できません"  
  
内部エラーの詳細には、次のようなメッセージが含まれます。  
  
-   "値 'SharePoint Principal' は、接続文字列プロパティ 'User Identity' ではサポートされていません。"  
  
**回避策:** SharePoint Server 2013 に PowerPivot for SharePoint 2013 インストーラー パッケージ (**spPowerPivot.msi**) をインストールします。 インストーラー パッケージは、 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 機能パックに付属しています。 この機能パックは、 [!INCLUDE[msCoName](../includes/msconame-md.md)] ダウンロード センターの [SQL Server 2012 SP1 機能パック](https://go.microsoft.com/fwlink/p/?LinkID=268266) からダウンロードできます。  
  
#### <a name="power-view-sheets-in-a-powerpivot-workbook-are-deleted-after-a-scheduled-data-refresh"></a>定期データ更新の後で、PowerPivot ブックの Power View シートが削除される  
**問題点**: PowerPivot for SharePoint アドインでは、Power View が含まれたブックで **定期データ更新** を使用すると、すべての Power View シートが削除されます。  
  
**回避策**:Power View ブックで **Scheduled Data Refresh** を使用するには、データ モデルだけの PowerPivot ブックを作成します。 Excel シートと Power View シートを含む別のブックを作成し、データ モデルを含む PowerPivot ブックにリンクします。 データ モデルを含む PowerPivot ブックに対してのみ、定期データ更新を実行します。  
  
### <a name="data-quality-services"></a>Data Quality Services  
  
#### <a name="dqs-available-in-the-incorrect-edition-of-sql-server-2012"></a>DQS がサポートされていないエディションの SQL Server 2012 で使用可能になる  
**問題点:** [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] RTM リリースでは、Enterprise、Business Intelligence、Developer 以外のエディションの SQL Server でも Data Quality Services (DQS) 機能を使用できます。 SQL Server 2012 SP1 のインストール後は、Enterprise、Business Intelligence、および Developer 以外のエディションで DQS を使用できなくなります。  
  
**回避策**:サポートされていないエディションで DQS を使用している場合は、サポートされているエディションにアップグレードするか、アプリケーションをこの機能に依存しないように変更します。  
  
### <a name="sql-server-express"></a>SQL Server Express  
  
#### <a name="full-version-of-sql-server-management-studio-available-in-sql-server-2012-express-sp1"></a>SQL Server 2012 Express SP1 で完全版の SQL Server Management Studio を使用可能  
SQL Server 2012 Express Service Pack 1 (SP1) リリースには、SQL Server 2012 Management Studio Express の代わりに、以前は SQL Server 2012 の DVD にしか収録されていなかった完全版の SQL Server 2012 Management Studio が含まれています。 SQL Server 2012 Express SP1 をダウンロードしてインストールする方法については、「 [SQL Server 2012 Express Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=267905)」を参照してください。  
  
### <a name="change-data-capture-service-and-designer-for-oracle-by-attunity"></a>Change Data Capture Service for Oracle by Attunity と Change Data Capture Designer for Oracle by Attunity  
  
#### <a name="upgrading-the-cdc-service-and-designer"></a>CDC Service および CDC Designer のアップグレード  
**問題点:** SQL Server 2012 SP1 をインストールする時点で、Change Data Capture Designer for Oracle および Change Data Capture Service for Oracle by Attunity がコンピューターにインストールされている場合、SP1 をインストールしてもこれらのコンポーネントはアップグレードされません。  
  
**回避策:** 次の手順に従って CDC コンポーネントを最新バージョンにアップグレードしてください。  
  
1.  [SQL Server 2012 SP1 Feature Pack ダウンロード ページ](https://go.microsoft.com/fwlink/p/?LinkID=268266)から Change Data Capture Service for Oracle by Attunity の .msi ファイルをダウンロードします。  
  
2.  .msi ファイルを実行します。  
  
### <a name="sql-server-data-tier-application-framework-dacfx"></a>SQL Server Data-Tier Application Framework (DACFx)  
**インプレース アップグレードのサポート**  
  
このバージョンの Data-Tier Application Framework (DACFx) では、以前のバージョンからのインプレース アップグレードがサポートされているので、このリリースにアップグレードする前に以前の DACFx インストールを削除する必要はありません。 今後のリリースの DACFx は、 [ここ](https://msdn.microsoft.com/library/dn702988.aspx)にあります。  
  
**選択的 XML インデックスのサポート**  
  
SQL Server 2012 SP1 には、 [選択的 XML インデックス (SXI)](https://msdn.microsoft.com/598ecdcd-084b-4032-81b2-eed6ae9f5d44)のサポートが含まれています。これは SQL Server の新機能であり、高いパフォーマンスと効率で XML 列データのインデックスを作成できます。  
  
DACFx は、すべての DAC シナリオとクライアント ツールで、SXI インデックスをサポートするようになりました。 SXI がサポートされるのは、最新のバージョンの SSDT のみです。 SSDT RTM バージョンおよび September 2012 バージョンでは、SXI はサポートされません。  
  
**ネイティブ BCP データ形式のサポート**  
  
以前は、テーブル データを DACPAC パッケージおよび BACPAC パッケージ内に格納するために使用されるデータ形式は JSON でした。 今回の更新により、データ保存形式がネイティブ BCP になりました。 この変更によって、SQL_Variant 型のサポートなど、DACFx に対する SQL Server データ型の忠実度が向上し、大規模なデータベースのデータ配置のパフォーマンスが強化されました。  
  
**パッケージの作成/配置時における CHECK 制約状態の保持**  
  
従来、DACFx はデータベース スキーマ内のテーブルで定義された CHECK 制約の状態 (WITH CHECK/NOCHECK) を保持せず、この情報を DACPAC 内に格納しませんでした。 この動作により、CHECK 制約に違反している既存のテーブル データがある場合に、パッケージ配置の問題が発生することがありました。 今回の更新により、DACFx が現在の CHECK 制約の状態を、データベースから抽出するときに DACPAC 内に格納し、パッケージの配置時に適切に復元するようになりました。  
  
**SqlPackage.exe (DACFx コマンド ライン ツール) に対する更新**  
  
-   データを含む DACPAC の抽出 - データベース スキーマの他にユーザー テーブルのデータを含むライブ SQL Server または Azure SQL Database から、データベース スナップショット ファイル (.dacpac) を作成します。 これらのパッケージは、SqlPackage.exe の Publish 操作を使用して、新規または既存の SQL Server または Azure SQL Database にパブリッシュできます。 パッケージに含まれているデータによって、ターゲット データベースの既存のデータは置き換えられます。  
  
-   BACPAC のエクスポート - オンプレミスの SQL Server から Azure SQL Database へのデータベースの移行に使用できる、データベース スキーマおよびユーザー データを含むライブ SQL Server または Azure SQL Database の論理バックアップ ファイル (.bacpac) を作成します。 サポートされているバージョンの SQL Server 間で、Azure と互換性のあるデータベースをエクスポートし、後でインポートできます。  
  
-   BACPAC のインポート - .bacpac ファイルをインポートして、SQL Server または Azure SQL Database を新規に作成したり、空のデータベースにデータを入力したりできます。  
  
SqlPackage.exe の完全なドキュメントは、MSDN の [ここ](https://msdn.microsoft.com/library/hh550080%28v=vs.103%29.aspx)にあります。  
  
**パッケージの互換性**  
  
今回のリリースでは、DAC パッケージの上位互換性シナリオが複数導入されています。  
  
-   今回のリリースで作成された、SXI 要素もテーブル データも含まない DAC パッケージは、以前のリリースの DACFx (SQL Server 2012 RTM、SQL Server 2012 CU1、および DACFx September 2012) で使用できます。  
  
-   以前のバージョンの DACFx で作成されたすべての DAC パッケージを、このリリースで使用できます。  
  
## <a name="see-also"></a>参照
- [SQL Server 2012 サービス更新プログラムのインストール](https://msdn.microsoft.com/library/hh479746(v=sql.110).aspx)
- [SQL Server のバージョンとエディションを識別する方法](https://support.microsoft.com/help/321185)
- [SQL Server 2012 サービス更新プログラムのインストール](https://msdn.microsoft.com/library/hh479746(v=sql.110).aspx)
- [SQL Server のバージョンとエディションを識別する方法](https://support.microsoft.com/help/321185) 
- [SQL Server のバージョンとエディションを確認する方法](https://support.microsoft.com/kb/321185)  
- [SQL Server 2014 の各エディションがサポートする機能](https://msdn.microsoft.com/5da61ff5-12b9-48e6-b3c8-0dacca1751c4)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
