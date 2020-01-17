---
title: SET ステートメント (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET
- SET_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ISO SET statements
- queries [SQL Server], executing
- dates [SQL Server], SET statements
- time [SQL Server], SET statements
- SET statement, about SET statement
- SET statement
- statistical information [SQL Server], SET statements
- locking [SQL Server], SET statements
ms.assetid: f7e107f8-0fcf-408b-b30f-da2323eeb714
author: CarlRabeler
ms.author: carlrab
monikerRange: = azure-sqldw-latest ||= azuresqldb-current || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 20cf6e1c3c98a99898a7b302980d76cef327be5d
ms.sourcegitcommit: 2da98f924ef34516f6ebf382aeb93dab9fee26c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2019
ms.locfileid: "70228492"
---
# <a name="set-statements-transact-sql"></a>SET ステートメント (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

[!INCLUDE[tsql](../../includes/tsql-md.md)] プログラミング言語には、現在のセッションにおける特定の情報の処理方法を変更する SET ステートメントがいくつか用意されています。 これらの SET ステートメントは、次の表に示すカテゴリに分類されます。  
  
SET ステートメントを使用したローカル変数の設定について詳しくは、「[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)」をご覧ください。  
  
|カテゴリ|ステートメント|  
|--------------|----------------|  
|日付時刻ステートメント|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)<br /><br /> [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)|  
|ロック ステートメント|[SET DEADLOCK_PRIORITY](../../t-sql/statements/set-deadlock-priority-transact-sql.md)<br /><br /> [SET LOCK_TIMEOUT](../../t-sql/statements/set-lock-timeout-transact-sql.md)|  
|その他のステートメント|[SET CONCAT_NULL_YIELDS_NULL](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)<br /><br /> [SET CURSOR_CLOSE_ON_COMMIT](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)<br /><br /> [SET FIPS_FLAGGER](../../t-sql/statements/set-fips-flagger-transact-sql.md)<br /><br /> [SET IDENTITY_INSERT](../../t-sql/statements/set-identity-insert-transact-sql.md)<br /><br /> [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)<br /><br /> [SET OFFSETS](../../t-sql/statements/set-offsets-transact-sql.md)<br /><br /> [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md)|  
|クエリ実行ステートメント|[SET ARITHABORT](../../t-sql/statements/set-arithabort-transact-sql.md)<br /><br /> [SET ARITHIGNORE](../../t-sql/statements/set-arithignore-transact-sql.md)<br /><br /> [SET FMTONLY](../../t-sql/statements/set-fmtonly-transact-sql.md)<br /> 注: [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br /><br /> [SET NOCOUNT](../../t-sql/statements/set-nocount-transact-sql.md)<br /><br /> [SET NOEXEC](../../t-sql/statements/set-noexec-transact-sql.md)<br /><br /> [SET NUMERIC_ROUNDABORT](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)<br /><br /> [SET PARSEONLY](../../t-sql/statements/set-parseonly-transact-sql.md)<br /><br /> [SET QUERY_GOVERNOR_COST_LIMIT](../../t-sql/statements/set-query-governor-cost-limit-transact-sql.md)<br /><br /> [結果セット キャッシュの設定](../../t-sql/statements/set-result-set-caching-transact-sql.md?view=azure-sqldw-latest) (プレビュー)<br /> 注:この機能は Azure SQL Data Warehouse にのみ適用されます。<br /><br /> [SET ROWCOUNT](../../t-sql/statements/set-rowcount-transact-sql.md)<br /><br /> [SET TEXTSIZE](../../t-sql/statements/set-textsize-transact-sql.md)|  
|ISO 設定ステートメント|[SET ANSI_DEFAULTS](../../t-sql/statements/set-ansi-defaults-transact-sql.md)<br /><br /> [SET ANSI_NULL_DFLT_OFF](../../t-sql/statements/set-ansi-null-dflt-off-transact-sql.md)<br /><br /> [SET ANSI_NULL_DFLT_ON](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)<br /><br /> [SET ANSI_NULLS](../../t-sql/statements/set-ansi-nulls-transact-sql.md)<br /><br /> [SET ANSI_PADDING](../../t-sql/statements/set-ansi-padding-transact-sql.md)<br /><br /> [SET ANSI_WARNINGS](../../t-sql/statements/set-ansi-warnings-transact-sql.md)|  
|統計ステートメント|[SET FORCEPLAN](../../t-sql/statements/set-forceplan-transact-sql.md)<br /><br /> [SET SHOWPLAN_ALL](../../t-sql/statements/set-showplan-all-transact-sql.md)<br /><br /> [SET SHOWPLAN_TEXT](../../t-sql/statements/set-showplan-text-transact-sql.md)<br /><br /> [SET SHOWPLAN_XML](../../t-sql/statements/set-showplan-xml-transact-sql.md)<br /><br /> [SET STATISTICS IO](../../t-sql/statements/set-statistics-io-transact-sql.md)<br /><br /> [SET STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md)<br /><br /> [SET STATISTICS PROFILE](../../t-sql/statements/set-statistics-profile-transact-sql.md)<br /><br /> [SET STATISTICS TIME](../../t-sql/statements/set-statistics-time-transact-sql.md)|  
|トランザクション ステートメント|[[SET IMPLICIT_TRANSACTIONS]](../../t-sql/statements/set-implicit-transactions-transact-sql.md)<br /><br /> [SET REMOTE_PROC_TRANSACTIONS](../../t-sql/statements/set-remote-proc-transactions-transact-sql.md)<br /><br /> [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)<br /><br /> [SET XACT_ABORT](../../t-sql/statements/set-xact-abort-transact-sql.md)| 
  
## <a name="considerations-when-you-use-the-set-statements"></a>SET ステートメントの使用に関する注意点  
  
- すべての SET ステートメントは実行時に実行されますが、次のステートメントは解析時に実行されます。

  - SET FIPS_FLAGGER
  - SET OFFSETS
  - [SET PARSEONLY]
  - SET QUOTED_IDENTIFIER  
  
- SET ステートメントをストアド プロシージャまたはトリガー内で実行した場合、SET オプションの値は、ストアド プロシージャやトリガーから制御が返された後、元に戻されます。 また、動的 SQL 文字列内で SET ステートメントを指定し、これを **sp_executesql** または EXECUTE で実行した場合、SET オプションの値は、動的 SQL 文字列で指定したバッチから制御が返された後、元に戻されます。  
  
- ストアド プロシージャでは、SET ANSI_NULLS と SET QUOTED_IDENTIFIERS を除き、実行時に指定した SET 設定が使用されます。 SET ANSI_NULLS または SET QUOTED_IDENTIFIER を指定するストアド プロシージャの場合は、ストアド プロシージャの作成時に指定した設定が使用されます。 ストアド プロシージャの内部で使用する場合、SET 設定は無視されます。  
  
- **sp_configure** の **user options** 設定を使用すると、サーバー単位で設定が行えます。この設定は複数のデータベースに対して有効です。 この設定は明示的な SET ステートメントと同じように動作しますが、ログイン時に使用される点が異なります。  
  
- ALTER DATABASE を使用して設定したデータベース設定は、データベース レベルで有効です。これは明示的に設定された場合のみ有効になります。 データベース設定は、**sp_configure** を使用して設定したインスタンス オプションの設定をオーバーライドします。  
  
- SET ステートメントで ON と OFF が使用される場合、複数の SET オプションに対していずれかを指定できます。
  
    > [!NOTE]  
    >  これは、統計情報に関連する SET オプションでは適用されません。
  
     たとえば `SET QUOTED_IDENTIFIER, ANSI_NULLS ON` を使用すると、QUOTED_IDENTIFIER と ANSI_NULLS の両方を ON に設定できます。  
  
- SET ステートメントの設定は、ALTER DATABASE を使用して設定した同一のデータベース オプションの設定をオーバーライドします。 たとえば、SET ANSI_NULLS ステートメントで指定した値は、ANSI_NULLS のデータベース設定よりも優先されます。 さらに、前回 **sp_configure user options** 設定を使用したときに有効になった値や、すべての ODBC および OLE/DB 接続に適用される値を使用してデータベースに接続すると、自動的に ON になる接続設定がいくつかあります。  
  
- ALTER、CREATE、DROP DATABASE ステートメントでは、SET LOCK_TIMEOUT の設定は無視されます。  
  
- グローバルまたはショートカット SET ステートメントでいくつかの設定を行っている場合、ショートカット SET ステートメントを実行すると、そのショートカット SET ステートメントの影響を受けるすべてのオプションに関する既存の設定がリセットされます。 ショートカット SET ステートメントを実行した後、ショートカット SET ステートメントの影響を受ける SET オプションを設定した場合は、個別の SET ステートメントの値の方が、同等のショートカットの設定よりも優先されます。 ショートカット SET ステートメントには SET ANSI_DEFAULTS などがあります。  
  
- バッチを使用する場合、データベースのコンテキストは、USE ステートメントを使って確立したバッチによって決まります。 ストアド プロシージャの外部で実行される、バッチ内の計画外クエリとその他すべてのステートメントは、USE ステートメントによって確立されるデータベースと接続のオプション設定を継承します。  
  
- 複数のアクティブな結果セット (MARS) 要求では、グローバル状態が共有されます。この状態には、最新のセッションでの SET オプション設定が含まれます。 各要求を実行するとき、SET オプションを変更できます。 この変更は対象となる要求のコンテキストだけに適用され、同時実行される他の MARS 要求には影響しませんが、 要求の実行が完了した後に、新しい SET オプションがグローバル セッション状態にコピーされます。 この変更後、同じセッションで実行される新しい要求では、これらの新しい SET オプション設定が使用されます。  
  
- バッチまたは他のストアド プロシージャからストアド プロシージャが実行された場合、そのストアド プロシージャが格納されているデータベースに設定されているオプション値で実行されます。 たとえば、ストアド プロシージャ **db1.dbo.sp1** でストアド プロシージャ **db2.dbo.sp2** を呼び出す場合、ストアド プロシージャ **sp1** はデータベース **db1** の現在の互換性レベル設定で実行され、ストアド プロシージャ **sp2** はデータベース **db2** の現在の互換性レベル設定で実行されます。  
  
- [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが複数のデータベースにあるオブジェクトに関係するとき、現在のデータベース コンテキストと現在の接続コンテキストがそのステートメントに適用されます。 ここで、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがバッチ内にある場合、現在の接続コンテキストは USE ステートメントで定義したデータベースになります。[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがストアド プロシージャ内にある場合、接続コンテキストはそのストアド プロシージャが格納されているデータベースになります。  
  
- 計算列やインデックス付きビューを作成し、操作しているとき、次の SET オプションを ON に設定する必要があります。ARITHABORT、CONCAT_NULL_YIELDS_NULL、QUOTED_IDENTIFIER、ANSI_NULLS、ANSI_PADDING、ANSI_WARNINGS。 NUMERIC_ROUNDABORT オプションは OFF に設定します。  
  
  これらのオプションのうち 1 つでも正しく設定しなかった場合は、インデックス付きビューに対して、または計算列にインデックスが含まれているテーブルに対して INSERT、UPDATE、DELETE、DBCC CHECKDB、DBCC CHECKTABLE を実行すると操作は失敗します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではエラーが発生し、正しく設定されなかったすべてのオプションが一覧表示されます。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、このようなテーブルやインデックス付きビューに対して SELECT ステートメントを実行すると、計算列またはビューにインデックスが存在しないものとして処理されます。 

- SET RESULT_SET_CACHING が ON の場合、現在のクライアント セッションの結果のキャッシュ機能が有効になります。   Result_set_caching がデータベース レベルで OFF にされていた場合、これをセッションで ON にすることはできません。    SET RESULT_SET_CACHING が OFF の場合、現在のクライアント セッションの結果セットのキャッシュ機能が無効になります。 この設定を変更するには、public ロールのメンバーシップが必要です。
適用対象:Azure SQL Data Warehouse Gen2
