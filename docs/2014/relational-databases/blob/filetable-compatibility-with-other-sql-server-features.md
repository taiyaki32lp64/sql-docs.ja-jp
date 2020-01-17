---
title: FileTable と他の SQL Server 機能の互換性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], using with other features
ms.assetid: f12a17e4-bd3d-42b0-b253-efc36876db37
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c8ea6a5fcfe99926c264fc2116a637f8d30c05df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010151"
---
# <a name="filetable-compatibility-with-other-sql-server-features"></a>FileTable と他の SQL Server 機能の互換性
  FileTable と他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]機能との連携について説明します。  
  
##  <a name="alwayson"></a> AlwaysOn 可用性グループと FileTable  
 FILESTREAM データまたは FileTable データを格納するデータベースが AlwaysOn 可用性グループに属する場合、次の処理が行われます。  
  
-   FileTable 機能は [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]で部分的にサポートされています。 フェールオーバー後、FileTable データはプライマリ レプリカ上でアクセスできますが、読み取り可能なセカンダリ レプリカ上ではアクセスできません。  
  
    > [!NOTE]  
    >  フェールオーバー後はすべての FILESTREAM 機能がサポートされることに注意してください。 FILESTREAM データは読み取り可能なセカンダリ レプリカと新しいプライマリの両方でアクセスできます。  
  
-   FILESTREAM および FileTable 関数は、コンピューター名ではなく仮想ネットワーク名 (VNN) のやり取りを行います。 関数の詳細については、「[Filestream および FileTable 関数 &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filestream-and-filetable-functions-transact-sql)」を参照してください。  
  
-   ファイル システム API を介した FILESTREAM または FileTable データへのすべてのアクセスでは、コンピューター名ではなく VNN を使用する必要があります。 詳細については、「[FILESTREAM および FileTable と AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)」を参照してください。  
  
##  <a name="OtherPartitioning"></a> パーティション分割と FileTable  
 FileTable ではパーティション分割はサポートされていません。 複数の FILESTREAM ファイル グループのサポートにより、ほとんどのシナリオにおいて、(SQL 2008 FILESTREAM とは異なり) パーティション分割に頼ることなく純粋なスケールアップに関する問題を処理できます。  
  
##  <a name="OtherRepl"></a> レプリケーションと FileTable  
 FileTable では、レプリケーションおよび関連機能 (トランザクション レプリケーション、マージ レプリケーション、変更データ キャプチャ、および変更の追跡) はサポートされていません。  
  
##  <a name="OtherIsolation"></a> トランザクション セマンティクスと FileTable  
 **Windows アプリケーション**  
 Windows アプリケーションはデータベース トランザクションを理解しないため、Windows 書き込み操作ではデータベース トランザクションの ACID プロパティが提供されません。 このため、Windows の更新操作ではトランザクションのロールバックと復旧は不可能です。  
  
 **Transact-SQL アプリケーション**  
 FileTable の FILESTREAM (file_stream) 列を操作する TSQL アプリケーションの分離セマンティクスは、通常のユーザー テーブル内の FILESTREAM データ型の場合と同じです。  
  
##  <a name="OtherQueryNot"></a> クエリ通知と FileTable  
 クエリでは、WHERE 句またはクエリのその他の部分に FileTable 内の FILESTREAM 列への参照を含めることはできません。  
  
##  <a name="OtherSelectInto"></a> SELECT INTO と FileTable  
 FileTable から SELECT INTO ステートメントを使用すると、(通常のテーブルの FILESTREAM 列と同様に) FileTable のセマンティクスはターゲット テーブルに反映されません。 ターゲット テーブルのすべての列が通常の列と同じように動作します。 FileTable のセマンティクスはターゲット テーブルの列に関連付けられません。  
  
##  <a name="OtherTriggers"></a> トリガーと FileTable  
 **DDL (データ定義言語) トリガー**  
 DDL トリガーと FileTable の使用については、特別な注意事項はありません。 FileTable に対する CREATE/ALTER TABLE 操作だけでなく、データベースの作成/変更操作でも、通常の DDL トリガーが起動されます。 トリガーは、EVENTDATA() 関数を呼び出すことによって、DDL コマンド テキストやその他の情報などの実際のイベント データを取得できます。 新しいイベントや既存の Eventdata スキーマに対する変更はありません。  
  
 **DML (データ操作言語) トリガー**  
 トリガーを作成するための DDL 操作において、以下の制限が適用されます。  
  
-   FileTable では、DML 操作のための INSTEAD OF トリガーはサポートされません。 これは、FILESTREAM 列を含むすべてのテーブルに対する既存の制限です。  
  
-   FileTable では、DML 操作用に AFTER トリガーがサポートされます。  
  
-   FileTable で定義されたトリガーは、(親 FileTable を含む) すべての FileTable を更新できません。 この制限は、主に、トリガーが同じトランザクション内でファイル システムによって保持されているロックとの間でロックの競合を起こすことを防止するために設定されています。  
  
 **非トランザクション アクセスとトリガーに対するその影響**  
 -   データベースで非トランザクション更新アクセスが許可されている場合は、そのデータベース内の FileTable を含む任意のテーブルで、FILESTREAM データのインプレース更新を行うことができます。 このため、FILESTREAM の内容の前イメージをトリガーで使用できない場合があります。  
  
