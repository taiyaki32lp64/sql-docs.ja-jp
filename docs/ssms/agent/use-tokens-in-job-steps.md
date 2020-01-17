---
title: ジョブ ステップでのトークンの使用 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [SQL Server Agent]
- security [SQL Server Agent], enabling alert job step tokens
- SQL Server Agent jobs, job steps
- tokens [SQL Server]
- escape macros [SQL Server Agent]
ms.assetid: 105bbb66-0ade-4b46-b8e4-f849e5fc4d43
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 13ee039c9f3a70b5468d3d7b726b1600e8f80339
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68260887"
---
# <a name="use-tokens-in-job-steps"></a>ジョブ ステップでのトークンの使用
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用すると、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ジョブ ステップ スクリプトでトークンを使用できます。 ジョブ ステップを記述するときにトークンを使用すると、ソフトウェア プログラムを記述するときの変数と同じような柔軟性が得られます。 ジョブ ステップ スクリプトにトークンを挿入した後、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブシステムでジョブ ステップが実行される前に、 [!INCLUDE[tsql](../../includes/tsql-md.md)] エージェントにより実行時にトークンが置き換えられます。  
  
  
## <a name="understanding-using-tokens"></a>トークンの使用について  
  
> [!IMPORTANT]  
> Windows イベント ログに対して書き込みのアクセス許可を持っている Windows ユーザーであればだれでも、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの警告または WMI 警告によってアクティブ化されるジョブ ステップにアクセスできます。 このセキュリティ上のリスクを避けるために、警告によってアクティブになるジョブで使用できる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント トークンは、既定で無効になっています。 このようなトークンには、**A-DBN**、**A-SVR**、**A-ERR**、**A-SEV**、**A-MSG**、**WMI(** _property_ **)** があります。 このリリースでは、トークンの使用はすべての警告に拡張されていることに注意してください。  
>   
> これらのトークンを使用する必要がある場合は、まず、Administrators グループなどの信頼されている Windows セキュリティ グループのメンバーのみが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が存在するコンピューターのイベント ログに対して書き込みのアクセス許可を持っていることを確認してください。 確認したら、[オブジェクト エクスプローラー] で **[SQL Server エージェント]** を右クリックし、 **[プロパティ]** をクリックします。次に、 **[警告システム]** ページで、 **[警告に応答するすべてのジョブのトークンを置き換える]** チェック ボックスをオンにして、これらのトークンを有効にします。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのトークンの置換は簡単で効率的です。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントにより、トークンのリテラル文字列値にそのまま置き換えられます。 すべてのトークンには大文字と小文字の区別があります。 ジョブ ステップでは、この点を考慮し、使用するトークンを正しく引用したり、置換後の文字列を正しいデータ型に変換したりする必要があります。  
  
たとえば、ジョブ ステップでデータベースの名前を表示するときに、次のステートメントを使用する場合があります。  
  
`PRINT N'Current database name is $(ESCAPE_SQUOTE(A-DBN))' ;`  
  
この例では、 **ESCAPE_SQUOTE** マクロは **A-DBN** トークンと共に挿入されます。 実行時に、 **A-DBN** トークンは適切なデータベース名に置き換えられます。 エスケープ マクロにより、トークンの置換後の文字列に誤って渡される可能性がある単一引用符がエスケープされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントにより、最後の文字列にある 1 つの単一引用符が 2 つの連続する単一引用符に置き換えられます。  
  
たとえば、トークンを置き換えるために渡される文字列が `AdventureWorks2012'SELECT @@VERSION --`の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ ステップで実行されるコマンドは次のようになります。  
  
`PRINT N'Current database name is AdventureWorks2012''SELECT @@VERSION --' ;`  
  
この場合、挿入されたステートメント `SELECT @@VERSION`は実行されません。 代わりに、追加の単一引用符によって、サーバーは挿入されたステートメントを文字列として解析します。 トークンの置換後の文字列に単一引用符が含まれていない場合は、エスケープされる文字はなく、トークンを含むジョブ ステップが意図したとおりに実行されます。  
  
ジョブ ステップでのトークンの使用をデバッグするには、 `PRINT N'$(ESCAPE_SQUOTE(SQLDIR))'` のような PRINT ステートメントを使用して、ジョブ ステップの出力をファイルまたはテーブルに保存します。 **[ジョブ ステップのプロパティ]** ダイアログ ボックスの **[詳細設定]** ページを使用して、ジョブ ステップの出力ファイルまたはテーブルを指定します。  
  
