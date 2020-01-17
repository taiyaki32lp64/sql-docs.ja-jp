---
title: '[データベースのプロパティ] ([オプション] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.options.f1
ms.assetid: a3447987-5507-4630-ac35-58821b72354d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a4420aaf7b11eccecf0b04bb67a55386215f1fc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62917088"
---
# <a name="database-properties-options-page"></a>[データベースのプロパティ] \([オプション] ページ)
  このページを使用すると、選択されているデータベースのオプションを表示または変更できます。 このページで使用できるオプションについては、次を参照してください。 [ALTER DATABASE SET Options &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)します。  
  
## <a name="page-header"></a>ページ ヘッダー  
 **[照合順序]**  
 データベースの照合順序を一覧から選択して指定します。 詳細については、「 [Set or Change the Database Collation](../collations/set-or-change-the-database-collation.md)」を参照してください。  
  
 **復旧モデル**  
 データベースを復旧するための、次のいずれかのモデルを指定します。 **[完全]** 、 **[一括ログ]** 、 **[単純]** 。 復旧モデルの詳細については、「[復旧モデル &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)」をご覧ください。  
  
 **互換性レベル**  
 データベースがサポートする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の最新バージョンを指定します。 指定できる値は、  **[SQL Server 2014 (120)]** 、  **[SQL Server 2012 (110)]** 、 **[SQL Server 2008 (100)]** です。 SQL Server 2005 データベースを SQL Server 2014 にアップグレードすると、そのデータベースの互換性レベルは 90 から 100 に変更されます。  互換性レベル 90 は SQL Server 2014 ではサポートされていません。 詳細については、「[ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)」を参照してください。  
  
 **[コンテインメントの種類]**  
 これが包含データベースであるかどうかを指定するには、[なし] または [部分] を指定します。 包含データベースの詳細については、「 [Contained Databases](contained-databases.md)」をご覧ください。 データベースを包含データベースとして構成するには、 **[包含データベースの有効化]** サーバー プロパティを **TRUE** に設定しておく必要があります。  
  
> [!IMPORTANT]  
>  部分的包含データベースを有効にすると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへのアクセス制御がデータベースの所有者にデリゲートされます。 詳細については、「 [Security Best Practices with Contained Databases](security-best-practices-with-contained-databases.md)」を参照してください。  
  
## <a name="automatic"></a>自動  
 **[自動終了]**  
 最後のユーザーが終了した後で、データベースを即座にシャットダウンしてリソースを解放するかどうかを指定します。 設定可能な値は `True` および `False` です。 `True` を指定すると、データベースは正常にシャットダウンされ、最後のユーザーがログオフするとデータベースのリソースは解放されます。  
  
 増分統計の自動作成  
 パーティションごとの統計を作成するときに増分オプションを使用するかどうかを指定します。 増分統計の詳細については、「[CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)」をご覧ください。  
  
 **[統計の自動作成]**  
 不足している最適化統計をデータベースで自動的に作成するかどうかを指定します。 設定可能な値は `True` および `False` です。 `True` を指定すると、クエリの最適化に必要な統計が不足している場合、最適化時に自動的に構築します。 詳細については、「[CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)」を参照してください。  
  
 **[自動圧縮]**  
 データベース ファイルを定期的な圧縮に使用できるかどうかを指定します。 設定可能な値は `True` および `False` です。 詳細については、「 [Shrink a Database](shrink-a-database.md)」を参照してください。  
  
 **[統計の自動更新]**  
 データベースで古い最適化統計を自動的に更新するかどうかを指定します。 設定可能な値は `True` および `False` です。 `True` を指定すると、クエリの最適化に必要な統計が期限切れの場合、最適化時に自動的に構築されます。 詳細については、「[CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)」を参照してください。  
  
 **[統計の非同期的自動更新]**  
 ときに`True`、古い統計の自動更新を開始するクエリをコンパイルする前に更新する統計を待ちません。 後続のクエリは、更新された統計が使用可能になった時点で、その統計を使用します。  
  
 ときに`False`、古い統計の自動更新を開始するクエリが、更新された統計はクエリ最適化プランで使用できるまでに待機します。  
  
 このオプションを設定`True`及ぼしませんしない限り、**統計の自動更新**にも設定されている`True`します。  
  
