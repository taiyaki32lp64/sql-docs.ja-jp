---
title: tablediff ユーティリティ |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- comparing data
- tablediff utility
- tables [SQL Server replication]
- table comparisons [SQL Server]
- command prompt utilities [SQL Server], tablediff
- troubleshooting [SQL Server replication], non-convergence
- non-convergence [SQL Server]
ms.assetid: 3c3cb865-7a4d-4d66-98f2-5935e28929fc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 48fc2d25bc65e76156da80c6b6117a62fa39e2a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986038"
---
# <a name="tablediff-utility"></a>tablediff ユーティリティ
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  **tablediff** ユーティリティは、2 つのテーブル内のデータを比較して非収束の発生を調べる場合に使用されます。これは、レプリケーション トポロジ内の非収束に対するトラブルシューティングを行うときに特に便利です。 このユーティリティは、コマンド プロンプトから、またはバッチ ファイル内で使用して、次のタスクを実行することができます。  
  
-   レプリケーション パブリッシャーとして動作する [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンス内のソース テーブルと、レプリケーション サブスクライバーとして動作する 1 つ以上の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスにある対象テーブルの間で、1 行単位の比較を行う。  
  
-   行数とスキーマのみを比較することによる高速比較を実行します。  
  
-   列レベルでの比較の実行。  
  
-   対象サーバーでの相違点を修正し、ソース テーブルと対象テーブルを収束させる [!INCLUDE[tsql](../includes/tsql-md.md)] スクリプトの作成。  
  
-   出力ファイルへの結果の記録、または対象データベース内にあるテーブルへの結果の記録。  
  
## <a name="syntax"></a>構文  
  
```  
  
tablediff   
[ -? ] |   
{  
        -sourceserver source_server_name[\instance_name]  
        -sourcedatabase source_database  
        -sourcetable source_table_name   
    [ -sourceschema source_schema_name ]  
    [ -sourcepassword source_password ]  
    [ -sourceuser source_login ]  
    [ -sourcelocked ]  
        -destinationserver destination_server_name[\instance_name]  
        -destinationdatabase subscription_database   
        -destinationtable destination_table   
    [ -destinationschema destination_schema_name ]  
    [ -destinationpassword destination_password ]  
    [ -destinationuser destination_login ]  
    [ -destinationlocked ]  
    [ -b large_object_bytes ]   
    [ -bf number_of_statements ]   
    [ -c ]   
    [ -dt ]   
    [ -et table_name ]   
    [ -f [ file_name ] ]   
    [ -o output_file_name ]   
    [ -q ]   
    [ -rc number_of_retries ]   
    [ -ri retry_interval ]   
    [ -strict ]  
    [ -t connection_timeouts ]   
}  
```  
  
## <a name="arguments"></a>引数  
 [ **-?** ]  
 サポートされているパラメーターのリストを返します。  
  
 **-sourceserver** _source_server_name_[ **\\** _instance\_name_]  
 ソース サーバー名を指定します。 *の既定のインスタンスの場合は、* source_server_name [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を指定します。 _の名前付きインスタンスの_ **\\** _source_server_name_ instance_name [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を指定します。  
  
 **-sourcedatabase** _source_database_  
 ソース データベース名を指定します。  
  
 **-sourcetable** _source_table_name_  
 調査するソース テーブルの名前を指定します。  
  
 **-sourceschema** _source_schema_name_  
 ソース テーブルのスキーマ所有者を指定します。 既定では、テーブル所有者は dbo と見なされます。  
  
 **-sourcepassword** _source_password_  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証でソース サーバーに接続する場合に使用するログインのパスワードを指定します。  
  
> [!IMPORTANT]  
>  可能である場合は、実行時にセキュリティ資格情報を指定します。 資格情報をスクリプト ファイルに格納する必要がある場合は、不正アクセスを防ぐためにファイルを保護してください。  
  
 **-sourceuser** _source_login_  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証でソース サーバーに接続する場合に使用するログインを指定します。 *source_login* を省略すると、Windows 認証がソース サーバーへの接続時に使用されます。 [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]  
  
 **-sourcelocked**  
 比較中は、TABLOCK および HOLDLOCK テーブル ヒントを使用して、ソース テーブルがロックされます。  
  
 **-destinationserver** _destination_server_name_[ **\\** _instance_name_]  
 対象サーバー名を指定します。 *の既定のインスタンスの場合は、* destination_server_name [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を指定します。 _の名前付きインスタンスの_ **\\** _destination_server_name_ instance_name [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を指定します。  
  
 **-destinationdatabase** _subscription_database_  
 対象データベース名を指定します。  
  
 **-destinationtable** _destination_table_  
 対象テーブルの名前を指定します。  
  
 **-destinationschema** _destination_schema_name_  
 対象テーブルのスキーマ所有者を指定します。 既定では、テーブル所有者は dbo と見なされます。  
  
 **-destinationpassword** _destination_password_  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証で対象サーバーに接続する場合に使用するログインのパスワードを指定します。  
  
> [!IMPORTANT]  
>  可能である場合は、実行時にセキュリティ資格情報を指定します。 資格情報をスクリプト ファイルに格納する必要がある場合は、不正アクセスを防ぐためにファイルを保護してください。  
  
 **-destinationuser** _destination_login_  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証で対象サーバーに接続する場合に使用するログインを指定します。 *destination_login* を省略すると、Windows 認証がサーバーへの接続時に使用されます。 [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]  
  
 **-destinationlocked**  
 比較中は、TABLOCK および HOLDLOCK テーブル ヒントを使用して、対象テーブルがロックされます。  
  
 **-b** _large_object_bytes_  
 ラージ オブジェクト データ型の列に対して比較するバイト数を指定します。列の型は、 **text**、 **ntext**、 **image**、 **varchar(max)** 、 **nvarchar(max)** 、 **varbinary(max)** です。 *large_object_bytes* の既定値は、列のサイズです。 *large_object_bytes* を超えるデータは比較されません。  
  
 **-bf**  _number_of_statements_  
 [!INCLUDE[tsql](../includes/tsql-md.md)] -f [!INCLUDE[tsql](../includes/tsql-md.md)] オプションを使用する場合に、現在の **スクリプト ファイルに書き込む** ステートメントの数を指定します。 [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの数が *number_of_statements*で指定した値を超えると、新しい [!INCLUDE[tsql](../includes/tsql-md.md)] スクリプト ファイルが作成されます。  
  
 **-c**  
 列レベルでの違いを比較します。  
  
 **-dt**  
 テーブルが既に存在している場合は、 *table_name*で指定された結果テーブルを削除します。  
  
 **-et** _table_name_  
 作成する結果テーブルの名前を指定します。 このテーブルが既に存在する場合は、 **-DT** を使用する必要があります。使用しない場合、この処理は失敗します。  
  
 **-f** [ *file_name* ]  
 対象サーバーにあるテーブルを、ソース サーバーにあるテーブルと収束させる [!INCLUDE[tsql](../includes/tsql-md.md)] スクリプトを生成します。 作成される [!INCLUDE[tsql](../includes/tsql-md.md)] スクリプト ファイルの名前とパスを指定できます (省略可能)。 *file_name* を指定しない場合は、ユーティリティが実行されているディレクトリに [!INCLUDE[tsql](../includes/tsql-md.md)] スクリプト ファイルが作成されます。  
  
 **-o** _output_file_name_  
 出力ファイルの完全な名前およびフル パスを指定します。  
  
 **-q**  
 行数とスキーマのみを比較することによる高速比較を実行します。  
  
 **-rc** _number_of_retries_  
 操作が失敗した場合に、ユーティリティが再試行する回数を指定します。  
  
 **-ri**  _retry_interval_  
 再試行間隔を指定します (秒単位)。  
  
 **-strict**  
 ソース スキーマと対象スキーマを厳密に比較することを指定します。  
  
 **-t** _connection_timeouts_  
 ソース サーバーと対象サーバーへの接続に関する接続タイムアウト時間を設定します (秒単位)。  
  
## <a name="return-value"></a>戻り値  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**0**|成功|  
|**1**|重大なエラー|  
|**2**|テーブルの差分|  
  
## <a name="remarks"></a>Remarks  
 **tablediff** ユーティリティは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 以外のサーバーでは使用できません。  
  
 **sql_variant** データ型列を含むテーブルはサポートされていません。  
  
 **tablediff** ユーティリティでは、既定により、ソース列と対象列の間で次のデータ型のマッピングがサポートされます。  
  
|ソースのデータ型|対象のデータ型|  
|----------------------|---------------------------|  
|**tinyint**|**smallint**、 **int**、または **bigint**|  
|**smallint**|**int** または **bigint**|  
|**int**|**bigint**|  
|**timestamp**|**varbinary**|  
|**varchar(max)**|**text**|  
|**nvarchar(max)**|**ntext**|  
|**varbinary(max)**|**image**|  
|**text**|**varchar(max)**|  
|**ntext**|**nvarchar(max)**|  
|**image**|**varbinary(max)**|  
  
 これらのマッピングを行わず、厳密な検証を行う場合は、 **-strict** オプションを使用します。  
  
 比較のソース テーブルには、主キー列、ID 列、または ROWGUID 列が少なくとも 1 つ必要です。 **-strict** オプションを使用する場合は、対象テーブルにも主キー列、ID 列、または ROWGUID 列が必要です。  
  
 対象テーブルを収束させるため作成される [!INCLUDE[tsql](../includes/tsql-md.md)] スクリプトには、次のデータ型は含められません。  
  
-   **varchar(max)**  
  
-   **nvarchar(max)**  
  
-   **varbinary(max)**  
  
-   **timestamp**  
  
-   **xml**  
  
-   **text**  
  
-   **ntext**  
  
-   **image**  
  
## <a name="permissions"></a>アクセス許可  
 テーブルを比較するには、比較するテーブル オブジェクトに対する SELECT ALL 権限が必要です。  
  
 **-et** オプションを使用するには、db_owner 固定データベース ロールのメンバーであることが必要です。または、少なくともサブスクリプション データベースでの CREATE TABLE 権限、および対象サーバーにある対象所有者スキーマに対する ALTER 権限を持っている必要があります。  
  
 **-dt** オプションを使用するには、db_owner 固定データベース ロールのメンバーであることが必要です。または、少なくとも対象サーバーにある対象所有者スキーマに対する ALTER 権限を持っている必要があります。  
  
 **-o** または **-f** オプションを使用するには、指定されたファイル ディレクトリの場所に対する書き込み権限を持っている必要があります。  
  
## <a name="see-also"></a>参照  
 [レプリケートされたテーブルを比較して相違があるかどうかを確認する &#40;レプリケーション プログラミング&#41;](../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)  
  
  
