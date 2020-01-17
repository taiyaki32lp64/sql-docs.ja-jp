---
title: '[データベースのプロパティ] ([オプション] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 08/28/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.options.f1
ms.assetid: a3447987-5507-4630-ac35-58821b72354d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9ea3a23299c15a2d473b68f691345d69afaaf1eb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049029"
---
# <a name="database-properties-options-page"></a>[データベースのプロパティ] \([オプション] ページ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このページを使用すると、選択されているデータベースのオプションを表示または変更できます。 このページで利用できるオプションの詳細については、「[ALTER DATABASE の SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)」と「[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)」をご覧ください。  
  
## <a name="page-header"></a>ページ ヘッダー  
 **[照合順序]**  
 データベースの照合順序を一覧から選択して指定します。 詳細については、「 [Set or Change the Database Collation](../../relational-databases/collations/set-or-change-the-database-collation.md)」を参照してください。  
  
 **復旧モデル**  
 データベースを復旧するための、次のいずれかのモデルを指定します。 **[完全]** 、 **[一括ログ]** 、 **[単純]** 。 復旧モデルの詳細については、「[復旧モデル &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)」をご覧ください。  
  
 **互換性レベル**  
 データベースがサポートする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の最新バージョンを指定します。 使用可能な値については、「[ALTER DATABASE (Transact-SQL) Compatibility Level](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」 (ALTER DATABASE (TRANSACT-SQL) 互換性レベル) を参照してください。 SQL Server データベースがアップグレードされると、そのデータベースの互換性レベルが保持される (可能な場合) か、新しいサポートされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の最小レベルに変更されます。 
  
 **[コンテインメントの種類]**  
 これが包含データベースであるかどうかを指定するには、[なし] または [部分] を指定します。 包含データベースの詳細については、「 [Contained Databases](../../relational-databases/databases/contained-databases.md)」をご覧ください。 データベースを包含データベースとして構成するには、 **[包含データベースの有効化]** サーバー プロパティを **TRUE** に設定しておく必要があります。  
  
> [!IMPORTANT]  
>  部分的包含データベースを有効にすると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへのアクセス制御がデータベースの所有者にデリゲートされます。 詳細については、「 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)」を参照してください。  
  
## <a name="automatic"></a>自動  
 **[自動終了]**  
 最後のユーザーが終了した後で、データベースを即座にシャットダウンしてリソースを解放するかどうかを指定します。 指定できる値は、 **[True]** および **[False]** です。 **[True]** を指定すると、最後のユーザーがログオフした後でデータベースは正常にシャットダウンされてリソースが解放されます。  

 **[増分統計の自動作成]**  
 パーティションごとの統計を作成するときに増分オプションを使用するかどうかを指定します。 増分統計の詳細については、「[CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)」をご覧ください。  
  
 **[統計の自動作成]**  
 不足している最適化統計をデータベースで自動的に作成するかどうかを指定します。 指定できる値は、 **[True]** および **[False]** です。 **[True]** を指定すると、クエリの最適化に必要な統計が不足している場合、最適化時に自動的に構築されます。 詳細については、「[CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)」を参照してください。  
  
 **[自動圧縮]**  
 データベース ファイルを定期的な圧縮に使用できるかどうかを指定します。 指定できる値は、 **[True]** および **[False]** です。 詳細については、「 [Shrink a Database](../../relational-databases/databases/shrink-a-database.md)」を参照してください。  
  
 **[統計の自動更新]**  
 データベースで古い最適化統計を自動的に更新するかどうかを指定します。 指定できる値は、 **[True]** および **[False]** です。 **[True]** を指定すると、クエリの最適化に必要な統計が期限切れの場合、最適化時に自動的に構築されます。 詳細については、「[CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)」を参照してください。  
  
 **[統計の非同期的自動更新]**  
 **[True]** が指定された場合、古い統計の自動更新を開始するクエリは、統計が更新されるのを待たずにコンパイルを開始します。 後続のクエリは、更新された統計が使用可能になった時点で、その統計を使用します。  
  
 **[False]** が指定された場合、古い統計の自動更新を開始するクエリは、更新された統計をクエリ最適化プランで使用できるようになるまで待機します。  
  
 このオプションを **[True]** に設定しても、 **[統計の自動更新]** も **[True]** に設定しない限り、効力はありません。  