## <a name="sql-server-agent-tokens-and-macros"></a>SQL Server エージェントのトークンとマクロ  
次の表では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントでサポートされているトークンとマクロについて説明します。  
  
### <a name="sql-server-agent-tokens"></a>SQL Server エージェントのトークン  
  
|トークン|[説明]|  
|---------|---------------|  
|**(A-DBN)**|データベース名。 ジョブが警告によって実行される場合、ジョブ ステップのこのトークンは自動的にデータベース名の値に置き換えられます。|  
|**(A-SVR)**|サーバー名。 ジョブが警告によって実行される場合、ジョブ ステップのこのトークンは自動的にサーバー名の値に置き換えられます。|  
|**(A-ERR)**|エラー番号。 ジョブが警告によって実行される場合、ジョブ ステップのこのトークンは自動的にエラー番号の値に置き換えられます。|  
|**(A-SEV)**|エラーの重大度。 ジョブが警告によって実行される場合、ジョブ ステップのこのトークンは自動的にエラー重大度の値に置き換えられます。|  
|**(A-MSG)**|メッセージ テキスト。 ジョブが警告によって実行される場合、ジョブ ステップのこのトークンは自動的にメッセージ テキストの値に置き換えられます。|  
|**(JOBNAME)**|ジョブの名前を指定します。 このトークンは、SQL Server 2016 以降でのみ利用できます。|  
|**(STEPNAME)**|ステップの名前。 このトークンは、SQL Server 2016 以降でのみ利用できます。|  
|**(DATE)**|YYYYMMDD 形式で表す現在の日付。|  
|**(INST)**|インスタンス名。 既定のインスタンスの場合、このトークンは既定のインスタンス名、MSSQLSERVER になります。|  
|**(JOBID)**|ジョブ ID。|  
|**(MACH)**|コンピューター名。|  
|**(MSSA)**|マスター SQLServerAgent サービス名。|  
|**(OSCMD)**|**CmdExec** ジョブ ステップの実行に使用されるプログラムのプレフィックス。|  
|**(SQLDIR)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされているディレクトリ。 特に指定しない限り、この値は C:\Program Files\Microsoft SQL Server\MSSQL です。|  
|**(SQLLOGDIR)**|SQL Server のエラー ログ フォルダー パスを表す置換トークン。たとえば、$ (ESCAPE_SQUOTE (SQLLOGDIR))。 このトークンは、SQL Server 2014 以降でのみ利用できます。|  
|**(STEPCT)**|対象となるステップが実行された回数。ただし、再試行は除きます。 ステップ コマンドでこの値を使用して、マルチステップ ループを強制終了させることができます。|  
|**(STEPID)**|ステップ ID。|  
|**(SRVR)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を実行しているコンピューターの名前。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが名前付きインスタンスである場合は、これにインスタンス名が含まれます。|  
|**(TIME)**|HHMMSS 形式で表す現在の時刻。|  
|**(STRTTM)**|HHMMSS 形式で表すジョブの実行開始時刻。|  
|**(STRTDT)**|YYYYMMDD 形式で表すジョブの実行開始日。|  
|**(WMI (** _プロパティ_ **))**|WMI 警告に応答して実行されるジョブの場合、 *プロパティ*で指定したプロパティの値。 たとえば、 `$(WMI(DatabaseName))` では、警告が実行される原因となった WMI イベントの **DatabaseName** プロパティの値が得られます。|  
  
### <a name="sql-server-agent-escape-macros"></a>SQL Server エージェントのエスケープ マクロ  
  
