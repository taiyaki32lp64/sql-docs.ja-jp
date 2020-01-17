---
title: SQL Server Express のユーザー インスタンス
description: SQL Server Express ユーザーインスタンスのサポートについて説明します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 00c12376-cb26-4317-86ad-e6e9c089be57
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 3b3ac1e395cc1240693ca0dc27324766964e0cfa
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452015"
---
# <a name="sql-server-express-user-instances"></a>SQL Server Express のユーザー インスタンス

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Microsoft SQL Server Express Edition (SQL Server Express) は、ユーザーインスタンス機能をサポートしています。これは、Microsoft SqlClient Data Provider for SQL Server を使用している場合にのみ使用できます。 ユーザーインスタンスは、親インスタンスによって生成される SQL Server Express データベースエンジンの個別のインスタンスです。 ユーザーインスタンスを使用すると、ローカルコンピューター上の管理者以外のユーザーが、SQL Server Express データベースにアタッチして接続することができます。 各インスタンスは、個々のユーザーのセキュリティコンテキストで実行されます。ユーザーごとに1つのインスタンスがあります。  
  
## <a name="user-instance-capabilities"></a>ユーザーインスタンスの機能  
ユーザーインスタンスは、最小限の特権を持つユーザーアカウント (LUA) で Windows を実行しているユーザーにとって役立ちます。これは、各ユーザーが、Windows として実行しなくても、コンピューター上で実行されているインスタンスに対してシステム管理者 (`sysadmin`) の特権を SQL Server しているためです。管理者も同様です。 SQL Server Express のインスタンスは、サービスとしてではなく、ユーザーの管理者以外の Windows アカウントで実行されているため、アクセス許可が制限されたユーザーインスタンスで実行されているソフトウェアでは、システム全体の変更を行うことができません。 各ユーザー インスタンスは、その親コンピューターや同じコンピューター上で実行されている他のユーザー インスタンスからは分離されます。 ユーザーインスタンスで実行されているデータベースはシングルユーザーモードでのみ開かれるので、複数のユーザーがユーザーインスタンスで実行されているデータベースに接続することはできません。 ユーザーインスタンスでは、レプリケーションクエリと分散クエリも無効になっています。  
  
詳細については、SQL Server オンライン ブックの「ユーザー インスタンス」を参照してください。  
  
> [!NOTE]
>  ユーザーインスタンスは、自分のコンピューターで既に管理者になっているユーザーや、複数のデータベースユーザーが関係するシナリオには必要ありません。  
  
## <a name="enabling-user-instances"></a>ユーザーインスタンスの有効化  
ユーザーインスタンスを生成するには、SQL Server Express の親インスタンスが実行されている必要があります。 SQL Server Express がインストールされている場合は、ユーザー インスタンスが既定で有効になります。また、システム管理者は、親インスタンスに対して **sp_configure** システム ストアド プロシージャを実行することで、ユーザー インスタンスの有効と無効を明示的に切り替えることもできます。  
  
```sql
-- Enable user instances.  
sp_configure 'user instances enabled','1'   
  
-- Disable user instances.  
sp_configure 'user instances enabled','0'  
```  
  
ユーザーインスタンスのネットワークプロトコルは、ローカルの名前付きパイプである必要があります。 SQL Server のリモートインスタンスでユーザーインスタンスを起動することはできません。また、SQL Server ログインは許可されません。  
  
## <a name="connecting-to-a-user-instance"></a>ユーザー インスタンスへの接続  
`User Instance` および `AttachDBFilename`<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> キーワードによって、<xref:Microsoft.Data.SqlClient.SqlConnection> でユーザー インスタンスに接続できます。 ユーザーインスタンスは、<xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> `UserInstance` および `AttachDBFilename` プロパティによってもサポートされています。  
  
次に示す接続文字列の例について、次の点に注意してください。  
  
- `Data Source` キーワードは、ユーザーインスタンスを生成している SQL Server Express の親インスタンスを参照します。 既定のインスタンスは .\sqlexpress です。  
  
- `Integrated Security` は `true` に設定されます。 ユーザーインスタンスに接続するには、Windows 認証が必要です。SQL Server ログインはサポートされていません。  
  
- `User Instance` は `true` に設定されています。これにより、ユーザーインスタンスが呼び出されます。 (既定値は `false` です。)  
  
- `AttachDbFileName` 接続文字列キーワードは、プライマリデータベースファイル (.mdf) をアタッチするために使用されます。このファイルには、完全なパス名を含める必要があります。 `AttachDbFileName` は、<xref:Microsoft.Data.SqlClient.SqlConnection> 接続文字列内の "拡張プロパティ" キーと "初期ファイル名" キーにも対応しています。  
  