## <a name="containment"></a>Containment  
 包含データベースでは、通常サーバー レベルで構成する設定の一部をデータベース レベルで構成できます。  
  
 **[既定のフルテキスト言語の LCID]**  
 フルテキスト インデックス列に、既定の言語を指定します。 フルテキスト インデックス データの言語の分析は、データの言語に依存します。 このオプションの既定値は、サーバーの言語です。 表示される設定に対応する言語については、「[sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)」をご覧ください。  
  
 **[既定の言語]**  
 他に指定しない限り、新しいすべての包含データベース ユーザーの既定の言語になります。  
  
 **[入れ子になったトリガーが有効]**  
 トリガーから他のトリガーを起動できるようにします。 トリガーは 32 レベルまで入れ子にできます。 詳細については、「[CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)」の「入れ子にされたトリガー」をご覧ください。  
  
 **[ノイズ ワード変換]**  
 ノイズ ワード (ストップワード) が原因でフルテキスト クエリのブール演算がゼロ行を返す場合に、エラー メッセージを非表示にします。 詳細については、「 [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)」を参照してください。  
  
 **[2 桁表記の年の基準になる年]**  
 年を 2 桁で入力する場合の最大年が示されます。 表示された年からさかのぼって 99 年間を 2 桁で入力できます。 その他の年はすべて 4 桁で入力する必要があります。  
  
 たとえば、既定の設定が 2049 の場合、「3/14/49」と入力した日付は 2049 年 3 月 14 日として解釈され、「3/14/50」と入力した日付は 1950 年 5 月 14 日と解釈されます。 詳細については、「 [two digit year cutoff サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)」を参照してください。  
  
## <a name="cursor"></a>カーソル  
 **[コミットでカーソルを閉じる]**  
 カーソルを開くトランザクションがコミットされた後で、カーソルを閉じるかどうかを指定します。 設定可能な値は `True` および `False` です。 `True` を指定すると、トランザクションのコミットまたはロールバック時にオープンされているカーソルはクローズされます。 `False` を指定すると、このようなカーソルはトランザクションのコミット時もオープンされたままです。 `False` の場合、トランザクションをロールバックすると、INSENSITIVE または STATIC として定義されているカーソルを除いてすべてのカーソルはクローズされます。 詳細については、「[SET CURSOR_CLOSE_ON_COMMIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-cursor-close-on-commit-transact-sql)」をご覧ください。  
  
 **[既定のカーソル]**  
 既定のカーソルの動作を指定します。 `True` を指定すると、カーソルの既定の宣言は LOCAL になります。 ときに`False`、[!INCLUDE[tsql](../../includes/tsql-md.md)]カーソルは既定でグローバルにします。  
  
