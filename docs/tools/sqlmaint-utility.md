---
title: sqlmaint Utility |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- database maintenance plans [SQL Server]
- sqlmaint utility
- maintaining databases [SQL Server]
- backups [SQL Server], sqlmaint utility
- command prompt utilities [SQL Server], sqlmaint
- maintenance plans [SQL Server], command prompt
- backing up [SQL Server], sqlmaint utility
ms.assetid: 937a9932-4aed-464b-b97a-a5acfe6a50de
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ecc0a38acd6ea00656e67e9f582a55c05ca15583
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986282"
---
# <a name="sqlmaint-utility"></a>sqlmaint ユーティリティ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **sqlmaint** ユーティリティは、1 つまたは複数のデータベース上で、指定された一連のメンテナンス操作を実行します。 **sqlmaint** を使用して、DBCC チェックの実行、データベースとデータベース トランザクション ログのバックアップ、統計の更新、およびインデックスの再構築を行います。 すべてのデータベース メンテナンス操作では、指定されたテキスト ファイル、HTML ファイル、または電子メール アカウントに送信できるレポートが生成されます。 **sqlmaint** は、以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]で作成されたデータベース メンテナンス プランを実行します。 コマンド プロンプトから [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] メンテナンス プランを実行するには、 [dtexec](../integration-services/packages/dtexec-utility.md)ユーティリティを使用します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../includes/ssnotedepnextavoid-md.md)] 代わりに、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] メンテナンス プラン機能を使用してください。 メンテナンス プランの詳細については、「 [メンテナンス プラン](../relational-databases/maintenance-plans/maintenance-plans.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlmaint   
[-?] |  
[  
     [-S server_name[\instance_name]]  
     [-U login_ID [-P password]]  
     {  
          [-D database_name | -PlanName name | -PlanID guid ]  
          [-Rpt text_file]  
          [-To operator_name]  
          [-HtmlRpt html_file [-DelHtmlRpt <time_period>] ]  
          [-RmUnusedSpace threshold_percentfree_percent]  
          [-CkDB | -CkDBNoIdx]  
          [-CkAl | -CkAlNoIdx]  
          [-CkCat]  
          [-UpdOptiStats sample_percent]  
          [-RebldIdx free_space]  
          [-SupportComputedColumn]  
          [-WriteHistory]  
          [  
               {-BkUpDB [backup_path] | -BkUpLog [backup_path] }  
               {-BkUpMedia  
                    {DISK [  
                           [-DelBkUps <time_period>]   
                           [-CrBkSubDir ]   
                           [-UseDefDir ]   
                          ]  
                     | TAPE   
                    }  
               }  
               [-BkUpOnlyIfClean]  
               [-VrfyBackup]  
          ]  
     }  
]  
<time_period> ::=  
number[minutes | hours | days | weeks | months]  
```  
  
## <a name="arguments"></a>引数  
 パラメーターとその値は、空白で区切る必要があります。 たとえば、 **-S** と *server_name*の間には空白が必要です。  
  
 **-?**  
 **sqlmaint** の構文ダイアグラムが返されます。 このパラメーターは単独で使用する必要があります。  
  
 **-S** _server_name_[ **\\** _instance\_name_]  
 対象となる [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のインスタンスを指定します。 サーバー上の [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]の既定のインスタンスに接続するには、_server\_name_ を指定します。 サーバー上の [!INCLUDE[ssDE](../includes/ssde-md.md)] の名前付きインスタンスに接続するには、_server\_name_ **\\** _instance\_name_ を指定します。 サーバーを指定しない場合、 **sqlmaint** は、ローカル コンピューター上にある [!INCLUDE[ssDE](../includes/ssde-md.md)] の既定のインスタンスに接続します。  
  
 **-U** _login_ID_  
 サーバーに接続するときに使用するログイン ID を指定します。 指定しない場合、 **sqlmaint** は [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 認証の使用を試みます。 *login_ID* に特殊文字が含まれる場合、特殊文字を二重引用符 (") で囲む必要があります。特殊文字が含まれない場合は、二重引用符は省略可能です。  
  
> [!IMPORTANT]  
>  可能な場合は、Windows 認証を使用します。  
  
 **-P** _password_  
 ログイン ID のパスワードを指定します。 **-U** パラメーターも指定されている場合にのみ有効です。 *password* に特殊文字が含まれる場合、特殊文字を二重引用符で囲む必要があります。特殊文字が含まれない場合は、二重引用符は省略可能です。  
  
> [!IMPORTANT]  
>  パスワードはマスクされません。 可能な場合は、Windows 認証を使用します。  
  
 **-D** _database_name_  
 メンテナンス操作の実行対象となるデータベースの名前を指定します。 *database_name* に特殊文字が含まれる場合、特殊文字を二重引用符で囲む必要があります。特殊文字が含まれない場合は、二重引用符は省略可能です。  
  
 **-PlanName** _name_  
 データベース メンテナンス プラン ウィザードを使用して定義される、データベース メンテナンス プランの名前を指定します。 **sqlmaint** が使用するプランの情報は、プラン内のデータベースのリストのみです。 他の **sqlmaint** パラメーターに指定するすべてのメンテナンス操作は、このデータベースのリストに適用されます。  
  
 **-PlanID** _guid_  
 データベース メンテナンス プラン ウィザードを使用して定義される、データベース メンテナンス プランのグローバル一意識別子 (GUID) を指定します。 **sqlmaint** が使用するプランの情報は、プラン内のデータベースのリストのみです。 他の **sqlmaint** パラメーターに指定するすべてのメンテナンス操作は、このデータベースのリストに適用されます。 このパラメーターの値は、msdb.dbo.sysdbmaintplans の plan_id 値に一致する必要があります。  
  
 **-Rpt** _text_file_  
 レポートの生成先となるファイルの完全なパスとファイル名を指定します。 レポートは画面上にも表示されます。 レポートによってファイル名に日時が追加され、バージョン情報が維持されます。 日時は、_*yyyyMMddhhmm*の形式で、ファイル名の最後 (ピリオドの前) に追加されます。 *yyyy* = 年、 *MM* = 月、 *dd* = 日、 *hh* = 時間、 *mm* = 分。  
  
 1996 年 12 月 1 日午前 10:23 に ユーティリティを実行し、 *text_file* 値が次のようになるとします。  
  
```  
c:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint.rpt  
```  
  
 生成されるファイル名は、次のようになります。  
  
```  
c:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint_199612011023.rpt  
```  
  
 *sqlmaint* がリモート サーバーにアクセスする場合、 **text_file** には、完全な汎用名前付け規則 (UNC) のファイル名を指定する必要があります。  
  
 **-To**  _operator_name_  
 生成されたレポートが SQL Mail を使用して送信される場合の、送信先となるオペレーターを指定します。  
  
 **-HtmlRpt** _html_file_  
 HTML レポートの生成先となるファイルの完全パスとファイル名を指定します。 **sqlmaint** は、 *-Rpt* パラメーターの場合と同じように、ファイル名に _ **yyyyMMddhhmm** 形式の文字列を追加してファイル名を生成します。  
  
 *sqlmaint* がリモート サーバーにアクセスする場合、 **html_file** には、完全な UNC ファイル名を指定する必要があります。  
  
 **-DelHtmlRpt** \<*time_period*>  
 レポート ファイル作成後の期間が \<*time_period*> を超える場合、レポート ディレクトリ内にあるすべての HTML レポートを削除します。 **-DelHtmlRpt** は、*html_file* パラメーターを基に生成されたパターンに適合する名前を持つファイルを検索します。 *html_file* が C:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint.htm の場合、 **-DelHtmlRpt** によって **sqlmaint** は、C:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint\*.htm というパターンに一致する名前を持つファイルを検索し、指定された \<*time_period*> より前のファイルをすべて削除します。  
  
 **-RmUnusedSpace** _threshold_percent free_percent_  
 **-D**に指定されたデータベースから使用されていない領域を削除します。 このオプションは、自動拡張が定義されているデータベースに対してのみ使用できます。 *Threshold_percent* は、 **sqlmaint** が使用されていないデータ領域を削除する基準となるデータベースのサイズを MB 単位で指定します。 データベースが *threshold_percent*より小さい場合、何も行われません。 *Free_percent* は、データベースに残す必要がある使用されていない領域の量を、データベースの最終的なサイズに対する割合として指定します。 たとえば、200 MB のデータベースに 100 MB のデータを取り込む場合、 *free_percent* に 10 を指定すると、最終的なデータベース サイズは 110 MB になります。 データベースが *free_percent* とデータベースのデータ量の合計より小さい場合、データベースは拡張されないことにご注意ください。 たとえば、108 MB のデータベースが 100 MB のデータを持つ場合、 *free_percent* に 10 を指定してもデータベースは 110 MB に拡張されず、108 MB のままです。  
  
 **-CkDB** |  **-CkDBNoIdx**  
 **-D**に指定されたデータベースで、DBCC CHECKDB ステートメント、または NOINDEX オプションを含んだ DBCC CHECKDB ステートメントを実行します。 詳細については、「DBCC CHECKDB」を参照してください。  
  
 *sqlmaint* を実行するときにデータベースが使用中の場合、 **text_file** に警告が書き込まれます。  
  
 **-CkAl** |  **-CkAlNoIdx**  
 **-D** に指定されたデータベースで、NOINDEX オプションを含んだ DBCC CHECKALLOC ステートメントを実行します。 詳細については、「[DBCC CHECKALLOC &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)」を参照してください。  
  
 **-CkCat**  
 **-D** に指定されたデータベースで、DBCC CHECKCATALOG (Transact-SQL) ステートメントを実行します。 詳細については、「[DBCC CHECKCATALOG &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md)」を参照してください。  
  
 **-UpdOptiStats** _sample_percent_  
 データベースの各テーブルで、次のステートメントを実行します。  
  
```  
UPDATE STATISTICS table WITH SAMPLE sample_percent PERCENT;  
```  
  
 テーブルが計算列を含む場合、 **-UpdOptiStats** を使用するときに **-SupportedComputedColumn**引数も指定する必要があります。  
  
 詳細については、「 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../t-sql/statements/update-statistics-transact-sql.md)で作成されたデータベース メンテナンス プランを実行します。  
  
 **-RebldIdx** _free_space_  
 FILL FACTOR とは逆の関係になる値として *free_space* の割合の値を使用し、対象データベースのテーブルのインデックスを再構築します。 たとえば、 *free_space* の割合が 30 の場合、使用される FILL FACTOR は 70 になります。 *free_space* の割合の値に 100 が指定された場合は、最初の FILL FACTOR 値を使用してインデックスが再構築されます。  
  
 インデックスが計算列にある場合、 **-RebldIdx** を使用するときに **-SupportComputedColumn**引数も指定する必要があります。  
  
 **-RebldIdx**  
 計算列に対して **sqlmaint** の DBCC メンテナンス コマンドを実行する場合は、必ず指定します。  
  
 **-WriteHistory**  
 **sqlmaint**によって実行される各メンテナンス操作に対して、msdb.dbo.sysdbmaintplan_history にエントリを作成します。 **-PlanName** または **-PlanID** が指定された場合、sysdbmaintplan_history のエントリには指定されたプランの ID が使用されます。 **-D** が指定された場合、sysdbmaintplan_history のエントリはプラン ID にゼロ値を使用して作成されます。  
  
 **-BkUpDB** [ *backup_path*] |  **-BkUpLog** [ *backup_path* ]  
 バックアップ操作を指定します。 **-BkUpDb** はデータベース全体をバックアップします。 **-BkUpLog** はトランザクション ログのみをバックアップします。  
  
 *backup_path* には、バックアップを格納するディレクトリを指定します。 *backup_path* は、 **-UseDefDir** も指定されている場合は必要ありません。ただし両方が指定されている場合は、 **-UseDefDir** によってオーバーライドされます。 バックアップは、ディレクトリまたはテープ デバイス アドレス ( \\\\.\TAPE0 など) に格納することができます。 データベース バックアップのファイル名は、次のように自動的に生成されます。  
  
```  
dbname_db_yyyyMMddhhmm.BAK  
  