- パイプ記号で囲まれた `|DataDirectory|` 置換文字列は、接続を開いているアプリケーションのデータディレクトリを参照し、.mdf および .ldf データベースとログファイルの場所を示す相対パスを提供します。 これらのファイルを別の場所に配置する場合は、ファイルへの完全パスを指定する必要があります。  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;AttachDBFilename=|DataDirectory|\InstanceDB.mdf;  
Initial Catalog=InstanceDB;  
```  
  
> [!NOTE]
>  また、<xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.UserInstance%2A> と <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.AttachDBFilename%2A> プロパティを使用して、実行時に接続文字列を作成することもできます。  
  
### <a name="using-the-124datadirectory124-substitution-string"></a>DataDirectory&#124;代替&#124;文字列の使用  
`DataDirectory` に `AttachDbFileName` を組み合わせて使用することで、データ ファイルへの相対パスを指定でき、完全パスを使用する代わりに、データ ソースの相対パスに基づいて接続文字列を作成できます。  
  
`DataDirectory` ポイントする物理的な場所は、アプリケーションの種類によって異なります。 この例では、添付する Northwind .mdf ファイルは、アプリケーションの \app_data フォルダーにあります。  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;  
AttachDBFilename=|DataDirectory|\app_data\Northwind.mdf;  
Initial Catalog=Northwind;  
```  
  
`DataDirectory` を使用する場合、結果として得られるファイルパスは、置換文字列によって指定されているディレクトリよりもディレクトリ構造の上位に配置することはできません。 たとえば、完全に展開された `DataDirectory` が C:\AppDirectory\app_data の場合、上記のサンプルの接続文字列は C:\ appdirectoryの下にあります。 しかしながら、`DataDirectory` を `|DataDirectory|\..\data` として指定すると、\data が \AppDirectory のサブディレクトリではないため、エラーが発生します。  
  
接続文字列に不適切な形式の置換文字列が含まれている場合は、<xref:System.ArgumentException> がスローされます。  
  
> [!NOTE]
>  <xref:Microsoft.Data.SqlClient> は、置換文字列をローカルコンピューターのファイルシステムに対する完全パスに解決します。 そのため、リモートサーバー、HTTP、および UNC のパス名はサポートされていません。 サーバーがローカルコンピューターに配置されていない場合、接続が開かれると、例外がスローされます。  
  
<xref:Microsoft.Data.SqlClient.SqlConnection> が開かれると、既定の SQL Server Express インスタンスから、呼び出し元のアカウントで実行されている実行時に開始されるインスタンスにリダイレクトされます。  
  
> [!NOTE]
>  ユーザーインスタンスの読み込みに通常のインスタンスよりも長い時間がかかるため、<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionTimeout%2A> の値を大きくすることが必要になる場合があります。  
  
次のコードフラグメントでは、新しい `SqlConnection` を開き、コンソールウィンドウに接続文字列を表示して、`using` コードブロックを終了すると接続を閉じます。  
  
```csharp  
private static void OpenSqlConnection()  
{  
    // Retrieve the connection string.  
    string connectionString = GetConnectionString();  
  
    using (SqlConnection connection =   
        new SqlConnection(connectionString))  
    {  
        connection.Open();  
        Console.WriteLine("ConnectionString: {0}",   
             connection.ConnectionString);  
    }  
}  
```  
  
> [!NOTE]
>  ユーザーインスタンスは、SQL Server 内で実行されている共通言語ランタイム (CLR) コードではサポートされていません。 接続文字列に `User Instance=true` を持つ <xref:Microsoft.Data.SqlClient.SqlConnection> で `Open` が呼び出されると、<xref:System.InvalidOperationException> がスローされます。  
  
## <a name="lifetime-of-a-user-instance-connection"></a>ユーザーインスタンス接続の有効期間  
サービスとして実行される SQL Server のバージョンとは異なり、SQL Server Express インスタンスを手動で開始および停止する必要はありません。 ユーザーがログインし、ユーザーインスタンスに接続するたびに、まだ実行されていないユーザーインスタンスが起動されます。 ユーザーインスタンスデータベースには、非アクティブな状態が一定期間続くとデータベースが自動的にシャットダウンされるように `AutoClose` オプションが設定されています。 開始された sqlservr.exe プロセスは、インスタンスへの最後の接続が終了した後、限られたタイムアウト期間、実行されたままになります。そのため、タイムアウトの期限が切れる前に別の接続を開いた場合は、再起動する必要はありません。 タイムアウト期間が経過する前に新しい接続が開いていない場合、ユーザーインスタンスは自動的にシャットダウンします。 親インスタンスのシステム管理者は、**sp_configure** を使用し、**user instance timeout** オプションを変更することにより、ユーザー インスタンスのタイムアウト期間を設定できます。 既定値は 60 分です。  
  