## <a name="azure"></a>Azure
Azure SQL Database に接続している場合、このセクションにはサービスレベル目標 (SLO) を制御するための設定があります。 新しいデータベースの既定の SLO は、Standard S2 です。

  **[現在のサービス レベル目標]** は、使用する特定の SLO です。 有効な値は、選択したエディションによって制限されます。 目的の SLO 値が一覧にない場合は、値を入力することができます。

  **[エディション]** は、Basic や Premium などの、使用する Azure SQL Database エディションです。 必要なエディションの値が一覧にない場合は、値を入力できます。その値は、Azure REST API で使用される値に一致している必要があります。
  
  **[最大サイズ]** は、データベースの最大サイズです。 目的のサイズの値が一覧にない場合は、値を入力できます。 特定のエディションと SLO の既定サイズは空白のままにします。
  
## <a name="containment"></a>Containment  
 包含データベースでは、通常サーバー レベルで構成する設定の一部をデータベース レベルで構成できます。  
  
 **[既定のフルテキスト言語の LCID]**  
 フルテキスト インデックス列に、既定の言語を指定します。 フルテキスト インデックス データの言語の分析は、データの言語に依存します。 このオプションの既定値は、サーバーの言語です。 表示される設定に対応する言語については、「[sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)」をご覧ください。  
  
 **[既定の言語]**  
 他に指定しない限り、新しいすべての包含データベース ユーザーの既定の言語になります。  
  
 **[入れ子になったトリガーが有効]**  
 トリガーから他のトリガーを起動できるようにします。 トリガーは 32 レベルまで入れ子にできます。 詳細については、「[CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)」の「入れ子にされたトリガー」をご覧ください。  
  
 **[ノイズ ワード変換]**  
 ノイズ ワード (ストップワード) が原因でフルテキスト クエリのブール演算がゼロ行を返す場合に、エラー メッセージを非表示にします。 詳細については、「 [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)」を参照してください。  
  
 **[2 桁表記の年の基準になる年]**  
 年を 2 桁で入力する場合の最大年が示されます。 表示された年からさかのぼって 99 年間を 2 桁で入力できます。 その他の年はすべて 4 桁で入力する必要があります。  
  
 たとえば、既定の設定が 2049 の場合、「3/14/49」と入力した日付は 2049 年 3 月 14 日として解釈され、「3/14/50」と入力した日付は 1950 年 5 月 14 日と解釈されます。 詳細については、「 [two digit year cutoff サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)」を参照してください。  
  
