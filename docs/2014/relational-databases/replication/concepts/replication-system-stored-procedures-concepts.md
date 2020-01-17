---
title: レプリケーション システム ストアド プロシージャの概念 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- stored procedures [SQL Server replication], programming
- programming [SQL Server replication], system stored procedures
- programming interfaces [SQL Server replication]
- system stored procedures [SQL Server replication]
- replication [SQL Server], how-to topics
ms.assetid: 816d2bda-ed72-43ec-aa4d-7ee3dc25fd8a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9f00eb93492ca150278800c4bbdfa3565550fdef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721944"
---
# <a name="replication-system-stored-procedures-concepts"></a>Replication System Stored Procedures Concepts
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、レプリケーション トポロジでユーザーが構成可能なすべての機能に、システム ストアド プロシージャを使ってプログラムからアクセスできます。 ストアド プロシージャは、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] や sqlcmd コマンド ライン ユーティリティを使って個別に実行することもできますが、一連のレプリケーション タスクを実行する [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプト ファイルを作成することで、その利点を最大限に活かすことができます。  
  
 レプリケーション タスクをスクリプト化することの利点を次に示します。  
  
-   レプリケーション トポロジを配置するために必要な手順を 1 つにまとめて再利用できる。  
  
-   単一のスクリプトを使って複数のサブスクライバーを構成できる。  
  
-   新人のデータベース管理者がコードを見て処理の内容を理解し、変更やトラブルシューティングに備えることで、迅速に仕事を覚えることができる。  
  
    > [!IMPORTANT]  
    >  スクリプトは、セキュリティ脆弱性の原因となる可能性があります。ユーザーが知らないうちに、またはユーザーが操作しなくても、スクリプトによってシステムの機能を実行することができます。また、セキュリティ資格情報が平文で含まれている場合もあります。 スクリプトを使用する前に、セキュリティの問題がないかどうかを確認してください。  
  
## <a name="creating-replication-scripts"></a>レプリケーション スクリプトの作成  
 レプリケーションの観点から言えば、スクリプトは、それぞれがレプリケーションのストアド プロシージャを実行する、1 つまたは複数の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントの集合です。 スクリプトは、sqlcmd ユーティリティを使って実行できるテキスト ファイルで、一般に、.sql という拡張子が使用されます。 スクリプト ファイルを実行すると、そこに格納された SQL ステートメントが sqlcmd ユーティリティによって実行されます。 同様に、スクリプトをクエリ オブジェクトとして [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] プロジェクトに格納することもできます。  
  
 レプリケーション スクリプトは、以下のような方法で作成できます。  
  
-   スクリプトを手動で作成する。  
  
-   レプリケーション ウィザードのスクリプト生成機能を使用する。または  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]。 詳しくは、「 [Scripting Replication](../scripting-replication.md)」をご覧ください。  
  