> [!NOTE]
>  接続文字列で0より大きい値を使用して `Min Pool Size` が使用されている場合、接続プーラーは、開いているいくつかの接続を常に維持し、ユーザーインスタンスは自動的にはシャットダウンされません。  
  
## <a name="how-user-instances-work"></a>ユーザーインスタンスの動作  
各ユーザーに対して最初にユーザー インスタンスが生成された時点で、そのユーザー インスタンスによって排他的に使用されるユーザーのローカル アプリケーション データ リポジトリ ディレクトリの下位パスに、Template Data フォルダーからシステム データベース **master** および **msdb** がコピーされます。 通常、このパスは `C:\Documents and Settings\<UserName>\Local Settings\Application Data\Microsoft\Microsoft SQL Server Data\SQLEXPRESS` です。 ユーザー インスタンスが開始されると、**tempdb**、ログ、トレース ファイルもこのディレクトリに書き込まれます。 インスタンスの名前が生成されます。これは、ユーザーごとに一意であることが保証されます。  
  
既定では、Windows Builtin\Users グループのすべてのメンバーには、ローカルインスタンスで接続するためのアクセス許可と、SQL Server バイナリに対する読み取りおよび実行のアクセス許可が付与されます。 ユーザーインスタンスをホストしている呼び出し元のユーザーの資格情報が検証されると、そのユーザーはそのインスタンスの `sysadmin` になります。 ユーザーインスタンスに対しては共有メモリのみが有効になっています。つまり、ローカルコンピューター上の操作のみが可能であることを意味します。  
  
ユーザーには、接続文字列で指定された .mdf ファイルと .ldf ファイルに対する読み取りと書き込みの両方の権限が付与されている必要があります。  
  
> [!NOTE]
>  .Mdf ファイルと .ldf ファイルは、それぞれデータベースとログファイルを表します。 これら2つのファイルは一致したセットであるため、バックアップ操作と復元操作の間に注意する必要があります。 データベースファイルには、ログファイルの正確なバージョンに関する情報が含まれており、間違ったログファイルと結合されている場合、データベースは開かれません。  
  
データの破損を防ぐために、ユーザーインスタンス内のデータベースは排他アクセスで開かれます。 2つの異なるユーザーインスタンスが同じコンピューター上の同じデータベースを共有している場合、最初のインスタンスのユーザーは、2番目のインスタンスで開く前に、データベースを閉じる必要があります。  
  
## <a name="user-instance-scenarios"></a>ユーザーインスタンスのシナリオ  
ユーザーインスタンスを使用すると、開発用コンピューターに管理者アカウントを持つ開発者に依存しない SQL Server データストアを持つデータベースアプリケーションを開発者に提供できます。 ユーザーインスタンスは Access/Jet モデルに基づいています。このモデルでは、データベースアプリケーションは単純にファイルに接続し、ユーザーは、システム管理者に許可を与えることなく、すべてのデータベースオブジェクトに対する完全なアクセス許可を自動的に付与します。許可. これは、ユーザーが最小特権のユーザーアカウント (LUA) で実行されていて、サーバーまたはローカルコンピューターに対する管理者特権を持っていない場合に、データベースオブジェクトとアプリケーションを作成する必要がある状況で動作することを目的としています。 ユーザーインスタンスを使用すると、より特権の高いシステムサービスのセキュリティコンテキストではなく、ユーザー独自のセキュリティコンテキストで実行されるインスタンスを実行時に作成できます。  
  
> [!IMPORTANT]
>  ユーザーインスタンスは、それを使用するすべてのアプリケーションが完全に信頼されているシナリオでのみ使用してください。  
  
ユーザーインスタンスのシナリオは次のとおりです。  
  
- データを共有する必要がないシングルユーザーアプリケーション。  
  
- ClickOnce 配置。 NET Framework 2.0 (以降) または .NET Core 1.0 (以降) および SQL Server Express が既にターゲット コンピューターにインストールされている場合、管理者以外のユーザーでも、ClickOnce アクションの結果としてダウンロードされたインストール パッケージをインストールして使用できます。 セットアップの一部である場合は、管理者が SQL Server Express をインストールする必要があることに注意してください。 詳細については、「 [ClickOnce Deployment for Windows フォーム](https://docs.microsoft.com/dotnet/framework/winforms/clickonce-deployment-for-windows-forms)」を参照してください。
  
- Windows 認証を使用した専用の ASP.NET ホスティング。 1つの SQL Server Express インスタンスは、イントラネット上でホストできます。 アプリケーションは、偽装を使用するのではなく、ASPNET Windows アカウントを使用して接続します。 すべてのアプリケーションが同じユーザーインスタンスを共有し、互いに分離されていない場合は、サードパーティまたは共有ホスティングのシナリオでは、ユーザーインスタンスを使用しないでください。  
  
## <a name="next-steps"></a>次の手順
- [SQL Server と ADO.NET](index.md)
