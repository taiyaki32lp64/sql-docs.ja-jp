---
title: 管理データ ウェアハウス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collector [SQL Server], management data warehouse
- data warehouse
- management data warehouse
ms.assetid: 9874a8b2-7ccd-494a-944c-ad33b30b5499
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8723d9750eb03eda14a7983cba8919ea8e92eb81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133619"
---
# <a name="management-data-warehouse"></a>管理データ ウェアハウス (management data warehouse)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  管理データ ウェアハウスは、データ コレクションの対象であるサーバーから収集されたデータを格納するリレーショナル データベースです。 このデータは、システム データ コレクション セットのレポートを生成するために使用され、カスタム レポートを作成する際にも使用できます。  
  
 データベース管理者が定義した保有ポリシーを実装するために必要なジョブやメンテナンス プランは、データ コレクターのインフラストラクチャによって定義されます。  
  
> [!IMPORTANT]  
>  このリリースのデータ コレクターでは、ログ記録を最小限に抑えるため、単純復旧モデルを使用して管理データ ウェアハウスが作成されます。 組織に適した復旧モデルを実装する必要があります。  
  
## <a name="deploying-and-using-the-data-warehouse"></a>データ ウェアハウスの配置と使用  
 管理データ ウェアハウスは、データ コレクターを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスと同じインスタンスにインストールできます。 ただし、監視中のサーバーでサーバー リソースやパフォーマンスが問題となっている場合は、別のコンピューターに管理データ ウェアハウスをインストールできます。  
  
 事前に定義されたシステム コレクション セットに必要なスキーマとそのオブジェクトは、管理データ ウェアハウス作成時に作成されます。 作成されるスキーマは、core と snapshots です。3 つ目のスキーマである custom_snapshots は、ジェネリック T-SQL Query コレクター型を使用するコレクション アイテムを含んだユーザー定義のコレクション セットの作成時に作成されます。  
  
###### <a name="core-schema"></a>core スキーマ  
 core スキーマでは、収集したデータの編成と識別に使用するテーブル、ストアド プロシージャ、およびビューが記述されます。 これらのテーブルは、個々のコレクター型ごとに作成されるすべてのデータ テーブルで共有されます。 このスキーマはロックされており、変更できるのは管理データ ウェアハウスのデータベースの所有者だけです。 このスキーマに記述されるテーブルは、名前の先頭に "core" が付加されます。  
  
 次の表では、core スキーマ内のデータベース テーブルについて説明します。 データ コレクターは、これらのデータベース テーブルで、データの出所、挿入者、データ ウェアハウスにアップロードされた時刻を追跡できます。  
  
|テーブル名|[説明]|  
|----------------|-----------------|  
|core.performance_counter_report_group_items|管理データ ウェアハウスのレポートがパフォーマンス カウンターをグループ化および集計する方法に関する情報を格納します。|  
|core.snapshots_internal|それぞれの新しいスナップショットを識別します。 アップロード パッケージによってデータの新しいバッチのアップロードが開始されるたびに、このテーブルに新しい行が挿入されます。|  
|core.snapshot_timetable_internal|スナップショット時間に関する情報を格納します。 多数のスナップショットがほぼ同時に発生する可能性があるため、スナップショット時間は別のテーブルに格納されます。|  
|core.source.info_internal|このテーブルは、データ ソースに関する情報を格納します。 新しいコレクション セットからデータ ウェアハウスへのデータのアップロードが開始されるたびに更新されます。|  
|core.supported_collector_types_internal|管理データ ウェアハウスにデータをアップロードできる、登録済みのコレクター型の ID を格納します。 このテーブルが更新されるのは、新しいコレクター型のサポートのためウェアハウスのスキーマが更新された場合だけです。 管理データ ウェアハウスの作成時に、データ コレクターで提供されるコレクター型の ID がこのテーブルに設定されます。|  
|core.wait_categories|wait_type 特性に従って待機の種類を分類するために使用されるカテゴリを格納します。|  
|core.wait_types|データ コレクターで認識される待機の種類を格納します。|  
|core.purge_info_internal|管理データ ウェアハウスのデータ削除を停止する要求が行われたことを示します。|  
  
 上記のテーブルは、コレクター型テーブルと共に情報を格納するために使用されます。 たとえば、ジェネリック SQL トレース コレクター型は、次のテーブルを使用してトレース データを格納します。  
  
