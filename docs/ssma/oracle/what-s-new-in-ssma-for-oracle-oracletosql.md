---
title: SSMA for Oracle の新機能 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 12/04/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: f196932ee9a37c9a814ad619b604520093b6098d
ms.sourcegitcommit: 26868c8ac3217176b370d972a26d307598a10328
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74834283"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>SSMA for Oracle の新機能 (OracleToSQL)

この記事では、各リリースでの Oracle の変更の SQL Server Migration Assistant (SSMA) を示します。

## <a name="ssma-v85"></a>SSMA v1.0

SSMA for Oracle の v2.0 リリースは、SQL server での JSON 機能の Azure Active Directory 認証と基本的なサポートがサポートされるようになり、使いやすさとパフォーマンスの向上を目的とした一連の修正が加えられました。

さらに、SSMA for Oracle では、次のサポートが強化されています。

* 探索対象として選択したオブジェクトの数を990に制限する [Oracle] IN (..) "句 limit は 1000 items] です。
* 生から UNIQUEIDENTIFIER へのデータ移行。
* PARALLEL_ENABLE 句を解析しています。

最後に、SSMA for Oracle の v1.0 リリースでは、次の機能が提供されるようになりました。

* 変換されたパッケージ定数のパフォーマンスの向上
* .NET 用の Oracle Data Provider バージョン19.5.0 の更新プログラム