-   ファイル システムを介した非トランザクション更新操作のために、SQL Server は内部トランザクションを作成し、CloseHandle 操作をキャプチャします。このトランザクションの一部として、任意の定義済み DML トリガーを起動できます。 トリガー内部でトランザクションのロールバックを行うことは可能ですが、FILESTREAM に対する変更はロールバックされません。  このようなロールバックによって、FILESTREAM の内容が変更されている場合でも、更新トリガーが起動されないことがあります。  
  
-   これらの影響以外にも、FileTable のトリガーで、以下の 2 つの動作に対処する必要があります。  
  
    -   ファイル システムを介した FileTable に対する非トランザクション更新操作の場合、FILESTREAM の内容が他の Win32 操作によって排他的にロックされ、トリガー内部からの読み取り/書き込みアクセスができなくなることがあります。 このような場合は、通常、トリガー内部で FILESTREAM の内容にアクセスしようとすると、"共有違反" エラーになります。 このようなエラーを適切に処理するようにトリガーを設計する必要があります。  
  
    -   (ファイル システム アクセスで許可されている共有モードのために) 他の非トランザクション更新によって FILESTREAM へのアクティブな書き込みが同時に行われることがあるので、FILESTREAM の後イメージが安定しない場合があります。  
  
-   Win32 ハンドルの異常終了 (管理者による Win32 ハンドルの明示的な終了、データベースのクラッシュなど) が生じた場合、異常終了した Win32 アプリケーションによって FILESTREAM の内容が変更されていた可能性がありますが、復旧操作中にユーザー トリガーは実行されません。  
  
##  <a name="OtherViews"></a> ビューと FileTable  
 **ビュー**  
 他のテーブルの場合と同様に、FileTable にもビューを作成できます。 ただし、FileTable にビューを作成する場合は、次の点に注意してください。  
  
-   ビューには FileTable のセマンティクスがありません。 つまり、(ファイル属性列を含めて) ビュー内の列は、特殊なセマンティクスを持たない通常のビュー列と同じように動作します。これは、ファイルやディレクトリを表す行の場合も同じです。  
  
-   ビューは、"更新可能なビュー" セマンティクスに基づいて更新できますが、基になるテーブルの制約により、テーブル内の場合と同様に更新が拒否されることがあります。  
  
-   ビューの明示的な列にファイル パスを追加することにより、ファイルのファイル パスをビューに視覚化することができます。 例 :  
  
     `CREATE VIEW MP3FILES AS SELECT column1, column2, ..., GetFileNamespacePath() AS PATH, column3,...  FROM Documents`  
  
 **インデックス付きビュー**  
 現在インデックス付きのビューには、FILESTREAM 列に依存する FILESTREAM 列、計算列、または保存される計算列を含めることはできません。 この動作は、FileTable に定義されているビューでも同じです。  
  
##  <a name="OtherSnapshots"></a> スナップショット分離と FileTable  
 Read Committed スナップショット分離 (RCSI) およびスナップショット分離 (SI) は、データの更新操作が行われているときでもリーダーによるデータのスナップショットの利用を可能にする機能に依存します。 ただし、FileTable では、Filestream データに対する非トランザクション書き込みアクセスが可能です。 その結果、FileTable を含むデータベースでのこれらの機能の使用に関して、次の制限が適用されます。  
  
-   FileTable を含むデータベースは、RCSI/SI を有効にするように変更できます。  
  
-   データベースに対する non_transactional アクセスを FULL に設定した場合、RCSI または SI で実行されるトランザクションは次のように動作します。  
  
    -   FileTable file_stream 列に対するすべての [!INCLUDE[tsql](../../../includes/tsql-md.md)] 読み取りは失敗します。 列に対する INSERT および UPDATE は、file_stream 列からの読み取りを行わない限り正常に実行されます。  
  
    -   [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントに READCOMMITTEDLOCK テーブル ヒントが指定されている場合、読み取りは正常に実行されます。このとき、行のバージョン管理の代わりに、行のロックが設定されます。  
  
    -   トランザクション Win32 FileStream を開く要求も失敗します。  
  
    -   非トランザクション FileTable Win32 アクセスは正常に実行されます。 FileTable によって実行されるすべての内部クエリは影響を受けません。  
  
    -   フルテキスト インデックス作成は、どのデータベース オプション (READ_COMMITTED_SNAPSHOT または ALLOW_SNAPSHOT_ISOLATION) が指定された場合でも常に正常に実行されます。  
  
##  <a name="readsec"></a> 読み取り可能なセカンダリ データベース  
 前のセクション「 [スナップショット分離と FileTable](#OtherSnapshots)」で説明したとおり、読み取り可能なデータベースには、スナップショットに対するのと同じ考慮事項が適用されます。  
  
##  <a name="CDB"></a> 包含データベースと FileTable  
 FileTable 機能が依存する FILESTREAM 機能では、データベースの外部での構成が一部必要となります。 そのため、FILESTREAM または FileTable を使用するデータベースは完全包含ではありません。  
  
 包含データベースの特定の機能 (包含ユーザーなど) を使用する場合は、データベースの包含を PARTIAL に設定します。 ただし、この場合、一部のデータベース設定はデータベースに含まれないため、データベースを移動するときに自動的には移動されないことに注意してください。  
  
## <a name="see-also"></a>参照  
 [FileTable の管理](manage-filetables.md)  
  
  