## <a name="cursor"></a>カーソル  
 **[コミットでカーソルを閉じる]**  
 カーソルを開くトランザクションがコミットされた後で、カーソルを閉じるかどうかを指定します。 指定できる値は、 **[True]** および **[False]** です。 **[True]** を指定すると、トランザクションのコミットまたはロールバック時に開いていたカーソルが閉じます。 **[False]** を指定すると、カーソルはトランザクションのコミット時も開いたままです。 **[False]** の場合、トランザクションをロールバックすると、INSENSITIVE または STATIC として定義されているカーソルを除いて、すべてのカーソルが閉じます。 詳細については、「[SET CURSOR_CLOSE_ON_COMMIT &#40;Transact-SQL&#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)」をご覧ください。  
  
 **[既定のカーソル]**  
 既定のカーソルの動作を指定します。 **[True]** を指定すると、カーソルの既定の宣言は LOCAL になります。 **[False]** を指定すると、 [!INCLUDE[tsql](../../includes/tsql-md.md)] カーソルは既定で GLOBAL になります。  
  
## <a name="database-scoped-configurations"></a>データベース スコープ構成  
 SQL Server 2016 と Azure SQL Database には、スコープをデータベース レベルに設定できるさまざまな構成プロパティがあります。 これらのすべての設定について詳しくは、「[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)」をご覧ください。  
  
 **レガシカーディナリティ推定**  
 データベースの互換性レベルに依存しない、プライマリのクエリ オプティマイザーのカーディナリティ推定モデルを指定します。 これは、 [トレース フラグ 9481](https://support.microsoft.com/kb/2801413)を指定した場合と同じです。  
  
 **セカンダリのレガシカーディナリティ推定**  
 データベースの互換性レベルに依存しない、セカンダリ (存在する場合) のクエリ オプティマイザーのカーディナリティ推定モデルを指定します。 これは、 [トレース フラグ 9481](https://support.microsoft.com/kb/2801413)を指定した場合と同じです。  
  
 **最大 DOP**  
 ステートメントで使用される、プライマリの [MAXDOP](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 設定の既定値を指定します。  
  
 **セカンダリの最大 DOP**  
 ステートメントで使用される、セカンダリ (存在する場合) の [MAXDOP](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 設定の既定値を指定します。  
  
 **パラメーター スニッフィング**  
 プライマリのパラメーター スニッフィングを有効にするか無効にするかを指定します。 これは、 [トレース フラグ 4136](https://support.microsoft.com/kb/980653)を指定した場合と同じです。  
  
 **セカンダリのパラメーター スニッフィング**  
 セカンダリ (存在する場合) のパラメーター スニッフィングを有効にするか無効にするかを指定します。 これは、 [トレース フラグ 4136](https://support.microsoft.com/kb/980653)を指定した場合と同じです。  
  
 **クエリ オプティマイザーの修正プログラム**  
 データベースの互換性レベルに関係なく、プライマリ上のクエリ オプティマイザーの修正プログラムを有効にするか無効にするかを指定します。 これは、 [トレース フラグ 4199](https://support.microsoft.com/kb/974006)を指定した場合と同じです。  
  
 **セカンダリのクエリ オプティマイザーの修正プログラム**  
 データベースの互換性レベルに関係なく、セカンダリ (存在する場合) 上のクエリ オプティマイザーの修正プログラムを有効にするか無効にするかを指定します。 これは、 [トレース フラグ 4199](https://support.microsoft.com/kb/974006)を指定した場合と同じです。  
  
## <a name="filestream"></a>FILESTREAM  
 **[FILESTREAM ディレクトリ名]**  
 選択したデータベースと関連付けられている FILESTREAM データのディレクトリ名を指定します。  
  
 **[FILESTREAM 非トランザクション アクセス]**  
 FileTable に格納されている FILESTREAM データへの、ファイル システムを通じた非トランザクション アクセスに対するオプションとして、次のいずれかを指定します。**OFF**、**READ_ONLY**、**FULL**。 FILESTREAM がサーバー上で有効になっていない場合、この値は OFF に設定され、変更できません。 詳細については、「[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)」をご覧ください。  
  
## <a name="miscellaneous"></a>その他  
**[スナップショット分離を許可]**  
この機能を有効にします。  

 **[ANSI NULL 既定値]**  
 **CREATE TABLE** または **ALTER TABLE** ステートメントの実行中に、 **NOT NULL** が明示的に定義されていないすべてのユーザー定義データ型または列に対して、NULL 値を許容します (既定の状態)。 詳細については、「[SET ANSI_NULL_DFLT_ON &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)」と「[SET ANSI_NULL_DFLT_OFF &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-null-dflt-off-transact-sql.md)」をご覧ください。  
  
 **[ANSI NULL 有効]**  
 `=`(等号) 比較演算子と`<>`(不等号) 比較演算子を NULL 値に対して使用した場合の動作を指定します。 指定できる値は、 **[True]** (オン) および **[False]** (オフ) です。 **[True]** を指定すると、NULL 値との比較結果はすべて UNKNOWN になります。 **[False]** を指定すると、UNICODE 以外の値と NULL 値の比較結果は、両方の値が NULL 値の場合に **[True]** になります。 詳細については、「[SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)」をご覧ください。  
  
 **[ANSI PADDING 有効]**  
 ANSI による埋め込みが有効かどうかを指定します。 指定できる値は、 **[True]** (オン) および **[False]** (オフ) です。 詳細については、「[SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)」を参照してください。  
  
 **[ANSI 警告有効]**  
 複数のエラー条件に対する ISO の標準動作を指定します。 **[True]** のときに NULL 値が集計関数 (SUM、AVG、MAX、MIN、STDEV、STDEVP、VAR、VARP、COUNT など) で使用されると、警告メッセージが生成されます。 **[False]** の場合は、警告メッセージは生成されません。 詳細については、「[SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)」をご覧ください。  
  
 **[算術アボート有効]**  
 算術アボートのデータベース オプションが有効かどうかを指定します。 指定できる値は、 **[True]** および **[False]** です。 **[True]** を指定すると、オーバーフローまたは 0 除算エラーが発生したときにクエリまたはバッチが終了します。 エラーがトランザクションの内部で発生した場合には、トランザクションはロールバックされます。 **[False]** を指定すると、警告メッセージが表示されますが、クエリ、バッチ、トランザクションは、エラーが発生しなかったときのように処理を続行します。 詳細については、「[SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)」をご覧ください。  
  
 **[NULL との連結で NULL を使用]**  
 NULL 値が連結された場合の動作を指定します。 プロパティ値が **[True]** の場合、 **string** + NULL は NULL を返します。 **[False]** の場合、結果は **string**です。 詳細については、「[SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)」をご覧ください。  
  
 **[複数データベースの組み合わせ所有権有効]**  
 複数データベースの組み合わせ所有権が有効になっているかどうかを示す、読み取り専用の値です。 **[True]** を指定した場合、複数データベースの組み合わせ所有権のソース データベースまたは対象データベースとしてこのデータベースを使用できます。 このプロパティを設定するには、ALTER DATABASE ステートメントを使用します。  
  
 **[日付の相関関係の最適化有効]**  
 **[True]** を指定すると、データベース内にある FOREIGN KEY 制約でリンクされ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datetime **列を含んでいる 2 つのテーブル間の相関関係に関する統計が** によって保持されます。  
  
 **[False]** を指定すると、相関関係の統計は保持されません。  
 
 **[遅延持続性]**  
 この機能を有効にします。  
 
 **[Is Read Committed Snapshot On]**  
 この機能を有効にします。  
 
 **[数値丸め処理アボート]**  
 データベースが丸めエラーを処理する方法を指定します。 指定できる値は、 **[True]** および **[False]** です。 **[True]** を指定すると、式の精度が低下したときにエラーが生成されます。 **[False]** を指定すると、精度が低下してもエラー メッセージは生成されず、結果はそれを格納する列または変数の精度まで丸められます。 詳細については、「[SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)」をご覧ください。  
  
 **[パラメーター化]**  
 **[単純]** を指定すると、データベースの既定の動作に基づいてクエリがパラメーター化されます。 **[強制]** を指定すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、データベースのすべてのクエリがパラメーター化されます。  
  
 **[引用符で囲まれた識別子有効]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] キーワードを引用符で囲んで識別子 (オブジェクト名または変数名) として使用できるかどうかを指定します。 指定できる値は、 **[True]** および **[False]** です。 詳細については、「[SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)」をご覧ください。  
  
 **[再帰トリガー有効]**  
 トリガーを他のトリガーによって起動できるかどうかを指定します。 指定できる値は、 **[True]** および **[False]** です。 **[True]** を指定すると、トリガーを再帰的に起動できます。 **[False]** を指定すると、直接再帰のみが回避されます。 間接再帰を無効にするには、sp_configure を使用して nested triggers サーバー オプションを 0 に設定します。 詳しくは、「 [入れ子になったトリガーの作成](../../relational-databases/triggers/create-nested-triggers.md)」をご覧ください。  
  
 **信頼可能**  
 読み取り専用オプションです。 **True**が表示されていれば、データベース内に確立された権限借用コンテキストでデータベース外部のリソースにアクセスすることが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により許可されることを示します。 権限借用コンテキストは、EXECUTE AS ユーザー ステートメントまたはデータベース モジュールの EXECUTE AS 句を使用して、データベース内に確立できます。  
  
 データベースの所有者がアクセス権を得るには、サーバー レベルの AUTHENTICATE SERVER 権限も必要です。  
  
 また、このプロパティを True に設定して、安全でない外部のアクセス アセンブリをデータベース内で作成および実行することもできます。 データベースの所有者は、このプロパティを **True**に設定することだけでなく、サーバー レベルの EXTERNAL ACCESS ASSEMBLY 権限または UNSAFE ASSEMBLY 権限も必要です。  
  
 既定では、すべてのユーザー データベースとすべてのシステム データベース ( **MSDB**を除く) で、このプロパティが **False**に設定されます。 **model** データベースおよび **tempdb** データベースのこの値は変更できません。  
  
 データベースをサーバーにアタッチするときは、必ず TRUSTWORTHY を **False** に設定します。  
  
 権限借用コンテキストでデータベース外部のリソースにアクセスするには、 **Trustworthy** オプションではなく、証明書と署名を使用する方法をお勧めします。  
  
 このプロパティを設定するには、ALTER DATABASE ステートメントを使用します。  
  
 **[VarDecimal ストレージ形式有効]**  
 このオプションは、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]以降では読み取り専用です。 **[True]** の場合、このデータベースは vardecimal ストレージ形式に対応しています。 データベースのいずれかのテーブルで vardecimal ストレージ形式を使用している場合、vardecimal ストレージ形式を無効にすることはできません。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンでは、すべてのデータベースが vardecimal ストレージ形式に対応します。 このオプションでは、 [sp_db_vardecimal_storage_format](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)が使用されます。  
  
## <a name="recovery"></a>復旧  
 **[ページ確認]**  
 ディスク I/O エラーによる不完全な I/O トランザクションを検出し、報告する場合に使用されるオプションを指定します。 指定できる値は、 **[None]** 、 **[TornPageDetection]** 、および **[Checksum]** です。 詳細については、「 [suspect_pages テーブルの管理 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)を使用してページを復元する方法について説明します。  
  
 **[ターゲットの復旧時間 (秒)]**  
 クラッシュが発生した場合、指定したデータベースが復旧に要する時間の上限を秒単位で指定します。 詳細については、「[データベース チェックポイント &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)」を参照してください。  

## <a name="service-broker"></a>Service Broker  
**[Broker が有効]**  
Service Broker を有効または無効にします。  

**[Broker の優先度の許可]**  
Service Broker の読み取り専用プロパティです。  

**[Service Broker 識別子]**  
読み取り専用の識別子です。  

## <a name="state"></a>状態  
 **[読み取り専用データベース]**  
 データベースが読み取り専用かどうかを指定します。 指定できる値は、 **[True]** および **[False]** です。 **[True]** を指定すると、ユーザーはデータベースのデータの読み取りのみを実行できます。 データまたはデータベース オブジェクトは変更できませんが、`DROP DATABASE` ステートメントを使用してデータベース自体を削除することはできます。 データベースの使用中には、 **[読み取り専用データベース]** オプションに新しい値を設定することができできません。 master データベースは例外です。このオプションが設定されていても、システム管理者だけは master データベースを使用できます。  
  
 **データベース状態**  
 データベースの現在の状態を表示します。 編集することはできません。 **[データベース状態]** の詳細については、「 [Database States](../../relational-databases/databases/database-states.md)」を参照してください。  

 **[暗号化有効]**  
 **[True]** の場合、このデータベースはデータベース暗号化に対応しています。 暗号化ではデータベース暗号化キーが必要です。 詳細については、「[透過的なデータ暗号化 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)」を参照してください。  
 
 **[アクセスの制限]**  
 データベースにアクセスできるユーザーを指定します。 有効な値は次のとおりです。  
  
-   **複数**  
  
     稼働データベースの通常の状態では、一度に複数のユーザーがデータベースにアクセスできます。  
  
-   **単一**  
  
     メンテナンス アクションで使用されます。データベースには一度に 1 人のユーザーのみがアクセスできます。  
  
-   **制限あり**  
  
     db_owner、dbcreator、または sysadmin ロールのメンバーのみがデータベースを使用できます。  
  


## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