|エスケープ マクロ|[説明]|  
|-----------------|---------------|  
|**$(ESCAPE_SQUOTE(** _token\_name_ **))**|トークンの置換後の文字列にある単一引用符 (') をエスケープします。 1 つの単一引用符を 2 つの連続する単一引用符に置き換えます。|  
|**$(ESCAPE_DQUOTE(** _token\_name_ **))**|トークンの置換後の文字列にある二重引用符 (") をエスケープします。 1 つの二重引用符を 2 つの連続する二重引用符に置き換えます。|  
|**$(ESCAPE_RBRACKET(** _token\_name_ **))**|トークンの置換後の文字列にある右角かっこ (]) をエスケープします。 1 つの右角かっこを 2 つの連続する右角かっこに置き換えます。|  
|**$(ESCAPE_NONE(** _token\_name_ **))**|文字列内の文字をエスケープせずにトークンを置き換えます。 このマクロは、トークンの置換後の文字列を信頼されたユーザーのみが必要としている環境で、旧バージョンとの互換性をサポートするために用意されています。 詳細については、このトピックの「マクロを使用するジョブ ステップの更新」を参照してください。|  
  
## <a name="updating-job-steps-to-use-macros"></a>マクロを使用するジョブ ステップの更新  
次の表では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントでトークンの置換がどのように処理されるのかを説明します。 警告トークンの置換の有効と無効を切り替えるには、オブジェクト エクスプローラーで **[SQL Server エージェント]** を右クリックし、 **[プロパティ]** を選択します。次に、 **[警告システム]** ページの **[警告に応答するすべてのジョブのトークンを置き換える]** チェック ボックスをオンまたはオフにします。  
  
|トークンの構文|警告トークンの置換が有効な場合|警告トークンの置換が無効な場合|  
|----------------|------------------------------|-------------------------------|  
|ESCAPE マクロを使用する|ジョブ内のすべてのトークンが正常に置き換えられます。|警告によってアクティブ化されるトークンは置き換えられません。 このようなトークンには、 **A-DBN**、 **A-SVR**、 **A-ERR**、 **A-SEV**、 **A-MSG**、および **WMI(** _プロパティ_ **)** があります。 他の静的なトークンは正常に置き換えられます。|  
|ESCAPE マクロを使用しない|トークンを含んでいるすべてのジョブが失敗します。|トークンを含んでいるすべてのジョブが失敗します。|  
  
## <a name="token-syntax-update-examples"></a>トークンの構文の更新例  
  
### <a name="a-using-tokens-in-non-nested-strings"></a>A. 入れ子になっていない文字列でトークンを使用する  
次の例では、適切なエスケープ マクロを使用して入れ子になっていない単純なスクリプトを更新する方法を示します。 更新スクリプトを実行する前に、次のジョブ ステップ スクリプトで、ジョブ ステップ トークンを使用して適切なデータベース名を表示します。  
  
`PRINT N'Current database name is $(A-DBN)' ;`  
  
更新スクリプトを実行すると、 `ESCAPE_NONE` マクロが `A-DBN` トークンの前に挿入されます。 表示する文字列を区切るために単一引用符が使用されているため、次のように、 `ESCAPE_SQUOTE` マクロを挿入してジョブ ステップを更新する必要があります。  
  
`PRINT N'Current database name is $(ESCAPE_SQUOTE(A-DBN))' ;`  
  
### <a name="b-using-tokens-in-nested-strings"></a>B. 入れ子になっている文字列でトークンを使用する  
トークンが入れ子になっている文字列やステートメントで使用されているジョブ ステップ スクリプトでは、入れ子になっているステートメントを複数のステートメントに書き直してから、適切なエスケープ マクロを挿入する必要があります。  
  
たとえば、次のジョブ ステップを考えてみましょう。 `A-MSG` トークンを使用するこのジョブ ステップは、エスケープ マクロで更新されていません。  
  
`PRINT N'Print ''$(A-MSG)''' ;`  
  
更新スクリプトを実行すると、 `ESCAPE_NONE` マクロがトークンと共に挿入されます。 ただし、この場合、次のように入れ子を使用しないスクリプトに書き直して `ESCAPE_SQUOTE` マクロを挿入し、トークンの置換後の文字列に渡される可能性がある区切り文字を正しくエスケープすることが必要な場合があります。  
  
<pre>DECLARE @msgString nvarchar(max)  
SET @msgString = '$(ESCAPE_SQUOTE(A-MSG))'  
SET @msgString = QUOTENAME(@msgString,'''')  
PRINT N'Print ' + @msgString ;</pre>  
  
また、この例では、QUOTENAME 関数によって引用符が設定されることにも注意してください。  
  
### <a name="c-using-tokens-with-the-escapenone-macro"></a>C. ESCAPE_NONE マクロと共にトークンを使用する  
次の例は、あるスクリプトの一部です。ここでは、 `job_id` テーブルから `sysjobs` を取得し、スクリプト内で既にバイナリ データ型として宣言された `JOBID` 変数を設定するために `@JobID` トークンを使用しています。 バイナリ データ型には区切り文字が不要なので、 `ESCAPE_NONE` マクロは `JOBID` トークンと共に使用されることに注意してください。 更新スクリプトの実行後、このジョブ ステップを更新する必要はありません。  
  
<pre>SELECT * FROM msdb.dbo.sysjobs  
WHERE @JobID = CONVERT(uniqueidentifier, $(ESCAPE_NONE(JOBID))) ;</pre>  
  
## <a name="see-also"></a>参照  
[ジョブの実装](../../ssms/agent/implement-jobs.md)  
[ジョブ ステップの管理](../../ssms/agent/manage-job-steps.md)  
  