## <a name="filestream"></a>FILESTREAM  
 **[FILESTREAM ディレクトリ名]**  
 選択したデータベースと関連付けられている FILESTREAM データのディレクトリ名を指定します。  
  
 **[FILESTREAM 非トランザクション アクセス]**  
 FileTable に格納されている FILESTREAM データへの、ファイル システムを通じた非トランザクション アクセスに対するオプションとして、次のいずれかを指定します。**OFF**、**READ_ONLY**、**FULL**。 FILESTREAM がサーバー上で有効になっていない場合、この値は OFF に設定され、変更できません。 詳細については、「[FileTables &#40;SQL Server&#41;](../blob/filetables-sql-server.md)」をご覧ください。  
  
## <a name="miscellaneous"></a>その他  
 **[ANSI NULL 既定値]**  
 `NOT NULL` または `CREATE TABLE` ステートメントの実行中に、`ALTER TABLE` が明示的に定義されていないすべてのユーザー定義データ型または列に対して、NULL 値を許容します (既定の状態)。 詳細については、「[SET ANSI_NULL_DFLT_ON &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-null-dflt-on-transact-sql)」と「[SET ANSI_NULL_DFLT_OFF &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-null-dflt-off-transact-sql)」をご覧ください。  
  
 **[ANSI NULL 有効]**  
 `=`(等号) 比較演算子と`<>`(不等号) 比較演算子を NULL 値に対して使用した場合の動作を指定します。 指定できる値は`True`(オン) と`False`(オフ)。 `True` を指定すると、NULL 値との比較結果はすべて UNKNOWN になります。 ときに`False`、UNICODE 以外の値に null 値の比較に評価`True`両方の値が NULL の場合。 詳細については、「[SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql)」をご覧ください。  
  
 **[ANSI PADDING 有効]**  
 ANSI による埋め込みが有効かどうかを指定します。 指定できる値は`True`(オン) と`False`(オフ)。 詳細については、「[SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql)」を参照してください。  
  
 **[ANSI 警告有効]**  
 複数のエラー条件に対する ISO の標準動作を指定します。 ときに`True`、(SUM、AVG、MAX、MIN、STDEV、STDEVP、VAR、VARP、または数) などの集計関数で null 値が表示されない場合に警告メッセージが生成されます。 ときに`False`警告は発行されません。 詳細については、「[SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)」をご覧ください。  
  
 **[算術アボート有効]**  
 算術アボートのデータベース オプションが有効かどうかを指定します。 設定可能な値は `True` および `False` です。 `True` を指定すると、オーバーフローまたは 0 除算エラーが発生したときにクエリまたはバッチが終了します。 エラーがトランザクションの内部で発生した場合には、トランザクションはロールバックされます。 `False` を指定すると、警告メッセージが表示されますが、クエリ、バッチ、またはトランザクションは、エラーが発生しなかったかのように処理を続行します。 詳細については、「[SET ARITHABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql)」をご覧ください。  
  
 **[NULL との連結で NULL を使用]**  
 NULL 値が連結された場合の動作を指定します。 プロパティ値が`True`、 `string` + NULL は NULL を返します。 ときに`False`、結果は`string`します。 詳細については、「[SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql)」をご覧ください。  
  
 **[複数データベースの組み合わせ所有権有効]**  
 複数データベースの組み合わせ所有権が有効になっているかどうかを示す、読み取り専用の値です。 ときに`True`、ソースまたはターゲット データベースにまたがる組み合わせ所有権のデータベースを指定できます。 このプロパティを設定するには、ALTER DATABASE ステートメントを使用します。  
  
 **[日付の相関関係の最適化有効]**  
 ときに`True`、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] FOREIGN KEY 制約でリンクされていて、データベースの 2 つのテーブル間の相関統計を保持`datetime`列。  
  
 ときに`False`、相関関係の統計は保持されません。  
  
 **[数値丸め処理アボート]**  
 データベースが丸めエラーを処理する方法を指定します。 設定可能な値は `True` および `False` です。 `True` を指定すると、式の精度が低下したときにエラーが生成されます。 ときに`False`、有効桁数の損失は、エラー メッセージを生成しないと、結果は、結果を格納する変数または列の有効桁数に丸められます。 詳細については、「[SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-numeric-roundabort-transact-sql)」をご覧ください。  
  
 **[パラメーター化]**  
 **[単純]** を指定すると、データベースの既定の動作に基づいてクエリがパラメーター化されます。 **[強制]** を指定すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、データベースのすべてのクエリがパラメーター化されます。  
  
 **[引用符で囲まれた識別子有効]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] キーワードを引用符で囲んで識別子 (オブジェクト名または変数名) として使用できるかどうかを指定します。 設定可能な値は `True` および `False` です。 詳細については、「[SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql)」をご覧ください。  
  
 **[再帰トリガー有効]**  
 トリガーを他のトリガーによって起動できるかどうかを指定します。 設定可能な値は `True` および `False` です。 設定すると`True`トリガーの再帰的に起動できます。 設定すると`False`のみ、直接再帰が回避されます。 間接再帰を無効にするには、sp_configure を使用して nested triggers サーバー オプションを 0 に設定します。 詳しくは、「 [入れ子になったトリガーの作成](../triggers/create-nested-triggers.md)」をご覧ください。  
  
 `Trustworthy`  
 表示するときに`True`、この読み取り専用オプションが示す[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース内で確立されている、権限借用コンテキストでデータベース外部のリソースにアクセスできます。 権限借用コンテキストは、EXECUTE AS ユーザー ステートメントまたはデータベース モジュールの EXECUTE AS 句を使用して、データベース内に確立できます。  
  
 データベースの所有者がアクセス権を得るには、サーバー レベルの AUTHENTICATE SERVER 権限も必要です。  
  
 また、このプロパティを True に設定して、安全でない外部のアクセス アセンブリをデータベース内で作成および実行することもできます。 データベースの所有者は、このプロパティを `True` に設定することだけでなく、サーバー レベルの EXTERNAL ACCESS ASSEMBLY 権限または UNSAFE ASSEMBLY 権限も必要です。  
  
 既定で、すべてのユーザー データベースとすべてのシステム データベース (例外として**MSDB**) このプロパティに設定されて`False`します。 **model** データベースおよび **tempdb** データベースのこの値は変更できません。  
  
 データベースをサーバーにアタッチするときは、必ず TRUSTWORTHY を `False` に設定します。  
  
 権限借用コンテキストでデータベース外部のリソースにアクセスするには、`Trustworthy` オプションではなく、証明書と署名を使用する方法をお勧めします。  
  
 このプロパティを設定するには、ALTER DATABASE ステートメントを使用します。  
  
 **[VarDecimal ストレージ形式有効]**  
 このオプションは読み取り専用で始まる[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]以降のバージョンですべてのデータベースは vardecimal ストレージ形式を有効になっているとします。 このオプションでは、 [sp_db_vardecimal_storage_format](/sql/relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql)が使用されます。  
  
## <a name="recovery"></a>復旧  
 **[ページ確認]**  
 ディスク I/O エラーによる不完全な I/O トランザクションを検出し、報告する場合に使用されるオプションを指定します。 指定できる値は、 **[None]** 、 **[TornPageDetection]** 、および **[Checksum]** です。 詳細については、「 [suspect_pages テーブルの管理 &#40;SQL Server&#41;](../backup-restore/manage-the-suspect-pages-table-sql-server.md)を使用してページを復元する方法について説明します。  
  
 **[ターゲットの復旧時間 (秒)]**  
 クラッシュが発生した場合、指定したデータベースが復旧に要する時間の上限を秒単位で指定します。 詳細については、「[データベース チェックポイント &#40;SQL Server&#41;](../logs/database-checkpoints-sql-server.md)」をご覧ください。  
  
## <a name="state"></a>状態  
 **[読み取り専用データベース]**  
 データベースが読み取り専用かどうかを指定します。 設定可能な値は `True` および `False` です。 `True` を指定すると、ユーザーはデータベースでデータの読み取りのみ行えます。 データまたはデータベース オブジェクトは変更できませんが、DROP DATABASE ステートメントを使用してデータベース自体を削除することはできます。 データベースの使用中には、 **[読み取り専用データベース]** オプションに新しい値を設定することができできません。 master データベースは例外です。このオプションが設定されていても、システム管理者だけは master データベースを使用できます。  
  
 **データベース状態**  
 データベースの現在の状態を表示します。 編集することはできません。 **[データベース状態]** の詳細については、「 [Database States](database-states.md)」を参照してください。  
  
 **[アクセスの制限]**  
 データベースにアクセスできるユーザーを指定します。 有効な値は次のとおりです。  
  
-   **複数**  
  
     稼働データベースの通常の状態では、一度に複数のユーザーがデータベースにアクセスできます。  
  
-   **単一**  
  
     メンテナンス アクションで使用されます。データベースには一度に 1 人のユーザーのみがアクセスできます。  
  
-   **制限あり**  
  
     db_owner、dbcreator、または sysadmin ロールのメンバーのみがデータベースを使用できます。  
  
 **[暗号化有効]**  
 ときに`True`、このデータベースはデータベースの暗号化に対応します。 暗号化ではデータベース暗号化キーが必要です。 詳細については、「[透過的なデータ暗号化 &#40;TDE&#41;](../security/encryption/transparent-data-encryption.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  