> [!IMPORTANT]
> SSMA v1.0 では、.Net 4.7.2 はインストールの前提条件です。 このバージョンをインストールする必要がある場合は、[ここ](https://dotnet.microsoft.com/download/dotnet-framework/net472)からランタイムファイルをダウンロードできます。

## <a name="ssma-v84"></a>SSMA v 8.4

SSMA for Oracle の v2.0 リリースは、ユーザー補助の問題に対処し、最大インデックス列 (16 ではなく 32) に関連するバグを修正するように設計された、SQL Server 2016 以降のバージョンで強化されています。

また、SSMA for Oracle のこのリリースでは、ストアドプロシージャ OUT パラメーターとして**SYS_REFCURSOR**の変換が追加されています。

> [!IMPORTANT]
> SSMA バージョン 7.4 ~ 8.4 の場合、.Net 4.5.2 はインストールの前提条件です。

## <a name="ssma-v83"></a>SSMA v 8.3

SSMA for Oracle の v2.0 リリースは、品質と変換のメトリックを向上させるように設計された対象の修正によって強化されています。 また、SSMA for Oracle のこのリリースでは、次のような修正が行われています。

* アクセシビリティに関する問題の解決
* SQL Server に ' hierarchyid ' 型の基本的なサポートを追加します
* シノニムによって呼び出された関数の戻り値の型が不明な問題を解決する
* ODP.NET を v 19.3 に更新する

## <a name="ssma-v82"></a>SSMA v 8.2

SSMA for Oracle の v2.0 リリースは次のように強化されています。

* DBMS_OUTPUT のサポートを追加します。有効/無効を切り替える。
* 既定のデータ移行クエリで、BINARY_FLOAT と BINARY_DOUBLE 列のキャストを FLOAT として削除します。
* 現在の値が変更された場合は、シーケンスの更新を修正します。
* 同じ名前の列が存在する場合は、擬似列 (ROWNUM など) の誤った解釈に関連するバグを修正します。
* あいまいな未解決の識別子を持つループの変換が発生するクラッシュを修正します。

さらに、このバージョンには、品質と変換のメトリックを改善するために設計された修正プログラムのセットと、次のような修正が含まれています。

* データ移行後の非クラスター化インデックスが無効になっている問題。
* サイレントインストール中の .NET Framework の検出。
* 新しいバージョンがダウンロードされると発生する断続的なクラッシュ。

> [!NOTE]
> 自動更新に関する既知の問題により、SSMA v2.0 から v2.0 への更新が失敗する場合があります。 このエラーが発生した場合は、新しいバージョンをダウンロードし、手動でインストールしてください。

## <a name="ssma-v81"></a>SSMA v 8.1

SSMA for Oracle の v2.0 リリースは、品質と変換のメトリックを向上させるように設計された対象の修正によって強化されています。

> [!NOTE]
> 自動更新に関する既知の問題により、SSMA v2.0 から v2.0 への更新が失敗する場合があります。 このエラーが発生した場合は、新しいバージョンをダウンロードし、手動でインストールしてください。

## <a name="ssma-v80"></a>SSMA 8.0

SSMA for Oracle の v2.0 リリースは、品質と変換メトリックの向上を目的とした修正プログラムによって強化されています。 このリリースには、次の新機能も用意されています。

* ターゲットとしての**Azure SQL Database Managed Instance**のサポート。 Azure SQL Database Managed Instance をターゲットとする新しいプロジェクトを作成できるようになりました。

  ![SQL DB MI プロジェクト](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > SSMA for Oracle 拡張パックも更新され、Azure SQL Database Managed Instance でのリモートインストールが可能になりました。
  >
  > ![SSMA for Oracle Extension Pack](../media/ssma-oracle-ext-pack.png)

  テスト担当者やサーバー側のデータの移行など、一部の機能は Azure SQL Database Managed Instance を対象としている場合はサポートされません。 詳細については、[こちら](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/)を参照してください。

* 変換後の**修正アドバイザー**。 詳細について[は、こちら](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)を参照してください。

* データベース/スキーマの事前選択。

  ソースに接続するときに、ユーザーは目的のデータベースまたはスキーマを選択できるようになりました。 移行を計画しているスキーマのみを選択すると、初期接続時に時間が節約され、全体的な SSMA パフォーマンスが向上します。

  ![SSMA フィルターオブジェクト](../media/ssma-filter-objects.png)

* 公式の管理対象 NET ドライバーを使用して Oracle に接続する機能。 OCI ドライバーは、Oracle の SQL Server Migration Assistant を使用するための前提条件ではなくなりました。

* 既定では、ROWID と UROWID を VARCHAR にマップする機能です。 明示的な ROWID 列のデータ移行に対応するように ' uniqueidentifier ' から変更されました。

## <a name="ssma-v710"></a>SSMA v 7.10

SSMA for Oracle のバージョン7.10 リリースには、次の変更が含まれています。

* グローバル要件の変化に対応するために、追加のセキュリティとプライバシーの保護を提供するように設計された修正。
* 階層クエリに関連する変換の改善。

## <a name="ssma-v79"></a>SSMA v 7.9

SSMA for Oracle の v1.0 リリースには、次の変更が含まれています。

* 品質と変換のメトリックを向上させる対象の修正。
* Oracle から SQL Server への "Continue" ステートメントの移行のサポート。
* SSMA コマンドラインでデータ型マッピングとプロジェクト設定を変更するためのサポート。
* SQL Server Integration Services (SSIS) を使用したデータ移行のサポート。 スキーマを変換した後、右クリックコンテキストメニューオプションを使用して SSIS パッケージを作成できます。
* SSMA の [Azure SQL Database 接続] ダイアログも、完全修飾サーバー名を指定するように変更されています。 以前のバージョンの SSMA では、プロジェクト設定内で Azure SQL Database プレフィックスを明示的に記述する必要がありました。

## <a name="ssma-v78"></a>SSMA v 7.8

SSMA for Oracle の v1.0 リリースには、次の変更が含まれています。

* のサポート:
  * IN 句の行式。
  * 暗黙的な型キャストです。
  * Azure SQL Database の UID 変換。
* [プロジェクトの設定] で強調表示されている型マッピングを変更します。
* ユーザーがテレメトリを無効にする機能。

## <a name="ssma-v77"></a>SSMA v 7.7

SSMA for Oracle のバージョン7.7 リリースには、次の変更が含まれています。

* SSMA for Oracle は、品質と変換のメトリックを向上させる対象の修正によって強化されています。
* 一般的な要求に基づいて、SSMA for Oracle の32ビットバージョンが返されます。 以前の実装と比較して (v2.0 より前)、インストーラーパッケージは2つありますが、サイドバイサイドでインストールすることはできません。 そのため、使用している接続コンポーネントに基づいて、最適なバージョンを選択する必要があります。 可能であれば、常に64ビットバージョンを使用することをお勧めします。
* SQL Server 2017 のサポートが、Linux でサポートされている Oracle 拡張パック (新しいリモートインストールオプション) で公式になりました。 テスト担当者とサーバー側のデータ移行機能はサポートされていないため、Linux にインストールされている場合は拡張パックの機能が制限されていることに注意してください。
* Ssma for Oracle では、具体化されたビューを通常のテーブルとして移行できます ([**プロジェクト設定** -> の**同期** -> ] の設定で構成できます)。具体化された**ビューのバッキングテーブルを検出**します。

## <a name="ssma-v76"></a>SSMA v1.0

SSMA for Oracle の v1.1 リリースは、品質と変換のメトリックを向上させ、SQL Server 2017 (パブリックプレビュー) をサポートする対象の修正によって強化されています。 Windows および Linux での SQL Server 2017 のサポートはパブリックプレビュー段階であり、運用環境への移行には使用しないでください。

## <a name="ssma-v75"></a>SSMA v 7.5

SSMA for Oracle の version 7.5 リリースには、次の変更が含まれています。

* 障碍のある方にとってアクセシビリティを向上させるために、いくつかの機能強化が施されました。
* 顧客からのフィードバックに基づいて、データ移行中の日付データ型と float データ型の処理の改善など、対象の修正によって品質と変換のメトリックが向上しました。

## <a name="ssma-v74"></a>SSMA v1.0

SSMA for Oracle の v2.0 リリースには、次の変更が含まれています。

* SSMA for Oracle では、移行のターゲットプラットフォームとして Azure SQL Data Warehouse がサポートされるようになりました。

  ![[新しいプロジェクト] ウィンドウ](../media/new-project.png)
  * では、次の図に示すように、データウェアハウスのストレージオプションがサポートされています。

  ![データウェアハウスのストレージオプション](../media/storage-options_red.png)
  * では、次の図に示すように、データ分散オプションがサポートされています。

  ![データウェアハウスのデータ分散](../media/data-distribution_red.png)

* [**クエリタイムアウト**] オプションは、ソースおよびターゲットでのスキーマオブジェクトの検出中に使用できるようになりました。

  ![クエリタイムアウトオプション](../media/query-timeout_red.png)

* お客様からのフィードバックに基づいて、品質と換算のメトリックが修正されました。

> [!IMPORTANT]
> .Net 4.5.2 は、SSMA v2.0 をインストールするための前提条件です。 さらに、v2.0 以降では、SSMA の32ビットバージョンは廃止されています。

## <a name="ssma-v73"></a>SSMA version 7.3

SSMA for Oracle の version 7.3 リリースには、次の変更が含まれています。

* お客様からのフィードバックに基づいて、対象の修正を含む品質と変換のメトリックが向上しました。
* SSMA 拡張フレームワークは、次の項目を介して公開されます。
  * SQL Server Data Tools (SSDT) プロジェクトに機能をエクスポートします。
    * SSMA から SSDT プロジェクトにスキーマスクリプトをエクスポートできるようになりました。 スキーマスクリプトを使用すると、追加のスキーマ変更を行ったり、データベースを配置したりすることができます。

      ![SSDT プロジェクトの名前を付けて保存コマンド](../media/export-schema-scripts_red.png)
  * カスタム変換を実行するために SSMA で使用できるライブラリ。
    * SSMA によって以前に処理されなかったカスタム構文変換と変換を処理できるコードを作成できるようになりました。
      * カスタムコンバーターを構築する方法については、このブログの投稿を参照してください。 [SQL Server Migration Assistant の変換機能が拡張](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)されます。
      * この[ブログの投稿](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)から、変換用のサンプルプロジェクトをダウンロードします。

## <a name="ssma-v72"></a>SSMA v 7.2

SSMA for Oracle の v2.0 リリースには、次の変更が含まれています。

* お客様からのフィードバックに基づいて、対象の修正を含む品質と変換のメトリックが向上しました。
* テレメトリの機能強化により、顧客の問題をトラブルシューティングし、SSMA のコンバージョン率を向上させるためのデータポイントが向上しました。

## <a name="ssma-v71"></a>SSMA 7.1

SSMA for Oracle の v2.0 リリースには、次の変更が含まれています。

* Windows と Linux CTP1 の SQL Server 2017 は、現在、移行のためにサポートされているターゲットプラットフォームです。 この機能は technical preview にあり、SQL server を対象とするスキーマとデータの移動を可能にします。
* SSMA は、最新バージョンの SSMA を利用できるようになったらすぐにダウンロードできる自動更新をサポートするようになりました。
* SSMA のインストール可能なバイナリは、Windows インストーラパッケージファイル (.msi) を介して配信されるようになりました。

## <a name="may-2016"></a>2016 年 5 月

SSMA for Oracle の2016年5月のリリースには、次の変更が含まれています。  

* SQL Server 2016 のサポートが追加されました。
* Oracle フラッシュバックのアーカイブテーブルの SQL Server テンポラルテーブルへの変換が追加されました。

  > [!NOTE]
  > SSMA は、Oracle フラッシュバックデータアーカイブテーブルから履歴データをコピーしません。 そのため、移行プロセス中に履歴データを手動でコピーする必要があります。 また、SSMA では、履歴テーブルはシステムテーブルとして扱われるため SQL Server メタデータエクスプローラーに表示されませんが、SQL Server Management Studio で履歴テーブルを表示できます。
  >
  > SQL Server 2016 では、次のようないくつかの Oracle フラッシュバック機能はサポートされていません。
  >
  > * Oracle フラッシュバックトランザクションクエリ
  > * DBMS_FLASHBACK パッケージ
  > * フラッシュバックトランザクション
  > * フラッシュバックデータアーカイブ
  > * フラッシュバックテーブル
  > * フラッシュフラッシュの削除
  > * フラッシュバックデータベース
* Oracle 用の SQL Server ポリシーオブジェクト (Oracle の場合は行レベルセキュリティ) への Oracle VPD ポリシーの変換が追加されました。
* Oracle の初期読み込みの時間が短縮します。
* パーサーと競合回避モジュールが向上しました。
* .Net 2.0 のインストーラーチェックが削除されました。
* .Net 3.5 から .Net 4.0 への拡張パックの依存関係を更新しました。
* SSMA コンソールの [プロジェクトの保存] コマンドと [プロジェクトを開く] コマンドを修正します。
* SSMA コンソールの "securepassword" コマンドを修正します。
* 初期読み込みのオブジェクトのカウントを固定します。
* Oracle の文字データ型の変換を修正します。
* グローバル設定のバグを修正した。
  
## <a name="march-2016"></a>2016 年 3 月

SSMA for Oracle の2016年3月のプレビューリリースでは、次のサポートが追加されました。  
  
* SQL Server 2016 への移行。  
* Oracle 行レベルセキュリティの移行 (いくつかの制限があります)。  
* Oracle のメモリテーブルを SQL Server 列ストアに移行しています。  
  
## <a name="january-2016"></a>2016 年 1 月

SSMA for Oracle の2014年1月のメンテナンスリリースには、次の変更が含まれています。  
  
* クラスター化インデックスのサポートが追加されました。  
* 低速の Oracle スキーマクエリ (RFC 5076207) を修正します。  
* コンソールから Azure への接続を修正します。  
* SSMA (RFC 5706203) に [ログの表示] メニュー項目が追加されました。 
* テレメトリを追加しました。
  
## <a name="july-2014"></a>2014年7月

SSMA for Oracle の2014年7月のリリースには、次の変更が含まれています。  
  
* Azure SQL DB のサポートが追加されました。
* 拡張パックの機能は、Azure SQL DB をサポートするためにスキーマに移行されました。
* Oracle の具体化されたビューのサポートを追加しました。  
* SQL Server 2014 メモリ最適化テーブルのサポートが追加されました。  
* 10,000 を超えるオブジェクトを含むデータベースに対してテストされたパフォーマンスの向上。  
* 多数のオブジェクトを処理するための UI の機能強化が追加されました。  
* "既知の" LOB スキーマの強調表示を追加しました。  
* 変換速度の向上が含まれます。  
* UI でオブジェクト数を表示するためのサポートを追加しました。  
* レポートのサイズが25% を超えています。
* 未解析のコンストラクトのエラーメッセージが改善されました。  
  
## <a name="april-2014"></a>2014 年 4 月

SSMA for Oracle の2014年4月のリリースには、次の変更が含まれています。  
  
* MS SQL Server 2014 のサポートが追加されました。  
* Oracle 12 とクエリの最適化のサポートが追加されました。  
* Azure への変換に関するバグを修正した。  
* IE 10 の非表示レポートページに関するバグを修正した。  
  
## <a name="january-2012"></a>2012 年 1 月

SSMA for Oracle の2012年1月のリリースでは、RowType と RecordType の入力パラメーターの既定値が NULL にサポートされるようになります。  
  
## <a name="july-2011"></a>2011 年 7 月

SSMA for Oracle の2011年7月のリリースには、次の変更が含まれています。  
  
* Oracle シーケンスから "Denali" シーケンスジェネレーター [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]への変換のサポートが追加されました。
* データ移行中のエラー報告の向上。  
* 予約語を使用したステートメントの変換が改善されました。  
* 関数の日付値の暗黙的な変換が改善されました。  
  
## <a name="april-2011"></a>2011年4月

SSMA for Oracle の2011年4月のリリースには、次の変更が含まれています。  
  
* "SSMA for Oracle" 製品の統合により[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、および "Denali" がサポートされています。
* "Denali" に接続して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移行するためのサポートを追加しました。  
* 拡張されたクライアント側のデータ移行エンジンで、データの並列移行がサポートされています。  
* 単純復旧モデルと一括ログ復旧モデルにより、データ移行のパフォーマンスが向上しました。  
* 以前のバージョンの SSMA (v1.0 および v1.1) で作成されたプロジェクトの旧バージョンとの互換性のためのサポートを追加しました。  
* Ssma for Oracle v1.0 製品を旧バージョンの SSMA (v2.0 および v1.1) とサイドバイサイド (SxS) でインストールする機能が追加されました。
* ユーザー定義型 (サブタイプ、VARRAY、入れ子になったテーブル、オブジェクトテーブル、オブジェクトビューを含む) の報告と、特別なエラーメッセージを含む PL/SQL ブロックでの使用に関するサポートが追加されました。  

## <a name="july-2010"></a>2010 年 7 月

SSMA for Oracle の2010年7月のリリースには、次のものが追加されました。

* SQL Server 2008 R2 への移行のサポート。  
* コマンドライン実行用の新しい SSMA コンソールアプリケーション。  
* サーバー側とクライアント側の両方のデータ移行エンジンを使用したデータ移行のサポート。  
* データ移行での "カスタム SELECT" ステートメントのサポート。  
* Oracle 11g R2 からの移行のサポート。  
  
## <a name="june-2008"></a>2008年6月

SSMA for Oracle の2008年6月のリリースには、次の変更が含まれています。  
  
* シノニムの追加情報、解析可能なオブジェクトの未加工のソース、パネルと SQL Server ロゴの削除、レイアウトの永続化など、評価レポートの機能強化が追加されました。  
* オブジェクト変換の機能強化が追加されました。  
  * パッケージ DBMS_LOB、DBMS_SQL 変換が追加されました。  
  * 結合変換の変更。  
  * コレクションとレコードの変換を変更し、フィールドごとに個別の変数を使用してリリースされた単純なケースでレコードを変換できるようになりました。  
  * レコードとコレクションの実装の機能強化。  
  * ウィンドウ集計関数が追加されました。  
  * ROLLUP/CUBE 句が追加されました。  
  * NEXTVAL/CURVAL の改善。  
  * SET 句、Grouping sets、および grouping ID の列グループが追加されました。  
  * MERGE ステートメントが追加されました。  
  * 新しい datetime 型をサポートし、CLR データ型としてレコードとコレクションを変換しました。  
* テスト担当者の新機能が追加されました。 テーブルは、テスト担当者を使用してオブジェクトとしてテストできるようになりました。テストケース内の複数のテスト可能なオブジェクトの呼び出し順序を変更できます。また、ユーザーは、レコードとコレクションを含むプロシージャと関数をパラメーターと戻り値としてテストし、依存関係アナライザーを追加して確認することができます。使用されたテーブルのみです。  
  
## <a name="august-2007"></a>2007年8月

SSMA for Oracle の2007年8月のリリースでは、次のことが追加されました。

* 新しい TESTER コンポーネントを使用すると、テストケースを作成、管理、および実行して、変換された SQL コードを確認できます。  
* SQL コンバーターには、Oracle のサブタイプ、コレクション、およびローカルモジュールの変換がサポートされています。  
* 新しい同期機能を使用すると、特定のオブジェクトを SQL Server データベースと同期させることができます。  
* 新しい変換オプション。  
  
## <a name="april-2007"></a>2007年4月

SSMA for Oracle の2007年4月のリリースは、最初のリリースでした。
