---
title: サーバー インスタンスでのフルテキスト検索の管理と監視 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], about
- full-text search [SQL Server], server management
ms.assetid: 2733ed78-6d33-4bf9-94da-60c3141b87c8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a6ed18416eadf1c2cc664029588bf0201038c261
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011169"
---
# <a name="manage-and-monitor-full-text-search-for-a-server-instance"></a>サーバー インスタンスでのフルテキスト検索の管理と監視
  サーバー インスタンスのフルテキスト検索の管理には次の作業があります。  
  
-   FDHOST ランチャー サービス (MSSQLFDLauncher) の管理、サービス アカウント資格情報の変更時のフィルター デーモン ホスト プロセスの再起動、サーバー全体のフルテキスト プロパティの構成、フルテキスト カタログのバックアップなどのシステム管理作業。 たとえば、サーバー レベルでは、サーバー インスタンス全体の既定の言語とは異なる、既定のフルテキスト言語を指定できます。  
  
-   フルテキスト言語コンポーネント (ワード ブレーカーおよびステミング機能、類義語辞典ファイル、ストップワードおよびストップリスト) の構成。  
  
-   フルテキスト検索を行うためのユーザー データベースの構成。 データベース用のフルテキスト カタログを 1 つ以上作成し、フルテキスト クエリを実行する各テーブルまたは各インデックス付きビューにフルテキスト インデックスを定義します。  
  
##  <a name="props"></a> フルテキスト検索のサーバー プロパティを表示および変更する  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのフルテキスト プロパティは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で表示できます。  
  
#### <a name="to-view-and-change-server-properties-for-full-text-search"></a>フルテキスト検索のサーバー プロパティを表示および変更するには  
  
1.  オブジェクト エクスプローラーでサーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[サーバーのプロパティ]** ダイアログ ボックスで、 **[詳細設定]** ページをクリックし、フルテキスト検索に関するサーバーの情報を表示します。 フルテキスト プロパティは次のとおりです。  
  
    -   **[既定のフルテキスト言語]**  
  
         フルテキスト インデックス列に、既定の言語を指定します。 フルテキスト インデックス データの言語の分析は、データの言語に依存します。 このオプションの既定値は、サーバーの言語です。 表示される設定に対応する言語については、「[sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)」をご覧ください。  
  
    -   **フルテキスト アップグレード オプション**  
  
         このサーバー プロパティは、データベースを [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] から新しいバージョンにアップグレードする際のフルテキスト インデックスの移行方法を制御します。 このプロパティは、データベースのインポート、データベース バックアップの復元、ファイル バックアップの復元、またはデータベース コピー ウィザードを使用したデータベースのコピーによってアップグレードする場合に適用されます。  
  
         選択肢は次のとおりです。  
  
         **[インポート]**  
         フルテキスト カタログがインポートされます。 通常、インポートの方が再構築よりもかなり高速に処理されます。 たとえば、CPU を 1 つだけ使用している場合、インポートは、再構築の約 10 倍の速さで実行されます。 ただし、インポートされたフルテキスト カタログでは、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]で導入された新しい拡張機能であるワード ブレーカーが使用されません。そのため、最終的にはフルテキスト カタログの再構築が必要になることがあります。  
  
        > [!NOTE]  
        >  再構築はマルチスレッド モードで実行できます。10 を超える CPU が使用可能な場合に、再構築でそれらの CPU をすべて使用できるようにすると、再構築の方がインポートよりも高速に実行されることがあります。  
  
         フルテキスト カタログが使用できない場合は、関連付けられたフルテキスト インデックスが再構築されます。 このオプションは [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] データベースでのみ使用できます。  
  
         **Rebuild**  
         フルテキスト カタログは、導入された新しい拡張機能であるワード ブレーカーを使用して再構築されます。 インデックスの再構築には時間がかかり、アップグレード後にかなりの量の CPU とメモリが必要になる可能性があります。  
  
         **リセット**  
         フルテキスト カタログがリセットされます。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のフルテキスト カタログ ファイルは削除されますが、フルテキスト カタログのメタデータおよびフルテキスト インデックスは保持されます。 アップグレード後、すべてのフルテキスト インデックスで変更の追跡は無効化されており、クロールは自動的には開始されません。 アップグレードの完了後、手動で完全作成を実行するまで、カタログは空のままになります。  
  
         フルテキスト アップグレード オプションを選択する方法の詳細については、次を参照してください。 [、フルテキスト検索のアップグレード](upgrade-full-text-search.md)します。  
  
        > [!NOTE]  
        >  フルテキスト アップグレード オプションは、[sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql) の **upgrade_option** 操作を使用して設定することもできます。  
  
##  <a name="metadata"></a> その他のフルテキスト サーバー プロパティの表示  
 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 関数を使用すると、フルテキスト検索のさまざまなサーバー レベルのプロパティの値を取得できます。 この情報は、フルテキスト検索の管理およびトラブルシューティングに役立ちます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サーバー インスタンスのフルテキスト プロパティと各プロパティに関連する [!INCLUDE[tsql](../../../includes/tsql-md.md)] 関数の一覧を次の表に示します。  
  
|プロパティ|説明|機能|  
|--------------|-----------------|--------------|  
|`IsFullTextInstalled`|フルテキスト コンポーネントが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の現在のインスタンスと共にインストールされているかどうかを示します。|[FULLTEXTSERVICEPROPERTY](/sql/t-sql/functions/fulltextserviceproperty-transact-sql)<br /><br /> [SERVERPROPERTY](/sql/t-sql/functions/serverproperty-transact-sql)|  
|`LoadOSResources`|オペレーティング システムのワード ブレーカーやフィルターが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに登録され、使用されているかどうかを示します。|FULLTEXTSERVICEPROPERTY|  
|`VerifySignature`|Full-Text Engine に署名付きバイナリのみを読み込むかどうかを指定します。|FULLTEXTSERVICEPROPERTY|  
  
##  <a name="monitor"></a> フルテキスト検索の利用状況の監視  
 サーバー インスタンスでのフルテキスト検索の実行状況を監視する場合は、以下の動的管理ビューと関数が役立ちます。  
  
 **作成操作が進行中のフルテキスト カタログに関する情報を表示するには**  
  
-   [sys.dm_fts_active_catalogs &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql)  
  
 **フィルター デーモン ホスト プロセスの現在の実行状況を表示するには**  
  
-   [sys.dm_fts_fdhosts &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql)  
  
 **進行中のインデックス作成に関する情報を表示するには**  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)  
  
 **クロールまたはクロール範囲の一部として使用される、メモリ プールのメモリ バッファーを表示するには**  
  
-   [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql)  
  
 **フルテキスト クロールまたはフルテキスト クロール範囲でフルテキスト Gatherer コンポーネントに使用できる共有メモリ プールを表示するには**  
  
-   [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql)  
  
 **各フルテキスト インデックス バッチに関する情報を表示するには**  
  
-   [sys.dm_fts_outstanding_batches &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql)  
  
 **進行中の作成に関連する特定の範囲についての情報を表示するには**  
  
-   [sys.dm_fts_population_ranges &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql)  
  
  
