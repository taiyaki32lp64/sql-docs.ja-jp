---
title: RESTORE の引数 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE statement, arguments
- RESTORE statement
ms.assetid: 4bfe5734-3003-4165-afd4-b1131ea26e2b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a39f9cf72f08e80face176412851778f1afec174
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982459"
---
# <a name="restore-statements---arguments-transact-sql"></a>RESTORE ステートメントの引数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

このトピックでは、RESTORE {DATABASE|LOG} ステートメントと、関連する補助ステートメントRESTORE FILELISTONLY、RESTORE HEADERONLY、RESTORE LABELONLY、RESTORE REWINDONLY、および RESTORE VERIFYONLY の「構文」に記載されている引数について説明します。 ほとんどの引数は、これら 6 つのステートメントでのみ使用できます。 各引数のサポート状況については、引数の説明で示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
 構文については、次のトピックを参照してください。  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
-   [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)  
  
-   [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
## <a name="arguments"></a>引数  
 DATABASE  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 対象のデータベースを指定します。 ファイルとファイル グループのリストを指定した場合は、そのファイルとファイル グループだけが復元されます。  
  
 データベースで完全な復旧モデルまたは一括ログ復旧モデルを使用しているときは、ほとんどの場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではデータベースの復元前にログ末尾のバックアップが必要になります。 RESTORE DATABASE ステートメントに WITH REPLACE 句または WITH STOPAT 句が指定されていない場合、最初にログ末尾のバックアップを行わずに、データベースを復元しようとするとエラーが発生します。これらの句は、データのバックアップ終了後の時間またはトランザクションの指定が必要となる句です。 ログ末尾のバックアップの詳細については、「[ログ末尾のバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)」をご覧ください。  
  
 LOG  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 トランザクション ログ バックアップをこのデータベースに適用することを指定します。 トランザクション ログは順番に適用する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、バックアップされたトランザクション ログがチェックされ、トランザクションが正しいデータベースに正しい順序で読み込まれていることが確認されます。 複数のトランザクション ログを適用するには、最後の復元操作を除くすべての復元操作で NORECOVERY オプションを使用します。  
  
> [!NOTE]  
>  通常、最後に復元されるログは、ログ末尾のバックアップです。 *ログ末尾のバックアップ* は、データベースを復元する直前 (通常は、データベースでの失敗の後) に行われるログ バックアップです。 損傷した可能性があるデータベースに関するログ末尾のバックアップを使用すると、まだバックアップされていないログ (ログの末尾) がキャプチャされるので、作業の抜けや失敗を防ぐことができます。 詳細については、「[ログ末尾のバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)」を参照してください。  
  
 詳細については、「[トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)」を参照してください。  
  
 { _database\_name_ |  **@** _database\_name\_var_}  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 ログまたはデータベース全体の復元先データベースを指定します。 変数 ( **@** _database\_name\_var_) として指定する場合、この名前は、文字列定数 ( **@** _database\_name\_var_ = *database*\_*name*) として、または **ntext** や **text** データ型を除く、文字列データ型の変数として指定できます。  
  
 \<file_or_filegroup_or_page> [ **,** ...*n* ]  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 RESTORE DATABASE または RESTORE LOG ステートメントに含める論理ファイル、論理ファイル グループ、またはページの名前を指定します。 ファイルまたはファイル グループのリストを指定できます。  
  
 単純復旧モデルを使用するデータベースでは、FILE および FILEGROUP オプションは、対象のファイルまたはファイル グループが読み取り専用の場合、またはこれが PARTIAL 復元である場合 (結果として[ファイル グループの機能停止](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)につながる) にのみ指定できます。  
  
 データベースで完全復旧モデルまたは一括ログ復旧モデルを使用している場合、RESTORE DATABASE を使用して 1 つ以上のファイル、ファイル グループ、ページを復元した後では、通常、復元したデータを含むこれらのファイルにトランザクション ログを適用する必要があります。トランザクション ログを適用すると、これらのファイルとデータベースの残りの部分の一貫性がとれるようになります。 ただし、次の場合は例外となります。  
  
-   復元するファイルが、前回のバックアップ時まで読み取り専用であった場合。この場合、トランザクション ログを適用する必要はありません。RESTORE ステートメントではこの状況が報告されます。  
  
-   バックアップにプライマリ ファイル グループが含まれており、部分バックアップを実行する場合。 この場合、バックアップ セットから自動的にログが復元されるので、復元ログは必要ありません。  
  
FILE **=** { *logical_file_name_in_backup*|  **@** _logical\_file\_name\_in\_backup\_var_}  
 データベースの復元に含めるファイルの名前を指定します。  
  
FILEGROUP **=** { *logical_filegroup_name* |  **@** _logical\_filegroup\_name\_var_ }  
 データベースの復元に含めるファイル グループの名前を指定します。  
  
 **注** 指定したファイル グループが読み取り専用で、これが部分復元である場合 (つまり、WITH PARTIAL が使用される場合)、FILEGROUP は単純復旧モデルでのみ使用できます。 復元されなかった読み書き可能なファイル グループは機能していないとマークされ、ここで復元されたデータベースには以降復元できなくなります。  
  
READ_WRITE_FILEGROUPS  
 読み書き可能なファイル グループをすべて選択します。 このオプションは、読み書き可能なファイル グループを復元した後で、読み取り専用のファイル グループを復元する場合に特に便利です。  
  
PAGE = **'** _file_ **:** _page* [ **,** ...*n* ] **'**  
 ページ復元の対象となる 1 ページまたは複数ページのリストを指定します (ページ復元は、完全復旧モデルまたは一括ログ復旧モデルを使用しているデータベースに対してのみサポートされています)。 値は次のとおりです。  
  
PAGE  
 1 つ以上のファイルおよびページで構成されるリストです。  
  
 *file*  
 復元する特定ページを含むファイルのファイル ID です。  
  
 *page*  
 ファイル内の復元対象ページのページ ID です。  
  
 *n*  
 複数のページを指定できることを示すプレースホルダーです。  
  
 復元シーケンスで 1 つのファイルに復元できる最大ページ数は、1,000 ページです。 ただし、ファイルに含まれる損傷ページの数が多い場合は、ページでなくファイル全体を復元することをお勧めします。  
  
> [!NOTE]  
>  ページ復元は復旧されません。  
  
 ページ復元の詳細については、「[ページ復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)」を参照してください。  
  
 [ **,** ...*n* ]  
 複数のファイル、ファイル グループ、およびページをコンマ区切りリストに指定できることを示すプレースホルダーです。 数の制限はありません。  
  
FROM { \<backup_device> [ **,** ...*n* ]| \<database_snapshot> } 通常、バックアップを復元する元のバックアップ デバイスを指定します。 または、RESTORE DATABASE ステートメントの中で FROM 句を使用して、データベースを元に戻すためのデータベース スナップショットの名前を指定することもできます。この場合、WITH 句は使用できません。  
  
 FROM 句を省略した場合、バックアップの復元は行われず、 代わりにデータベースが復旧されます。 この機能により、NORECOVERY オプションで復元されているデータベースを復旧したり、スタンバイ サーバーに切り替えたりすることができます。 FROM 句を省略する場合は、WITH 句の中で NORECOVERY、RECOVERY、または STANDBY を指定する必要があります。  
  
 \<backup_device> [ **,** ...*n* ] 復元操作に使用する論理または物理バックアップ デバイスを指定します。  
  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)、[RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)、[RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)、[RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)、[RESTORE REWINDONLY](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)、[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。  
  
 \<backup_device>::= バックアップ操作に使用する論理または物理バックアップ デバイスを、次のように指定します。  
  
 { _logical\_backup\_device\_name_ |  **@** _logical\_backup\_device\_name\_var_ }  
 データベースの復元元である、**sp_addumpdevice** で作成されたバックアップ デバイスの論理名を指定します。この名前は識別子の規則に従っている必要があります。 変数 ( **@** _logical\_backup\_device\_name\_var_) として指定する場合、バックアップ デバイス名は、文字列定数 ( **@** _logical\_backup\_device\_name\_var_ = _logical\_backup\_device\_name_) として、または **ntext** や **text** データ型を除く、文字の文字列データ型の変数として指定できます。  
  
 {DISK | TAPE } **=** { **'** _physical\_backup\_device\_name_ **'**  |  **@** _physical\_backup\_device\_name\_var_ }  
 指定したディスク デバイスまたはテープ デバイスから、バックアップを復元することを許可します。 ディスクとテープのデバイスの種類は、`DISK ='Z:\SQLServerBackups\AdventureWorks.bak'` や `TAPE ='\\\\.\TAPE0'` のように、デバイスの実際の名前 (たとえば、完全なパスとファイル名) を使用して指定する必要があります。 変数 ( **@** _physical\_backup\_device\_name\_var_) として指定する場合、デバイス名は、文字列定数 ( **@** _physical\_backup\_device\_name\_var_ = '*physical_backup_device_name*') として、または **ntext** や **text** データ型を除く、文字の文字列データ型の変数として指定できます。  
  
 UNC 名 (マシン名を含む必要があります) を持つネットワークサーバーを使用している場合は、ディスクのデバイスの種類を指定します。 UNC 名を使用する方法の詳細については、「[バックアップ デバイス &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)」を参照してください。  
  
 RESTORE 操作を実行するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行するアカウントに、リモート コンピューターまたはネットワーク サーバーへの読み取りアクセス権が与えられている必要があります。  
  
 *n*  
 最大 64 個のバックアップ デバイスをコンマ区切りリストに指定できることを示すプレースホルダーです。  
  
 以下に示すように、復元シーケンスで必要になるバックアップ デバイスの数が、バックアップが含まれるメディア セットの作成で使用したデバイスの数と同じになるかどうかは、復元をオフラインとオンラインのどちらで行うかによって決まります。  
  
-   オフライン復元の場合は、バックアップの作成時よりも少ない数のデバイスでバックアップを復元できます。  
  
-   オンライン復元の場合は、バックアップの作成時に使用されたすべてのバックアップ デバイスが必要です。 それより少ない数のデバイスで復元しようとしても失敗します。  
  
 たとえば、サーバーに接続している 4 つのテープ ドライブに、データベースがバックアップされているとします。 これをオンライン復元する場合は、サーバーに 4 つのドライブを接続する必要がありますが、オフライン復元する場合は、マシンに接続しているドライブが 3 つ以下でもバックアップを復元できます。  
  
> [!NOTE]  
>  ミラー化メディア セットからバックアップを復元する場合は、各メディア ファミリに対して 1 つのミラーだけを指定できます。 エラーが発生したとき、他に複数のミラーを用意しておくと復元に関する問題をすばやく解決できる場合があります。 損傷したメディア ボリュームは、別のミラーの対応するボリュームで代替できます。 オフライン復元の場合は、メディア ファミリの数よりも少ない数のデバイスから復元できますが、各ファミリは一度しか処理されないことに注意してください。  
  
\<database_snapshot>::=  
**サポートしているステートメント:** [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
DATABASE_SNAPSHOT **=** _database\_snapshot\_name_  
 *database_snapshot_name* で指定したデータベース スナップショットにデータベースを戻します。 DATABASE_SNAPSHOT オプションは、データベース全体の復元にのみ使用できます。 元に戻す操作では、データベース スナップショットがデータベース全体のバックアップの代わりとなります。  
  
 指定したデータベース スナップショットが、データベース上の唯一のデータベース スナップショットであることが必要です。 元に戻す操作の実行中は、データベース スナップショットと出力先データベースの両方が `In restore` としてマークされます。 詳細については、「[RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)」の「解説」セクションを参照してください。  
  
### <a name="with-options"></a>WITH オプション  
 復元操作で使用するオプションを指定します。 各オプションを使用するステートメントの一覧については、このトピックに後述される「WITH オプションと対応ステートメントの一覧」を参照してください。  
  
> [!NOTE]  
>  ここでは、WITH オプションが「[RESTORE {DATABASE|LOG}](../../t-sql/statements/restore-statements-transact-sql.md)」の「構文」セクションと同じ順序で構成されています。  
  
 PARTIAL  
 **サポートしているステートメント:** [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 部分復元操作で、プライマリ ファイル グループと指定したセカンダリ ファイル グループを復元することを指定します。 PARTIAL オプションでは暗黙的にプライマリ ファイル グループが選択されるので、FILEGROUP = 'PRIMARY' を指定する必要はありません。 セカンダリ ファイル グループを復元するには、FILE オプションまたは FILEGROUP オプションで明示的にファイル グループを指定する必要があります。  
  
 PARTIAL オプションは、RESTORE LOG ステートメントでは使用できません。  
  
 PARTIAL オプションによって段階的な部分復元の初期段階を開始できるようになりました。この場合、残りのファイル グループは後で復元することができます。 詳細については、「[段階的な部分復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)」を参照してください。  
  
 [ **RECOVERY** | NORECOVERY | STANDBY ]  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 **RECOVERY**  
 復元操作に対して、コミットされていないトランザクションをロールバックすることを指定します。 復元操作の後、データベースは使用可能な状態になります。 NORECOVERY、RECOVERY、または STANDBY のいずれも指定しない場合は、RECOVERY が既定値になります。  
  
 この後 RESTORE 操作 (差分バックアップからの RESTORE LOG または RESTORE DATABASE) を予定している場合は、代わりに NORECOVERY または STANDBY を指定してください。  
  
 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で作成したバックアップ セットを復元するときには、データベースのアップグレードが必要になる場合があります。 このアップグレードは、WITH RECOVERY が指定されていれば自動的に実行されます。 詳細については、「[トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  FROM 句を省略する場合は、WITH 句の中で NORECOVERY、RECOVERY、または STANDBY を指定する必要があります。  
  
 NORECOVERY  
 復元操作に対して、コミットされていないトランザクションをロールバックしないことを指定します。 別のトランザクション ログを後で適用する必要がある場合は、NORECOVERY または STANDBY オプションのいずれかを指定してください。 NORECOVERY、RECOVERY、または STANDBY のいずれも指定しない場合は、RECOVERY が既定値になります。 NORECOVERY オプションを使用したオフライン復元操作が行われている間、データベースは使用できません。  
  
 データベース バックアップと 1 つ以上のトランザクション ログを復元する場合や、複数の RESTORE ステートメントが必要な場合 (データベース全体を復元してからデータベースの差分バックアップを復元する場合など) は、最後の RESTORE ステートメントを除くすべての RESTORE ステートメントに、WITH NORECOVERY オプションを指定する必要があります。 推奨事項としては、複数段階に分かれた復元シーケンスで、すべてのステートメントに WITH NORECOVERY を使用して目的の復旧ポイントまで復旧を行います。その後で、個別の RESTORE WITH RECOVERY ステートメントを使用して、復旧のみを行うことをお勧めします。  
  
 ファイルまたはファイル グループの復元操作で NORECOVERY を使用した場合、データベースは復元操作の後も復元中の状態になります。 これは、次の状況で効果的です。  
  
-   復元スクリプトが実行されていて、ログが常に適用される場合。  
  
-   ファイルが順番に復元されており、2 つの復元操作の間でデータベースを使用できないようにする場合。  
  
 場合によっては、RESTORE WITH NORECOVERY では、ロールフォワード セットがデータベースとの一貫性を保てるポイントまでロールフォワードされることがあります。 このような場合、ロールバックは発生せず、データはオフラインのままになります。これはこのオプションに想定されている動作ですが、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]からは情報メッセージが返され、RECOVERY オプションを使用してロールフォワード セットを復元できるようになったことが示されます。  
  
STANDBY **=** _standby\_file\_name_  
 スタンバイ ファイルを指定します。このファイルを使用すると、復旧の結果を元に戻すことができます。 STANDBY オプションは、部分復元を含むオフライン復元で使用でき、 オンライン復元では使用できません。 オンライン復元操作に STANDBY オプションを指定すると、復元操作は失敗します。 また、データベースのアップグレードが必要な場合も、STANDBY は使用できません。  
  
 スタンバイ ファイルは、RESTORE WITH STANDBY の Undo パスにおいて変更されるページに対して、"書き込み時コピー" のプリイメージを保持するために使用されます。 スタンバイ ファイルを使用すると、トランザクション ログの復元の間では、読み取り専用でデータベースにアクセスできます。また、このファイルは、ウォーム スタンバイ サーバーを使用する場合や、特別な復旧状況 (ログの復元の間にデータベースを調査する場合など) で使用できます。 RESTORE WITH STANDBY 操作の後、次に RESTORE 操作を行うと、UNDO ファイルは自動的に削除されます。 次に RESTORE 操作を行う前にスタンバイ ファイルを手動で削除した場合は、データベース全体をもう一度復元する必要があります。 データベースが STANDBY の状態にある間、このスタンバイ ファイルは他のデータベース ファイルと同様に扱う必要があります。 ただし他のデータベース ファイルと異なり、このファイルは、アクティブな復元操作の実行中のみ、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって開かれたままになります。  
  
 *standby_file_name* では、場所がデータベースのログに格納されるスタンバイ ファイルを指定します。 指定した名前が既存のファイルのものである場合はファイルが上書きされ、そうでない場合は[!INCLUDE[ssDE](../../includes/ssde-md.md)]によってファイルが作成されます。  
  
 スタンバイ ファイルのサイズ要件は、復元操作において、コミットされていないトランザクションを元に戻す操作がどれだけあるかによって決まります。  
  
> [!IMPORTANT]  
>  指定したスタンバイ ファイルが格納されるドライブでディスク容量がなくなった場合、復元操作は停止します。  
  
 RECOVERY と NORECOVERY の比較については、「[RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)」の「解説」セクションを参照してください。  
  
LOADHISTORY  
 **サポートしているステートメント:** [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 復元操作で情報が **msdb** 履歴テーブルに読み込まれることを指定します。 LOADHISTORY オプションを指定した場合は、確認中の 1 つのバックアップ セットに対して、メディア セットに格納されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップに関する情報が、**msdb** データベース内のバックアップおよび復元履歴テーブルに読み込まれます。 履歴テーブルの詳細については、「[システム テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)」を参照してください。  
  
#### <a name="general_with_options--n-"></a>\<general_WITH_options> [ ,...n ]  
 RESTORE DATABASE および RESTORE LOG ステートメントでは、一般的な WITH オプションをすべて使用できます。 これらのオプションの一部は、以下で説明するように 1 つ以上の補助ステートメントでもサポートされます。  
  
##### <a name="restore-operation-options"></a>復元操作オプション  
 以下のオプションは、復元処理の動作に影響します。  
  
MOVE **'** _logical\_file\_name\_in\_backup_ **'** TO **'** _operating\_system\_file\_name_ **'** [ ...*n* ]  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)、[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 *logical_file_name_in_backup* で論理名が指定されるデータまたはログ ファイルを、*operating_system_file_name* で指定される場所に復元して移動するように指定します。 バックアップ セット内のデータ ファイルまたはログ ファイルの論理ファイル名は、バックアップ セットが作成されたときのデータベース内における論理名と同じです。  
  
*n* は追加の MOVE ステートメントを指定できることを示すプレースホルダーです。 バックアップ セットから新しい位置に復元する論理ファイルごとに、MOVE ステートメントを指定してください。 既定では、*logical_file_name_in_backup* ファイルが元の場所に復元されます。  
  
> [!NOTE]  
>  バックアップ セットに含まれる論理ファイルの一覧を取得するには、RESTORE FILELISTONLY を使用します。  
  
 RESTORE ステートメントを使用して、データベースを同じサーバーに再配置したり、別のサーバーにコピーするとき、データベース ファイルの再配置によって既存ファイルとの衝突が発生するのを防ぐために、MOVE オプションが必要になる場合があります。  
  
 RESTORE LOG で MOVE オプションを使用する場合は、復元するログの対象期間中に追加されたファイルを再配置するためにのみ使用してください。 たとえば、ログ バックアップにファイル `file23` のファイル追加操作が含まれる場合、このファイルは RESTORE LOG で MOVE オプションを使用して再配置することがあります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スナップショット バックアップで使用する際は、MOVE オプションは、元の BLOB と同じストレージ アカウント内の Azure BLOB にファイルを再配置する場合にのみ使用できます。 ローカル ファイルまたは別のストレージ アカウントには、スナップショット バックアップを復元するのには、MOVE オプションを使用できません。  
  
 RESTORE VERIFYONLY ステートメントを使用して、データベースを同じサーバーに再配置するか別のサーバーにコピーする場合は、対象となるサーバーに利用可能な容量が十分あるかどうか、および既存のファイルと衝突する可能性がないかどうかを確認するために、MOVE オプションが必要になる場合があります。  
  
 詳細については、「 [バックアップと復元によるデータベースのコピー](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)」を参照してください。  
  
CREDENTIAL  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)、[RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)、[RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)、[RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)、[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。  
  
**適用対象**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 以降
  
 Microsoft Azure Blob ストレージ サービスからバックアップを復元する場合にのみ使用されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 から [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] の場合、URL からの復元時にのみ、1 つのデバイスから復元できます。 URL からの復元時に複数のデバイスから復元するには、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)を使用する必要があります。また、Shared Access Signature (SAS) トークンを使用する必要があります。 詳細については、「[Microsoft Azure への SQL Server マネージド バックアップを有効にする](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)」と「[Simplifying creation of SQL Credentials with Shared Access Signature ( SAS ) tokens on Azure Storage with PowerShell](https://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx)」 (PowerShell を使用する Azure ストレージにおける Shared Access Signature (SAS) トークンでの SQL 資格情報の作成の簡素化) を参照してください。  
  
 [REPLACE]  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 指定したデータベースと同じ名前のデータベースが既に存在していても、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でデータベースとその関連ファイルを作成することを指定します。 この場合、既存のデータベースは削除されます。 REPLACE オプションを指定しない場合、安全性チェックが行われます。 これにより、他のデータベースを誤って上書きするのを防止できます。 安全性チェックで次の両方に該当した場合は、RESTORE DATABASE ステートメントで現在のサーバーにデータベースが復元されることはありません。  
  
-   RESTORE ステートメントで指定したデータベースが、現在のサーバー上に既に存在する。  
  
-   データベース名が、バックアップ セットに記録されているデータベース名と異なる。  
  
 REPLACE を指定すると、既存のファイルが復元するデータベースに属するかどうかを確認できない場合も、RESTORE でそのファイルを上書きできます。 通常、RESTORE では既存のファイルは上書きされません。 WITH REPLACE は、RESTORE LOG オプションと同じ方法で使用することもできます。  
  
 REPLACE はまた、データベースを復元する前のログ末尾のバックアップの要件をオーバーライドします。  
  
 REPLACE オプションを使用した場合の影響については、「[RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)」を参照してください。  
  
RESTART  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で中断されていた復元操作を再開することを指定します。 RESTART では、中断された時点から復元操作が再開されます。  
  
RESTRICTED_USER  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)。  
  
 新しく復元したデータベースへのアクセスを、**db_owner**、**dbcreator**、または **sysadmin** ロールのメンバーに制限します。  RESTRICTED_USER は、DBO_ONLY に置き換わるオプションです。 DBO_ONLY は、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] で廃止されました。  
  
 RECOVERY オプションと共に使用します。  
  
##### <a name="backup-set-options"></a>バックアップ セット オプション  
 以下のオプションは、復元されるバックアップを含んでいるバックアップ セットに適用されます。  
  
FILE **=** { *backup_set_file_number* |  **@** _backup\_set\_file\_number_ }  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)、[RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)、[RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)、[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。  
  
 復元するバックアップ セットを特定します。 たとえば、 *1* の **backup_set_file_number** は、バックアップ 目での最初のバックアップ セットを示し、2 の *backup_set_file_number* は **2** 番目のバックアップ セットを示します。 バックアップ セットの *backup_set_file_number* を取得するには、 [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) ステートメントを使用します。  
  
 値を指定しない場合は、RESTORE HEADERONLY を除き、既定値の **1** が使用されます。RESTORE HEADERONLY では、メディア セットにあるすべてのバックアップ セットが処理されます。 詳細については、このトピック内の後にある「バックアップ セットの指定」を参照してください。  
  
> [!IMPORTANT]  
>  この FILE オプションには、データベース ファイルを指定するための FILE オプション (FILE **=** { *logical_file_name_in_backup* |  **@** _logical\_file\_name\_in\_backup\_var_ }) との関連はありません。  
  
 PASSWORD  **=** { *password* |  **@** _password\_variable_ }  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)、[RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)、[RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)、[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。  
  
 バックアップ セットのパスワードを指定します。 バックアップ セットのパスワードは文字列です。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 バックアップ セットの作成時にパスワードを設定した場合、このバックアップ セットから復元操作を実行するときにはそのパスワードが必要になります。 間違ったパスワードを指定した場合や、パスワードが設定されていないバックアップ セットにパスワードを指定した場合はエラーになります。  
  
> [!IMPORTANT]  
>  このパスワードは、メディア セットを保護する手段としては強力なものではありません。 詳細については、各ステートメントの「権限」を参照してください。  
  
##### <a name="media-set-options"></a>メディア セットのオプション  
 以下のオプションは、メディア セット全般に適用されます。  
  
 MEDIANAME **=** { *media_name* |  **@** _media\_name\_variable_}  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)、[RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)、[RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)、[RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)、[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。  
  
 メディアの名前を指定します。 メディア名を指定する場合、その名前がバックアップ ボリューム上のメディア名と一致している必要があります。一致していない場合、復元操作は終了します。 RESTORE ステートメントにメディア名を指定しない場合は、バックアップ ボリューム上のメディア名と一致するかどうかの確認は行われません。  
  
> [!IMPORTANT]  
>  バックアップ操作と復元操作で同じメディア名を一貫して使用することで、復元操作で選択されたメディアに対する安全性チェックが強化されます。  
  
 MEDIAPASSWORD **=** { *mediapassword* |  **@** _mediapassword\_variable_ }  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)、[RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)、[RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)、[RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)、[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。  
  
 メディア セットのパスワードを指定します。 メディア セットのパスワードは文字列です。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 メディア セットのフォーマット時にパスワードを設定した場合、メディア セット上のバックアップ セットにアクセスするときにはそのパスワードが必要になります。 間違ったパスワードを指定した場合や、パスワードが設定されていないメディア セットにパスワードを指定した場合はエラーになります。  
  
> [!IMPORTANT]  
>  このパスワードは、メディア セットを保護する手段としては強力なものではありません。 詳細については、関連するステートメントの「権限」セクションを参照してください。  
  
 BLOCKSIZE **=** { *blocksize* |  **@** _blocksize\_variable_ }  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 物理ブロック サイズをバイト単位で指定します。 サポートされるサイズは、512、1024、2048、4096、8192、16384、32768、および 65536 (64 KB) バイトです。 テープ デバイスの場合の既定値は 65536 バイトで、他のデバイスの場合の既定値は 512 バイトです。 通常は、RESTORE でデバイスに適するブロック サイズが自動的に選択されるので、このオプションは不要です。 ブロック サイズを明示的に指定すると、自動選択されたブロック サイズがオーバーライドされます。  
  
 CD-ROM からバックアップを復元する場合は、BLOCKSIZE=2048 と指定します。  
  
> [!NOTE]  
>  このオプションがパフォーマンスに影響するのは、通常、テープ デバイスから読み取るときだけです。  
  
##### <a name="data-transfer-options"></a>データ転送オプション  
 このオプションでは、バックアップ デバイスからのデータ転送を最適化できます。  
  
 BUFFERCOUNT **=** { *buffercount* |  **@** _buffercount\_variable_ }  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 復元操作に使用される I/O バッファーの総数を指定します。 任意の正の整数を指定できますが、バッファー数が多いと Sqlservr.exe プロセス内で仮想アドレス空間が不足し、"メモリ不足" エラーが発生する場合があります。  
  
 バッファーで使用される領域の合計は、_buffercount_* *\** _maxtransfersize_ で決定されます。  
  
 MAXTRANSFERSIZE **=** { _maxtransfersize_ |  **@** _maxtransfersize\_variable_ }  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 バックアップ メディアと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の間で使用される最大転送単位をバイト単位で指定します。 有効値は 65536 バイト (64 KB) の倍数で、最大有効値は 4194304 バイト (4 MB) です。  
> [!NOTE]  
>  データベースで FILESTREAM が構成されているか、メモリ内 OLTP ファイル グループが含まれている場合、復元時の `MAXTRANSFERSIZE` は、バックアップの作成時に使用されたものより大きくなります。  
  
##### <a name="error-management-options"></a>エラー管理オプション  
 このオプションでは、復元操作でバックアップのチェックサムを有効にするかどうか、およびエラー発生時に操作を停止するかどうかを指定できます。    
  
 { CHECKSUM | NO_CHECKSUM }  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)、[RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)、[RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)、[RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)、[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。  
  
 既定の動作では、チェックサムがある場合はチェックサムの確認が行われ、チェックサムがない場合は確認せずに動作が続行されます。  
  
 CHECKSUM  
 バックアップ チェックサムを必ず確認することを指定します。バックアップにバックアップ チェックサムがない場合、復元操作は失敗し、チェックサムがないことを示すメッセージが返されます。  
  
> [!NOTE]  
>  ページ チェックサムは、バックアップ チェックサムが使用されている場合にのみバックアップ操作に関連します。  
  
 既定では、無効なチェックサムが検出されると、RESTORE によってチェックサム エラーがレポートされ処理が停止します。 ただし、CONTINUE_AFTER_ERROR を指定した場合は、破損による影響がない限り、チェックサム エラーと無効なチェックサムを含むページ番号が返された後、RESTORE の処理が続行します。  
  
 バックアップ チェックサムの操作の詳細については、「[バックアップ中および復元中に発生する可能性があるメディア エラー &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)」を参照してください。  
  
 NO_CHECKSUM  
 復元操作によるチェックサムの検証を、明示的に無効にします。  
  
 { **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR }  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)、[RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)、[RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)、[RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)、[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。  
  
 STOP_ON_ERROR  
 最初にエラーが発生した時点で、復元操作を停止することを指定します。 これは RESTORE の既定の動作ですが、VERIFYONLY では既定の動作ではありません。VERIFYONLY の既定の動作は、CONTINUE_AFTER_ERROR になります。  
  
 CONTINUE_AFTER_ERROR  
 エラーが発生した後も、復元操作を続行することを指定します。  
  
 バックアップに破損したページが含まれている場合は、エラーがない別のバックアップ、たとえばページが破損する前に作成したバックアップなどを使用して、復元操作をもう一度実行することをお勧めします。 ただし、最終的な手段として、復元ステートメントの CONTINUE_AFTER_ERROR オプションを使用して破損したバックアップを復元し、データの復旧を試みることもできます。  
  
##### <a name="filestream-options"></a>FILESTREAM オプション  
 FILESTREAM ( DIRECTORY_NAME =*directory_name* )  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)、[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降
  
 Windows と互換性のあるディレクトリ名です。 この名前は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内のすべてのデータベース レベルの FILESTREAM ディレクトリ名の間で一意である必要があります。 一意性の比較では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の照合順序の設定とは関係なく、大文字と小文字は区別されません。  
  
##### <a name="monitoring-options"></a>監視オプション  
 このオプションでは、バックアップ デバイスからのデータ転送を監視できます。  
  
 STATS [ **=** _percentage_ ]  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)、[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 指定したパーセンテージが完了するたびにメッセージを表示します。進行状況を判断する場合に使用できます。 *percentage* を省略した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では約 10% 完了するごとにメッセージが表示されます。  
  
 STATS オプションでは、次のパーセンテージ間隔を報告するしきい値に達した時点までに、完了したパーセンテージを報告します。 このしきい値は、指定したパーセンテージを正確に反映するものではありません。たとえば、STATS=10 の場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)]では正確に 40% ではなく、43% の時点でメッセージが表示される場合があります。 大きいバックアップ セットの場合、これは重要な問題にはなりません。それは、完了した I/O コール間の完了パーセンテージの差異はそれほど大きくないためです。  
  