-   レプリケーション管理オブジェクト (RMO) を使用し、RMO オブジェクトを作成するためのスクリプトをプログラムから生成する。  
  
 レプリケーション スクリプトを手動で作成する場合は、次の点に注意してください。  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトは 1 つ以上のバッチを含んでいます。 GO コマンドによってバッチの終了を示します。 [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトに GO ステートメントがない場合は、1 つのバッチとして実行されます。  
  
-   1 つのバッチで複数のレプリケーション ストアド プロシージャを実行する場合は、そのバッチの中で、最初のプロシージャの後に続くすべてのプロシージャの先頭に EXECUTE キーワードを指定する必要があります。  
  
-   バッチに含まれるすべてのストアド プロシージャは、バッチの実行前にコンパイルする必要があります。 ただし、バッチがコンパイルされ、実行プランが作成された後で、実行時エラーが発生する可能性もあります。  
  
-   レプリケーションの構成スクリプトを作成する場合は、セキュリティ資格情報をスクリプト ファイルに格納しなくて済むように、Windows 認証の使用をお勧めします。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
## <a name="sample-replication-script"></a>サンプル レプリケーション スクリプト  
 次のスクリプトを実行すると、サーバー上にパブリッシングとディストリビューションをセットアップできます。  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Install the Distributor and the distribution database.  
DECLARE @distributor AS sysname;  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @directory AS nvarchar(500);  
DECLARE @publicationDB AS sysname;  
-- Specify the Distributor name.  
SET @distributor = $(DistPubServer);  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
-- Specify the replication working directory.  
SET @directory = N'\\' + $(DistPubServer) + '\repldata';  
-- Specify the publication database.  
SET @publicationDB = N'AdventureWorks2012';   
  
-- Install the server MYDISTPUB as a Distributor using the defaults,  
-- including autogenerating the distributor password.  
USE master  
EXEC sp_adddistributor @distributor = @distributor;  
  
-- Create a new distribution database using the defaults, including  
-- using Windows Authentication.  
USE master  
EXEC sp_adddistributiondb @database = @distributionDB,   
    @security_mode = 1;  
GO  
  
-- Create a Publisher and enable AdventureWorks2012 for replication.  
-- Add MYDISTPUB as a publisher with MYDISTPUB as a local distributor  
-- and use Windows Authentication.  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
  
USE [distribution]  
EXEC sp_adddistpublisher @publisher=@publisher,   
    @distribution_db=@distributionDB,   
    @security_mode = 1;  
GO  
  
```  
  
 その後、このスクリプトを `instdistpub.sql` としてローカルに保存しておけば必要に応じていつでも再実行できます。  
  
 以前のスクリプトには **sqlcmd** スクリプト変数が含まれており、この変数は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックのレプリケーション コード サンプルの多くで使用されています。 スクリプト変数は `$(MyVariable)` 構文を使用して定義します。 変数の値は、コマンド ラインまたは [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] でスクリプトに渡すことができます。 詳細については、このトピックの次のセクション「レプリケーション スクリプトの実行」を参照してください。  
  
## <a name="executing-replication-scripts"></a>レプリケーション スクリプトの実行  
 作成したレプリケーション スクリプトは、次のいずれかの方法で実行できます。  
  
### <a name="creating-a-sql-query-file-in-sql-server-management-studio"></a>SQL Server Management Studio を使った SQL クエリ ファイルの作成  
 レプリケーション [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプト ファイルは、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] プロジェクトで SQL クエリ ファイルとして作成できます。 スクリプトを作成した後、このクエリ ファイルが格納されたデータベースに接続することによってスクリプトを実行できます。 作成する方法についての詳細は[!INCLUDE[tsql](../../../includes/tsql-md.md)]スクリプトを使用して[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]を参照してください[クエリおよびテキスト エディター &#40;SQL Server Management Studio&#41;](../../scripting/query-and-text-editors-sql-server-management-studio.md))。  
  
 スクリプト変数を含むスクリプトを使用するには、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] を **sqlcmd** モードで実行する必要があります。 **sqlcmd** モードでは、変数の値として使用される `:setvar` などの **sqlcmd** に固有の追加の構文を Query Editor で使用できます。 **sqlcmd** モードの詳細については、「[クエリ エディターによる SQLCMD スクリプトの編集](../../scripting/edit-sqlcmd-scripts-with-query-editor.md)」を参照してください。 次のスクリプトでは、`$(DistPubServer)` 変数の値の指定に `:setvar` を使用しています。  
  
```  
:setvar DistPubServer N'MyPublisherAndDistributor';  
  
-- Install the Distributor and the distribution database.  
DECLARE @distributor AS sysname;  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @directory AS nvarchar(500);  
DECLARE @publicationDB AS sysname;  
-- Specify the Distributor name.  
SET @distributor = $(DistPubServer);  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
  
--  
-- Additional code goes here  
--  
```  
  
### <a name="using-the-sqlcmd-utility-from-the-command-line"></a>コマンド ラインからの sqlcmd ユーティリティの使用  
 次の例に、[sqlcmd ユーティリティ](../../../tools/sqlcmd-utility.md)を使用してコマンド ラインから `instdistpub.sql` スクリプト ファイルを実行する方法を示します。  
  
```  
sqlcmd.exe -E -S sqlserverinstance -i C:\instdistpub.sql -o C:\output.log -v DistPubServer="N'MyDistributorAndPublisher'"  
```  
  
 この例の `-E` スイッチは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] との接続に Windows 認証を使用することを指定しています。 Windows 認証を使用した場合、ユーザー名やパスワードをスクリプト ファイルに格納する必要はありません。 スクリプト ファイルの名前とパスは `-i` スイッチで指定し、出力ファイルの名前は `-o` スイッチで指定します (このスイッチを使用した場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] からの出力はコンソールでなくこのファイルに書き込まれます)。 `sqlcmd` ユーティリティの `-v` スイッチを使用すると、実行時にスクリプト変数を [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトに渡すことができます。 この例では、`sqlcmd` によって、スクリプト中に出現するすべての `$(DistPubServer)` のインスタンスが、実行前に `N'MyDistributorAndPublisher'` という値に置き換えられます。  
  
> [!NOTE]  
>  `-X` スイッチを指定すると、スクリプト変数が無効化されます。  
  
### <a name="automating-tasks-in-a-batch-file"></a>バッチ ファイルを使用したタスクの自動化  
 バッチ ファイルを使用すると、レプリケーションの管理や同期などのタスクを同じバッチ ファイルにまとめることによって自動化できます。 次のバッチ ファイルでは、**sqlcmd** ユーティリティを使用して、サブスクリプション データベースの削除と再作成を行い、マージ プル サブスクリプションを追加します。 その後、マージ エージェントを呼び出して、新しいサブスクリプションを同期しています。  
  
```  
REM ----------------------Script to synchronize merge subscription ----------------------  
REM -- Creates subscription database and   
REM -- synchronizes the subscription to MergeSalesPerson.  
REM -- Current computer acts as both Publisher and Subscriber.  
REM -------------------------------------------------------------------------------------  
  
SET Publisher=%computername%  
SET Subscriber=%computername%  
SET PubDb=AdventureWorks  
SET SubDb=AdventureWorksReplica  
SET PubName=AdvWorksSalesOrdersMerge  
  
REM -- Drop and recreate the subscription database at the Subscriber  
sqlcmd /S%Subscriber% /E /Q"USE master IF EXISTS (SELECT * FROM sysdatabases WHERE name='%SubDb%' ) DROP DATABASE %SubDb%"  
sqlcmd /S%Subscriber% /E /Q"USE master CREATE DATABASE %SubDb%"  
  
REM -- Add a pull subscription at the Subscriber  
sqlcmd /S%Subscriber% /E /Q"USE %SubDb% EXEC sp_addmergepullsubscription @publisher = %Publisher%, @publication = %PubName%, @publisher_db = %PubDb%"  
sqlcmd /S%Subscriber% /E /Q"USE %SubDb%  EXEC sp_addmergepullsubscription_agent @publisher = %Publisher%, @publisher_db = %PubDb%, @publication = %PubName%, @subscriber = %Subscriber%, @subscriber_db = %SubDb%, @distributor = %Publisher%"  
  
REM -- This batch file starts the merge agent at the Subscriber to   
REM -- synchronize a pull subscription to a merge publication.  
REM -- The following must be supplied on one line.  
"\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE"  -Publisher  %Publisher% -Subscriber  %Subscriber%  -Distributor %Publisher%  -PublisherDB  %PubDb% -SubscriberDB %SubDb% -Publication %PubName% -PublisherSecurityMode 1 -OutputVerboseLevel 1  -Output  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1 -Validate 3  
  
```  
  
## <a name="scripting-common-replication-tasks"></a>一般的なレプリケーション タスクのスクリプト化  
 次に、システム ストアド プロシージャを使ってスクリプト化することのできる、最も一般的なレプリケーション タスクをいくつか紹介します。  
  
-   パブリッシングおよびディストリビューションを構成する。  
  
-   パブリッシャーとディストリビューターのプロパティを変更する。  
  
-   パブリッシングおよびディストリビューションを無効化する。  
  
-   パブリケーションを作成し、アーティクルを定義する。  
  
-   パブリケーションおよびアーティクルを削除する。  
  
-   プル サブスクリプションを作成する。  
  
-   プル サブスクリプションを変更する。  
  
-   プル サブスクリプションを削除する。  
  
-   プッシュ サブスクリプションを作成する。  
  
-   プッシュ サブスクリプションを変更する。  
  
-   プッシュ サブスクリプションを削除する。  
  
-   プル サブスクリプションを同期する。  
  
## <a name="see-also"></a>関連項目  
 [レプリケーションのプログラミング概念](replication-programming-concepts.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql)   
 [レプリケーションのスクリプト作成](../scripting-replication.md)  
  
  