-   core.source_info_internal  
  
-   core.snapshots_internal  
  
-   snapshots.trace_info  
  
-   snapshots.trace_data  
  
###### <a name="snapshots-schema"></a>snapshots スキーマ  
 snapshots スキーマでは、提供されているコレクター型で収集されるデータの格納と保持に必要なオブジェクトが記述されます。 このスキーマのテーブルは固定であり、コレクター型の有効期間中に変更する必要はありません。 変更が必要な場合、スキーマを変更できるのは mdw_admin ロールのメンバーだけです。 このテーブルは、システム データ コレクション セットによって収集されたデータを格納するために作成されます。  
  
 次の表は、管理データ ウェアハウス スキーマの、サーバー利用状況コレクション セットとクエリ統計情報コレクション セットに必要な部分を示しています。  
  
-   システム レベルのリソースのテーブル  
  
    -   **snapshots.os_wait_stats**  
  
    -   **snapshots.os_latch_stats**  
  
    -   **snapshots.os_schedulers**  
  
    -   **snapshots.os_memory_clerks**  
  
    -   **snapshots.os_memory_nodes**  
  
    -   snapshots.sql_process_and_system_memory  
  
-   システムの利用状況  
  
    -   snapshots.active_sessions_and_requests  
  
-   クエリ統計情報  
  
    -   snapshots.query_stats  
  
-   I/O 統計  
  
    -   **snapshots.io_virtual_file_stats**  
  
-   クエリ テキストとクエリ プラン  
  
    -   snapshots.notable_query_text  
  
    -   snapshots.notable_query_plan  
  
-   正規化されたクエリ統計  
  
    -   snapshots.distinct_queries  
  
    -   snapshots.distinct_query_to_handle  
  
 **custom_snapshots スキーマ**  
  
 custom_snapshots スキーマでは、標準のコレクター型またはサード パーティのコレクター型を使用してユーザー定義のコレクション セットを作成するときに作成される新しいテーブルとビューが記述されます。 コレクション アイテム用の新しいデータ テーブルを必要とするコレクター型がある場合は、このスキーマにそのテーブルを作成できます。 このスキーマに新しいテーブルを追加できるのは、mdw_writer ロールのメンバーです。 スキーマにそれ以外の変更を加えられるのは、mdw_admin ロールのメンバーだけです。  
  
 データベース テーブルの列のデータ型とコンテンツの詳細情報については、各テーブルに適したデータ コレクターのストアド プロシージャに関するマニュアルの記述を参照してください。  
  
### <a name="best-practices"></a>ベスト プラクティス  
 管理データ ウェアハウスの操作に関して推奨するベスト プラクティスを次に示します。  
  
-   新しいコレクター型を追加する場合を除き、管理データ ウェアハウスのテーブルのメタデータは変更しないでください。  
  
-   管理データ ウェアハウスのデータは直接変更しないでください。 収集済みのデータに変更を加えると、収集したデータの正当性がなくなります。  
  
-   インスタンスとアプリケーション データにアクセスするには、テーブルを直接使用する代わりに、データ コレクターで提供される、ドキュメントに記載のストアド プロシージャと関数を使用してください。 テーブル名と定義は変更できます。これらは、アプリケーションを更新するときには必ず変更してください。テーブル名と定義は、将来のリリースでは変更される可能性がある情報です。  
  
## <a name="change-history"></a>変更履歴  
  
|変更内容|  
|---------------------|  
|「core スキーマ」セクションに core.performance_counter_report_group_items テーブルを追加しました。|  
|「snapshots スキーマ」セクションのテーブルの一覧を更新しました。 snapshots.os_memory_clerks、snapshots.sql_process_and_system_memory、および snapshots.io_virtual_file_stats を追加しました。 snapshots.os_process_memory および snapshots.distinct_query_stats を削除しました。|  
  
## <a name="see-also"></a>参照  
 [管理データ ウェアハウスのストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/management-data-warehouse-stored-procedures-transact-sql.md)   
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [データ コレクション](../../relational-databases/data-collection/data-collection.md)   
 [コレクション セット レポートの表示 &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)  
  
  