##### <a name="tape-options"></a>テープ オプション  
 このオプションはテープ デバイスにのみ適用されます。 テープ以外のデバイスが使用される場合、このオプションは無視されます。  
  
 { **REWIND** | NOREWIND }  
 このオプションはテープ デバイスにのみ適用されます。 テープ以外のデバイスが使用される場合、このオプションは無視されます。  
  
 REWIND  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)、[RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)、[RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)、[RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)、[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でテープを解放して巻き戻すように指定します。 既定値は REWIND です。  
  
 NOREWIND  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)、[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 これ以外の復元ステートメントで NOREWIND を指定するとエラーが発生します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でバックアップ操作後にテープを開いたままにしておくことを指定します。 このオプションを使用すると、1 つのテープに対して複数のバックアップ操作を実行する場合のパフォーマンスを向上できます。  
  
 NOREWIND は暗黙的に NOUNLOAD も意味しています。この 2 つのオプションを同一の RESTORE ステートメント内で同時に使用することはできません。  
  
> [!NOTE]  
>  NOREWIND を使用する場合、テープ ドライブの所有権は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスによって保持されます。同じプロセス内で実行される BACKUP ステートメントや RESTORE ステートメントで REWIND オプションまたは UNLOAD オプションが使用されるか、サーバー インスタンスがシャットダウンすると、所有権は解放されます。 テープを開いたままにすると、他のプロセスではそのテープにアクセスできません。 開いているテープの一覧を表示する方法、および開いているテープを閉じる方法については、「[バックアップ デバイス &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)」を参照してください。  
  
 { **UNLOAD** | NOUNLOAD }  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)、[RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)、[RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)、[RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)、[RESTORE REWINDONLY](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)、[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。  
  
 このオプションはテープ デバイスにのみ適用されます。 テープ以外のデバイスが使用される場合、このオプションは無視されます。  
  
> [!NOTE]  
>  UNLOAD または NOUNLOAD はセッションの設定であり、セッションが終了するまで、または代わりとなるオプションの指定によりリセットされるまで有効です。  
  
 UNLOAD  
 バックアップ完了後、テープの巻き戻しおよびアンロードを自動的に行います。 UNLOAD は、セッション開始時の既定値です。  
  
 NOUNLOAD  
 RESTORE 操作の後、テープ ドライブにテープを読み込んだままにすることを指定します。  
  
#### <a name="replication_with_option"></a><replication_WITH_option>  
 このオプションは、バックアップ作成時にデータベースがレプリケートされた場合にのみ使用します。  
  
 KEEP_REPLICATION  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
KEEP_REPLICATION は、ログ配布と共に動作するようにレプリケーションを設定する場合に使用します。 これによって、データベースのバックアップまたはログのバックアップをウォーム スタンバイ サーバーで復元し、データベースが復旧したときに、レプリケーションの設定が削除されるのを防ぐことができます。 NORECOVERY オプションを使用してバックアップを復元するときにこのオプションを指定することはできません。 復元の後、レプリケーションを確実に機能させるには、次のことが必要です。  
  
-   ウォーム スタンバイ サーバーにある **msdb** および **master** データベースが、プライマリ サーバーにある **msdb** および **master** データベースと同期していること。  
  
-   ウォーム スタンバイ サーバーの名前が、プライマリ サーバーと同じ名前に変更されていること。  
  
#### <a name="change_data_capture_with_option"></a><change_data_capture_WITH_option>  
 このオプションは、バックアップ作成時にデータベースで変更データ キャプチャが有効になっていた場合にのみ使用します。  
  
 KEEP_CDC  
 **サポートしているステートメント:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 KEEP_CDC は、データベースのバックアップまたはログのバックアップを別のサーバーで復元してデータベースを復旧するときに、変更データ キャプチャの設定が削除されないようにするために使用する必要があります。 NORECOVERY オプションを使用してバックアップを復元するときにこのオプションを指定することはできません。  
  
 KEEP_CDC を指定してデータベースを復元すると、変更データ キャプチャ ジョブは作成されません。 データベースを復元した後にログから変更を抽出するには、復元されたデータベースに対してキャプチャ プロセス ジョブとクリーンアップ ジョブを再作成します。 詳細については、「[sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)」を参照してください。  
  
 データベース ミラーリングでの変更データ キャプチャの使用については、「[変更データ キャプチャとその他の SQL Server 機能](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)」を参照してください。  
  
#### <a name="service_broker_with_options"></a>\<service_broker_WITH_options>  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] のメッセージ配信を有効または無効にするか、新しい [!INCLUDE[ssSB](../../includes/sssb-md.md)] 識別子を設定します。 このオプションは、バックアップ作成時にデータベースに対して [!INCLUDE[ssSB](../../includes/sssb-md.md)] が有効 (アクティブ) になっていた場合にのみ使用します。  
  
 { ENABLE_BROKER  | ERROR_BROKER_CONVERSATIONS  | NEW_BROKER }  
 **サポートしているステートメント:** [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 ENABLE_BROKER  
 復元の終わりに [!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージ配信を有効にして、メッセージをすぐに送信できるようにすることを指定します。 既定では、[!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージ配信は復元中に無効化されています。 データベースは、既存の Service Broker 識別子を保持します。  
  
 ERROR_BROKER_CONVERSATIONS  
 データベースがアタッチまたは復元されていることを示すエラーと共に、すべてのメッセージ交換を終了します。 これによりアプリケーションは、既存のメッセージ交換に対して、通常のクリーンアップを実行できます。 Service Broker メッセージ配信はこの操作が完了するまで無効になり、その後有効になります。 データベースは、既存の Service Broker 識別子を保持します。  
  
 NEW_BROKER  
 データベースに新しい Service Broker 識別子を割り当てることを指定します。 データベースは新しい Service Broker と見なされるため、データベースにおける既存のメッセージ交換は、終了ダイアログ メッセージを生成せずに、直ちに削除されます。 古い Service Broker 識別子を参照するルートは、新しい識別子を使用して作成し直す必要があります。  
  
#### <a name="point_in_time_with_options"></a>\<point_in_time_WITH_options>  
 **サポートしているステートメント:** [RESTORE {DATABASE|LOG}](../../t-sql/statements/restore-statements-transact-sql.md) および完全または一括ログ復旧モデルの場合のみ。  
  
 STOPAT、STOPATMARK、または STOPBEFOREMARK 句で目的の復旧ポイントを指定することで、特定の時点またはトランザクションにデータベースを復元できます。 指定された時間またはトランザクションへの復元は、常にログ バックアップから行われます。 復元シーケンスのすべての RESTORE ステートメントで、同一の STOPAT、STOPATMARK、STOPBEFOREMARK のいずれかの句で目的の時間またはトランザクションを指定する必要があります。  
  
 特定の時点への復元の前提条件として、最初にエンド ポイントが目的の復旧ポイントよりも前になっているデータベースの完全バックアップを復元する必要があります。 復元するデータベース バックアップを識別しやすくするには、RESTORE DATABASE ステートメントで WITH STOPAT、WITH STOPATMARK、WITH STOPBEFOREMARK のいずれかの句をオプションで指定し、指定した目的の時間に対してデータのバックアップが近すぎる場合はエラーが発生するようにします。 ただし、目的の時間が指定されている場合でも常にデータのバックアップ全体が復元されます。  
  
> [!NOTE]  
>  特定の時点を指定する WITH オプションは RESTORE_DATABASE と RESTORE_LOG で似ていますが、*mark_name* 引数をサポートするのは RESTORE LOG のみです。  
  
 { STOPAT | STOPATMARK | STOPBEFOREMARK }   
 
 STOPAT **=** { **'** _datetime_ **'**  |  **@** _datetime\_var* }  
 *datetime* または **@** _datetime\_var_ パラメーターで指定された日時の状態にデータベースを復元するように指定します。 日付と時刻の指定については、「[日付と時刻のデータ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)」を参照してください。  
  
 STOPAT に変数を使用する場合、変数は **varchar**、**char**、**smalldatetime**、または **datetime** データ型にする必要があります。 指定した日付と時刻以前に書き込まれたトランザクション ログ レコードだけが、データベースに適用されます。  
  
> [!NOTE]  
>  指定した STOPAT 時間が前回のログ バックアップ後である場合、データベースは、NORECOVERY を指定して RESTORE LOG を実行した場合と同様に、復旧されていない状態のままになります。  
  
 詳細については、「[SQL Server データベースを特定の時点に復元する &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)」を参照してください。  
  
 STOPATMARK **=** { **'** _mark\_name_ **'**  |  **'** lsn:_lsn\_number_ **'** } [ AFTER **'** _datetime_ **'** ]  
 復旧を、指定された復旧ポイントに指定します。 指定したトランザクションは復旧に含められますが、このトランザクションがコミットされるのは、トランザクションの実際の生成時に既にコミットされていた場合のみです。  
  
 RESTORE DATABASE と RESTORE LOG の両方で *lsn_number* パラメーターがサポートされます。 このパラメーターは、ログ シーケンス番号を指定します。  
  
 *mark_name* パラメーターは、RESTORE LOG ステートメントでのみサポートされます。 このパラメーターは、ログ バックアップでトランザクション マークを識別します。  
  
 RESTORE LOG ステートメントでは、AFTER *datetime* を省略すると、指定された名前の最初のマークで復旧が停止します。 AFTER *datetime* を指定すると、*datetime* 以降の指定した名前を持つ最初のマークで復旧が停止します。  
  
> [!NOTE]  
>  指定したマーク LSN または時間が前回のログ バックアップ後である場合、データベースは、NORECOVERY を指定して RESTORE LOG を実行した場合と同様に、復旧されていない状態のままになります。  
  
 詳細については、「[マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)」と「[ログ シーケンス番号への復旧 &#40;SQL Server&#41;](../../relational-databases/backup-restore/recover-to-a-log-sequence-number-sql-server.md)」を参照してください。  
  
 STOPBEFOREMARK **=** { **'** _mark\_name_ **'**  |  **'** lsn:_lsn\_number_ **'** } [ AFTER **'** _datetime_ **'** ]  
 復旧を、指定された復旧ポイントまでに指定します。 指定したトランザクションは復旧に含められず、WITH RECOVERY を使用していればロールバックされます。  
  
 RESTORE DATABASE と RESTORE LOG の両方で *lsn_number* パラメーターがサポートされます。 このパラメーターは、ログ シーケンス番号を指定します。  
  
 *mark_name* パラメーターは、RESTORE LOG ステートメントでのみサポートされます。 このパラメーターは、ログ バックアップでトランザクション マークを識別します。  
  
 RESTORE LOG ステートメントでは、AFTER *datetime* を省略すると、指定した名前の最初のマークの直前に復旧が停止します。 AFTER *datetime* を指定すると、*datetime* 以降の指定した名前を持つ最初のマークの直前に復旧が停止します。  
  
> [!IMPORTANT]  
>  部分復元シーケンスで FILESTREAM ファイル グループを除外した場合、特定の時点への復元はサポートされません。 復元シーケンスを強制的に実行して続行することもできます。 ただし、RESTORE ステートメントから除外された FILESTREAM ファイル グループは復元できません。 特定の時点への復元を強制的に実行するには、STOPAT、STOPATMARK、または STOPBEFOREMARK オプションに CONTINUE_AFTER_ERROR オプションを組み合わせて指定します。 CONTINUE_AFTER_ERROR を指定した場合、部分復元シーケンスは正常に実行されますが、FILESTREAM ファイル グループは復元できなくなります。  
  
## <a name="result-sets"></a>結果セット  
 結果セットについては、次のトピックを参照してください。  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
## <a name="remarks"></a>Remarks  
 追加説明については、次のトピックを参照してください。  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
-   [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)  
  
-   [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
## <a name="specifying-a-backup-set"></a>バックアップ セットの指定  
 *バックアップ セット* には、正常に終了した 1 つのバックアップ操作のバックアップが含まれます。 RESTORE、RESTORE FILELISTONLY、RESTORE HEADERONLY、および RESTORE VERIFYONLY ステートメントは、単一または複数の指定バックアップ デバイス上のメディア セット内にある単一のバックアップ セットに対して機能します。 該当するメディア セット内の必要なバックアップを指定する必要があります。 バックアップ セットの *backup_set_file_number* を取得するには、 [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) ステートメントを使用します。  
  
 復元するバックアップ セットを指定するときのオプションは次のとおりです。  
  
 FILE **=** { *backup_set_file_number* |  **@** _backup\_set\_file\_number_ }  
  
 ここで *backup_set_file_number* は、メディア セット内のバックアップの位置を示します。 たとえば、*backup_set_file_number* が 1 (FILE = 1) の場合はバックアップ メディア内の最初のバックアップ セット、*backup_set_file_number* が 2 (FILE = 2) の場合は 2 番目のバックアップ セットというように示されます。  
  
 次の表で説明するように、このオプションの動作はステートメントによって異なります。  
  
|ステートメントから削除してください。|バックアップ セットの FILE オプションの動作|  
|---------------|-----------------------------------------|  
|RESTORE|既定のバックアップ セット ファイル番号は 1 です。 1 つの RESTORE ステートメントでは、1 つのバックアップ セットの FILE オプションのみが許可されます。 ここではバックアップ セットを順序どおり指定することが重要です。|  
|RESTORE FILELISTONLY|既定のバックアップ セット ファイル番号は 1 です。|  
|RESTORE HEADERONLY|既定では、メディア セット内のすべてのバックアップ セットが処理されます。 RESTORE HEADERONLY の結果セットでは、メディア セット内における**位置**など、各バックアップ セットに関する情報が返されます。 特定のバックアップ セットの情報が返されるようにするには、その位置番号を FILE オプションの *backup_set_file_number* 値として使用します。<br /><br /> 注:テープ メディアの場合、RESTORE HEADER では、読み込まれているテープのバックアップ セットのみが処理されます。|  
|RESTORE VERIFYONLY|既定の *backup_set_file_number* は 1 です。|  
  
> [!NOTE]  
>  バックアップ セットを指定するための FILE オプションには、データベース ファイルを指定するための FILE オプション (FILE **=** { *logical_file_name_in_backup* |  **@** _logical\_file\_name\_in\_backup\_var_ }) との関連はありません。  
  
## <a name="summary-of-support-for-with-options"></a>WITH オプションのサポートの一覧  
 次の WITH オプションは、RESTORE ステートメントのみがサポートしています。BLOCKSIZE、BUFFERCOUNT、MAXTRANSFERSIZE、PARTIAL、KEEP_REPLICATION、{ RECOVERY | NORECOVERY | STANDBY }、REPLACE、RESTART、RESTRICTED_USER、{ STOPAT | STOPATMARK | STOPBEFOREMARK }  
  
> [!NOTE]  
>  PARTIAL オプションは、RESTORE DATABASE でのみ使用できます。  
  
 次の表は、1 つ以上のステートメントで使用できる WITH オプションと、各オプションの対応ステートメントの一覧です。 チェックマーク (√) はそのオプションが使用できることを示し、ダッシュ (-) は使用できないことを示します。  
  
|WITH のオプション|RESTORE|RESTORE FILELISTONLY|RESTORE HEADERONLY|RESTORE LABELONLY|RESTORE REWINDONLY|RESTORE VERIFYONLY|  
|-----------------|-------------|--------------------------|------------------------|-----------------------|------------------------|------------------------|  
|{ CHECKSUM<br /><br /> &#124; NO_CHECKSUM }|√|√|√|√|-|√|  
|{ CONTINUE_AFTER_ERROR<br /><br /> &#124; STOP_ON_ERROR }|√|√|√|√|-|√|  
|FILE<sup>1</sup>|√|√|√|-|-|√|  
|LOADHISTORY|-|-|-|-|-|√|  
|MEDIANAME|√|√|√|√|-|√|  
|MEDIAPASSWORD|√|√|√|√|-|√|  
|MOVE|√|-|-|-|-|√|  
|PASSWORD|√|√|√|-|-|√|  
|{ REWIND &#124; NOREWIND }|√|REWIND のみ|REWIND のみ|REWIND のみ|-|√|  
|STATS|√|-|-|-|-|√|  
|{ UNLOAD &#124; NOUNLOAD }|√|√|√|√|√|√|  
  
 <sup>1</sup> FILE **=** _backup\_set\_file\_number_。{FILE | FILEGROUP} とは異なります。  
  
## <a name="permissions"></a>アクセス許可  
 権限については、次のトピックを参照してください。  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
-   [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)  
  
-   [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
## <a name="examples"></a>使用例  
 例については、次のトピックを参照してください。  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [SQL Server データベースのバックアップと復元](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
  
  