```  
  
 パラメーターの説明  
  
-   *dbname* はバックアップするデータベースの名前です。  
  
-   *yyyyMMddhhmm* はバックアップ操作の日時です ( *yyyy* = 年、 *MM* = 月、 *dd* = 日、 *hh* = 時間、 *mm* = 分)。  
  
 トランザクション バックアップ用のファイル名は、次のように同じ形式を使用して自動的に生成されます。  
  
```  
dbname_log_yyyymmddhhmm.BAK  
  
```  
  
 **-BkUpDB** パラメーターを使用する場合は、 **-BkUpMedia** パラメーターを使用してメディアを指定する必要があります。  
  
 **-BkUpMedia**  
 バックアップのメディアの種類 (DISK または TAPE) を指定します。  
  
 **DISK**  
 バックアップ メディアがディスクであることを指定します。  
  
 **-DelBkUps**< *time_period* >  
 ディスク バックアップの場合で、バックアップ作成後の期間が \<*time_period*> を超える場合、バックアップ ディレクトリ内にあるすべてのバックアップ ファイルを削除します。  
  
 **-CrBkSubDir**  
 ディスク バックアップの場合で、[*backup_path*] ディレクトリ内、または **-UseDefDir** が指定されている場合は、既定のバックアップ ディレクトリ内にサブディレクトリを作成します。 サブディレクトリの名前は、 **-D**に指定されるデータベース名を基に生成されます。 **-CrBkSubDir** を使用すると、 *backup_path* パラメーターを変更せずに、異なるデータベースのすべてのバックアップを、個別のサブディレクトリに簡単に格納することができます。  
  
 **-UseDefDir**  
 ディスク バックアップの場合、既定のバックアップ ディレクトリにバックアップ ファイルを作成します。 **UseDefDir** は、*backup_path* をオーバーライドします (両方が指定されている場合)。 既定の [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] セットアップでは、既定のバックアップ ディレクトリは C:\Program Files\Microsoft SQL Server\MSSQL10_50.MSSQLSERVER\MSSQL\Backup です。  
  
 **TAPE**  
 バックアップ メディアがテープであることを指定します。  
  
 **-BkUpOnlyIfClean**  
 指定されたすべての **-Ck** チェックでデータに問題が検出されなかった場合のみ、バックアップを行います。 メンテナンス操作は、コマンド プロンプトでの指定と同じ順序で実行されます。 **-BkUpOnlyIfClean**を指定する場合、またはチェックで問題がレポートされるかどうかに関係なくバックアップが発生する場合は、 **-BkUpDB**-BkUpLog **パラメーターの前に**-CkDB **、** -CkDBNoIdx **、** -CkAl **、** -CkAlNoIdx **、** / **-CkTxtAl** 、または **-CkCat**のパラメーターを指定します。  
  
 **-VrfyBackup**  
 バックアップの完了時、バックアップに対して RESTORE VERIFYONLY を実行します。  
  
 *number*[**minutes**| **hours**| **day**| **weeks**| **months**]  
 レポートまたはバックアップ ファイルを削除する時期であるかどうかを判断するための期間を指定します。 *number* は整数値で、続けてスペースを含めずに時間単位を指定します。 次は有効な例です。  
  
-   **12weeks**  
  
-   **3months**  
  
-   **15days**  
  
 *number* だけを指定する場合、既定では、 **weeks**と見なされます。  
  
## <a name="remarks"></a>Remarks  
 **sqlmaint** ユーティリティは、1 つまたは複数のデータベースでメンテナンス操作を実行します。 **-D** を指定する場合、残りのスイッチで指定する操作は指定したデータベースでのみ実行されます。 **-PlanName** または **-PlanID** が指定された場合、指定されたメンテナンス プランから **sqlmaint** が取得する情報は、プラン内のデータベースのリストのみです。 その他の **sqlmaint** パラメーターに指定されるすべての操作は、プランから取得されたリスト内の各データベースに対して適用されます。 **sqlmaint** ユーティリティでは、プラン自体に定義されているメンテナンス操作は適用されません。  
  
 **sqlmaint** ユーティリティは、実行が成功した場合には 0 を、実行が失敗した場合には 1 を返します。 失敗は次の場合にレポートされます。  
  
-   メンテナンス作業のすべてが失敗した場合。  
  
-   **-CkDB**、 **-CkDBNoIdx**、 **-CkAl**、 **-CkAlNoIdx**、 **-CkTxtAl**、または **-CkCat** のチェックでデータの問題が検出された場合。  
  
-   一般エラーが発生した場合。  
  
## <a name="permissions"></a>アクセス許可  
 **に対して** 読み取りおよび実行 **権限のある Windows ユーザーが、** sqlmaint `sqlmaint.exe`ユーティリティを実行できます。このファイルは、既定では `x:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER1\MSSQL\Binn` フォルダーに格納されています。 さらに、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -login_ID **で指定される** ログインは、指定の操作を実行するのに必要な [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の権限を持っている必要があります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] への接続で Windows 認証を使用する場合、認証される Windows ユーザーにマップされている [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ログインが指定の操作を実行するには、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の権限が必要です。  
  
 たとえば、 **-BkUpDB** を使用するには、BACKUP ステートメントを実行するための権限が必要です。 また、 **-UpdOptiStats** 引数を使用するには、UPDATE STATISTICS ステートメントを実行するための権限が必要です。 詳細については、オンライン ブックの該当トピックで「権限」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-performing-dbcc-checks-on-a-database"></a>A. データベースで DBCC チェックを実行する  
  
```  
sqlmaint -S MyServer -D AdventureWorks2012 -CkDB -CkAl -CkCat -Rpt C:\MyReports\AdvWks_chk.rpt  
```  
  
### <a name="b-updating-statistics-using-a-15-sample-in-all-databases-in-a-plan-also-shrink-any-of-the-database-that-have-reached-110-mb-to-having-only-10-free-space"></a>B. プラン内にあるすべてのデータベースから 15% のサンプルを使用して統計を更新し、 110 MB に達したすべてのデータベースを圧縮して、10% の未使用領域を確保する  
  
```  
sqlmaint -S MyServer -PlanName MyUserDBPlan -UpdOptiStats 15 -RmUnusedSpace 110 10  
```  
  
### <a name="c-backing-up-all-the-databases-in-a-plan-to-their-individual-subdirectories-in-the-default-xprogram-filesmicrosoft-sql-servermssql13mssqlservermssqlbackup-directory-also-delete-any-backups-older-than-2-weeks"></a>C. 既定の x:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup ディレクトリ内にある個別のサブディレクトリに、プラン内のすべてのデータベースをバックアップし、 2 週間を経過したバックアップはすべて削除する  
  
```  
sqlmaint -S MyServer -PlanName MyUserDBPlan -BkUpDB -BkUpMedia DISK -UseDefDir -CrBkSubDir -DelBkUps 2weeks  
```  
  
### <a name="d-backing-up-a-database-to-the-default-xprogram-filesmicrosoft-sql-servermssql13mssqlservermssqlbackup-directory"></a>D. 既定の x:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup ディレクトリにデータベースをバックアップする  
  
```  
sqlmaint -S MyServer -BkUpDB -BkUpMedia DISK -UseDefDir  
```  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](../t-sql/statements/backup-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../t-sql/statements/update-statistics-transact-sql.md)  
  
  
