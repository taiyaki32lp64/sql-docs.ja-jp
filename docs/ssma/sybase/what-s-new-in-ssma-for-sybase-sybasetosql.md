---
title: SSMA for SAP ASE の新機能 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 12/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: 094db4e2d374f79e8102d111d0a9f9bfda22e6b7
ms.sourcegitcommit: 26868c8ac3217176b370d972a26d307598a10328
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74834262"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>SSMA for SAP ASE の新機能 (SybaseToSQL)

この記事では、各リリースでの SAP ASE (旧称 SSMA for Sybase) の変更 (SSMA) の SQL Server Migration Assistant を示します。

## <a name="ssma-v85"></a>SSMA v1.0

SSMA for SAP ASE の v1.0 リリースは、SQL server での JSON 機能の Azure Active Directory 認証と基本的なサポートがサポートされるようになり、使いやすさとパフォーマンスを向上させるように設計された修正プログラムが対象となりました。

さらに、SSMA for SAP ASE では、システムテーブルとビューを非表示にする (変換から除外する) ことができます。

> [!IMPORTANT]
> SSMA v1.0 では、.Net 4.7.2 はインストールの前提条件です。 このバージョンをインストールする必要がある場合は、[ここ](https://dotnet.microsoft.com/download/dotnet-framework/net472)からランタイムファイルをダウンロードできます。

## <a name="ssma-v84"></a>SSMA v 8.4

SSMA for SAP ASE の v1.0 リリースは、ユーザー補助の問題に対処し、最大インデックス列 (16 ではなく 32) に関連するバグを修正して、SQL Server 2016 以降のバージョンに対応するように設計された、対象の修正によって強化されています。

> [!IMPORTANT]
> SSMA バージョン 7.4 ~ 8.4 の場合、.Net 4.5.2 はインストールの前提条件です。

## <a name="ssma-v83"></a>SSMA v 8.3

SSMA for SAP ASE の v2.0 リリースは、品質と変換のメトリックを向上させるように設計された対象の修正によって強化されています。 また、SSMA for SAP ASE の今回のリリースでは、次のような修正が行われています。

* アクセシビリティに関する問題の解決
* SQL Server に ' hierarchyid ' 型の基本的なサポートを追加します

## <a name="ssma-v82"></a>SSMA v 8.2

SSMA for SAP ASE の v2.0 リリースは、品質と変換のメトリックを向上するように設計された修正プログラムのセットと、次のような修正によって強化されています。

* データ移行後の非クラスター化インデックスが無効になっている問題。
* サイレントインストール中の .NET Framework の検出。
* 新しいバージョンがダウンロードされると発生する断続的なクラッシュ。

> [!NOTE]
> 自動更新に関する既知の問題により、SSMA v2.0 から v2.0 への更新が失敗する場合があります。 このエラーが発生した場合は、新しいバージョンをダウンロードし、手動でインストールしてください。

## <a name="ssma-v81"></a>SSMA v 8.1

SSMA for SAP ASE の v2.0 リリースは、品質と変換のメトリックを向上させるように設計された対象の修正によって強化されています。

> [!NOTE]
> 自動更新に関する既知の問題により、SSMA v2.0 から v2.0 への更新が失敗する場合があります。 このエラーが発生した場合は、新しいバージョンをダウンロードし、手動でインストールしてください。

## <a name="ssma-v80"></a>SSMA 8.0

SSMA for SAP ASE の v2.0 リリースは、品質と変換メトリックの向上を目的とした修正を対象として強化されています。 また、このリリースでは、次の新機能が提供されています。

* ターゲットとしての**Azure SQL Database Managed Instance**のサポート。 Azure SQL Database Managed Instance をターゲットとする新しいプロジェクトを作成できるようになりました。

  ![SQL DB MI プロジェクト](../media/ssma-newproject-sqldbmi.png)

* 変換後の**修正アドバイザー**。 詳細について[は、こちら](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)を参照してください。

* データベース/スキーマの事前選択。

  ソースに接続するときに、ユーザーは目的のデータベースまたはスキーマを選択できるようになりました。 移行を計画しているスキーマのみを選択すると、初期接続時に時間が節約され、全体的な SSMA パフォーマンスが向上します。

  ![SSMA フィルターオブジェクト](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v 7.10

SSMA for SAP ASE のバージョン7.10 リリースは、グローバル要件の変化に対応するための追加のセキュリティとプライバシーの保護を提供するように設計された修正プログラムによって強化されています。

## <a name="ssma-v79"></a>SSMA v 7.9

SSMA for SAP ASE の v1.0 リリースには、次の変更が含まれています。

* 品質と変換のメトリックを向上させる対象の修正。
* SSMA コマンドラインでデータ型マッピングとプロジェクト設定を変更するためのサポート。
* SQL Server Integration Services (SSIS) を使用したデータ移行のサポート。 スキーマを変換した後、右クリックコンテキストメニューオプションを使用して SSIS パッケージを作成できます。
* SSMA の [Azure SQL Database 接続] ダイアログも、完全修飾サーバー名を指定するように変更されています。 以前のバージョンの SSMA では、プロジェクト設定内で Azure SQL Database プレフィックスを明示的に記述する必要がありました。

## <a name="ssma-v78"></a>SSMA v 7.8

SSMA for SAP ASE の v1.0 リリースには、次の変更が含まれています。

* [プロジェクトの設定] で強調表示されている型マッピングを変更します。
* ユーザーがテレメトリを無効にする機能。

## <a name="ssma-v77"></a>SSMA v 7.7

SSMA for SAP ASE のバージョン7.7 リリースには、次の変更が含まれています。

* SSMA for SAP ASE は、品質と変換のメトリックを向上させる対象の修正によって強化されています。
* 一般的な要求に基づいて、SSMA for SAP ASE の32ビットバージョンは戻ります。 以前の実装と比較して (v2.0 より前)、インストーラーパッケージは2つありますが、サイドバイサイドでインストールすることはできません。 そのため、使用している接続コンポーネントに基づいて、最適なバージョンを選択する必要があります。 可能であれば、常に64ビットバージョンを使用することをお勧めします。

## <a name="ssma-v76"></a>SSMA v1.0

SSMA for SAP ASE の v1.1 リリースには、次の変更が含まれています。

* 品質と変換のメトリックを向上させ、SQL Server 2017 (パブリックプレビュー) をサポートするように対象とする修正。 Windows および Linux での SQL Server 2017 のサポートはパブリックプレビュー段階であり、運用環境への移行には使用しないでください。
* Sybase 関数の変換のサポート。

## <a name="ssma-v75"></a>SSMA v 7.5

SSMA for SAP ASE のバージョン7.5 リリース (以前の SSMA for Sybase) には、次の変更が含まれています。

* 障碍のある方にとってアクセシビリティを向上させるためにいくつかの機能強化が行われました。
* CREATE または REPLACE 構文のサポート。

## <a name="ssma-v74"></a>SSMA v1.0

SSMA for Sybase の v2.0 リリースには、次の変更が含まれています。

* [**クエリタイムアウト**] オプションは、ソースおよびターゲットでのスキーマオブジェクトの検出中に使用できるようになりました。

  ![クエリタイムアウトオプション](../media/query-timeout_red.png)
* お客様からのフィードバックに基づいて、品質と換算のメトリックが修正されました。

  > [!IMPORTANT]
  > .Net 4.5.2 は、SSMA v2.0 をインストールするための前提条件です。 さらに、v2.0 以降では、SSMA の32ビットバージョンは廃止されています。  

## <a name="ssma-v73"></a>SSMA version 7.3

SSMA for Sybase の version 7.3 リリースには、次の変更が含まれています。

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

SSMA for Sybase のバージョン7.2 には、次の変更が含まれています。

* お客様からのフィードバックに基づいて、対象の修正を含む品質と変換のメトリックが向上しました。
* テレメトリの機能強化により、顧客の問題をトラブルシューティングし、SSMA のコンバージョン率を向上させるためのデータポイントが向上しました。

## <a name="ssma-v71"></a>SSMA 7.1

SSMA for Sybase の v2.0 リリースには、次の変更が含まれています。

* Windows と Linux CTP1 の SQL Server 2017 は、現在、移行のためにサポートされているターゲットプラットフォームです。 この機能は technical preview であり、SQL server を対象とするスキーマとデータの移動をサポートしています。
* 最新バージョンの SSMA が利用可能になるとすぐにダウンロードするための自動更新のサポート。
* SSMA のインストール可能なバイナリは、Windows インストーラパッケージファイル (.msi) を介して配信されるようになりました。

## <a name="may-2016"></a>2016 年 5 月

SSMA for Sybase の2016年5月のリリースには、次の変更が含まれています。  

* SQL Server 2016 のサポートが追加されました。
* .Net 2.0 のインストーラーチェックが削除されました。
* .Net 3.5 から .Net 4.0 への拡張パックの依存関係を更新しました。
* SSMA コンソールの [プロジェクトの保存] コマンドと [プロジェクトを開く] コマンドを修正します。
* SSMA コンソールの "securepassword" コマンドを修正します。
* 初期読み込みのオブジェクトのカウントを固定します。
* グローバル設定のバグを修正した。

## <a name="march-2016"></a>2016 年 3 月

SSMA for Sybase の2016年3月のプレビューリリースでは、SQL Server 2016 への移行のサポートが追加されます。  
  
## <a name="january-2016"></a>2016 年 1 月

SSMA for Sybase の2016年1月のメンテナンスリリースには、次の変更が含まれています。  
  
* SSMA (RFC 5706203) に [ログの表示] メニュー項目が追加されました。  
* テレメトリを追加しました。

## <a name="july-2014"></a>2014年7月

SSMA for Sybase の2014年7月のリリースには、次の変更が含まれています。  
  
* Azure SQL DB のコード変換が改善されました。  
* 拡張パックの機能をスキーマに移動し、Azure SQL DB をサポートするようになりました。  
* 10,000 を超えるオブジェクトを含むデータベースに対してテストされたパフォーマンスの改善。  
* 多数のオブジェクトを処理するための UI の機能強化が追加されました。  
* "既知の" LOB スキーマを強調表示する機能が追加されました (そのため、変換では無視できます)。  
* 変換速度が向上しました。  
* UI でオブジェクト数を表示する機能が追加されました。
* レポートのサイズが25% を超えています。  
* 未解析のコンストラクトのエラーメッセージが改善されました。  
  
## <a name="april-2014"></a>2014 年 4 月

SSMA for Sybase の2014年4月のリリースには、次の変更が含まれています。  
  
* MS SQL Server 2014 のサポートが追加されました。  
* Azure への変換に関するバグを修正した。  
* IE 10 の非表示レポートページに関するバグを修正した。  
  
## <a name="january-2012"></a>2012 年 1 月

SSMA for Sybase の2012年1月リリースには、次の変更が含まれています。  
  
* ロールバックトリガー変換のサポートが追加されました。
* 同じ SET ステートメントで @@ROWCOUNTと @@ERRORを変換するための修正を提供しました。  
  
## <a name="july-2011"></a>2011 年 7 月

SSMA for Sybase の2011年7月のリリースでは、データ移行中のエラー報告が改善されています。  
  
## <a name="april-2011"></a>2011年4月

SSMA for Sybase の2011年4月のリリースには、次の変更が含まれています。  
  
* "SSMA for Sybase" 製品が統合され[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]てい[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]これは2005、2008、"Denali"、および Azure SQL をサポートしています。  
* "Denali" に接続して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移行するためのサポートを追加しました。  
* Sybase データベースを変換して Azure SQL に移行するための新機能が追加されました。  
* 拡張されたクライアント側のデータ移行エンジンで、データの並列移行がサポートされています。  
* 単純復旧モデルと一括ログ復旧モデルにより、データ移行のパフォーマンスが向上しました。
* 大文字と小文字を区別する Sybase データベースを適切に変換し、大文字と小文字を区別する SQL Server に移行する機能が追加されました。  
* Ansi join ステートメントの SQL Server への変換のサポートが追加され、ステートメントを削除および更新できるようになりました。  
* Sybase ASE ODBC プロバイダと Sybase ASE ADO.Net プロバイダを使用して Sybase ASE サーバーに接続するための追加の接続オプションが用意されています。
* **Sysdb**という名前の別のデータベースへの依存関係を削除しました。これには、Sybase エミュレーション関数 (拡張パックの一部としてインストールされます) が含まれています。
* SSMA for Sybase Extension Pack をクラスターに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インストールする機能が追加されました。
* 以前のバージョンの SSMA (v1.0 および v1.1) で作成されたプロジェクトの下位互換性が追加されました。  
* Ssma for Sybase version 5.0 製品を旧バージョンの SSMA (v2.0 および v1.1) とサイドバイサイド (SxS) でインストールする機能が追加されました。  
  
## <a name="july-2010"></a>2010 年 7 月

SSMA for Sybase の2010年7月のリリースは、次のように追加されました。

* SQL Server 2008 R2 への移行のサポート。  
* コマンドライン実行用の新しい SSMA コンソールアプリケーション。  
* サーバー側とクライアント側の両方のデータ移行エンジンを使用したデータ移行のサポート。  
* データ移行での "カスタム SELECT" ステートメントのサポート。  
* Sybase ASE 15.0.3 と15.5 からの移行のサポート。  
  
## <a name="june-2008"></a>2008年6月

SSMA for Sybase の2008年6月のリリースには、次の変更が含まれています。  
  
* SSMA Tester が追加されました。 ssma テスターは、SSMA によって行われたデータベースオブジェクトの変換とデータ移行を自動的にテストします。 SSMA の移行手順がすべて完了したら、SSMA Tester を使用して、変換されたオブジェクトが同じように動作することと、すべてのデータが適切に転送されたことを確認します。
* SQL 変換前の変換が追加されました。 ユーザーは、変換に使用する各ソースプロシージャの一時テーブル (およびその他のオブジェクト) の宣言を指定できるようになりました。
* オブジェクト変換の機能強化が追加されました。  
  * 結合変換の変更。  
  * /Group by 句を指定せずに集計と非集計を行います。  
  * SELECT INTO ステートメントを含む IDENTITY 関数。  
  * データのみがロックされているクラスター化された制約とインデックス。  
  * SELECT INTO によって作成された一時テーブル。  
  * 一時テーブルの制約/インデックス。  
  * 新しい[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 datetime 型がサポートされています。  
  * Sybase 15.0 の接続とデータ型のサポート。  
  
## <a name="may-2007"></a>5月2007

SSMA for Sybase の2007年5月のリリースが追加されました。  
  
* プロジェクトを保存するときに、データベースの内容をすばやく読み込むことができます。  
* SQL Server 書式設定された SQL モードでのユーザー入力のコメントのサポート。  
* オブジェクト変換の機能強化。  

## <a name="november-2006"></a>2006年11月

SSMA for Sybase の2006年11月のリリースには、次の変更が含まれています。  
  
* 新しいグローバル設定を追加しました:  
  * エディターウィンドウで行番号を表示するように選択できます。  
  * SSMA を構成して、重複するオブジェクトの置換を求めるメッセージを表示したり、スキーマの変換中に重複するオブジェクトを常に置き換えることができます。  
* 次の状況を SSMA が処理する方法を構成できる新しい変換オプションが追加されました。  
  * バイナリ文字列を含む CAST または CONVERT ステートメント。  
  * 等値式で null 値をチェックします。  
  * プロキシテーブル。  
  * RAISERROR のユーザーメッセージエラー番号。  
  * 未解決の識別子を含む UPDATE ステートメント。  
* 新しい移行オプションが追加されました。このオプションを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ssma が日付範囲外の日付をどのように処理するかを指定できます。  
* [ **Sql** ] タブに、書式設定された**sql**設定が追加されました。これにより、コードの読みやすさが向上します。  
* バグの修正 (次を含む):
  * SSMA により、{SHARED | のロックテーブル*テーブル*が変換されるようになりましたEXCLUSIVE} モードのステートメント。 TABLOCK または TABLOCKX ヒントを、テーブルに対する後続の SELECT クエリに追加します。  
  * 文字式でバイナリ型を使用するときに、必要なキャストが追加されるようになりました。  
  * メモリとパフォーマンスの向上。  
  
## <a name="july-2006"></a>2006年7月

SSMA for Sybase は、2006 年 7 月のリリースが初回のリリースでした。  
  
## <a name="see-also"></a>参照

[SSMA for Sybase のはじめに &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
