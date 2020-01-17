---
title: sp_adddistributiondb (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 04/30/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddistributiondb_TSQL
- sp_adddistributiondb
helpviewer_keywords:
- sp_adddistributiondb
ms.assetid: e9bad56c-d2b3-44ba-a4d7-ff2fd842e32d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ef595adcf3772dcac92c58764d99bca4374aeb0a
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771354"
---
# <a name="sp_adddistributiondb-transact-sql"></a>sp_adddistributiondb (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  新しいディストリビューション データベースを作成し、ディストリビューター スキーマをインストールします。 ディストリビューションデータベースには、レプリケーションで使用されるプロシージャ、スキーマ、およびメタデータが格納されます。 このストアドプロシージャは、ディストリビューションデータベースを作成するために、ディストリビューター側で master データベースに対して実行されます。また、レプリケーションディストリビューションを有効にするために必要なテーブルとストアドプロシージャをインストールします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_adddistributiondb [ @database= ] 'database'   
    [ , [ @data_folder= ] 'data_folder' ]   
    [ , [ @data_file= ] 'data_file' ]   
    [ , [ @data_file_size= ] data_file_size ]   
    [ , [ @log_folder= ] 'log_folder' ]   
    [ , [ @log_file= ] 'log_file' ]   
    [ , [ @log_file_size= ] log_file_size ]   
    [ , [ @min_distretention= ] min_distretention ]   
    [ , [ @max_distretention= ] max_distretention ]   
    [ , [ @history_retention= ] history_retention ]   
    [ , [ @security_mode= ] security_mode ]   
    [ , [ @login= ] 'login' ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @createmode= ] createmode ]  
    [ , [ @from_scripting = ] from_scripting ] 
    [ , [ @deletebatchsize_xact = ] deletebatchsize_xact ] 
    [ , [ @deletebatchsize_cmd = ] deletebatchsize_cmd ] 
```  
  
## <a name="arguments"></a>引数  
`[ @database = ] database'`作成するディストリビューションデータベースの名前を指定します。 *データベースのデータ*型は**sysname**で、既定値はありません。 指定したデータベースが既に存在し、既にディストリビューションデータベースとしてマークされていない場合は、ディストリビューションを有効にするために必要なオブジェクトがインストールされ、データベースがディストリビューションデータベースとしてマークされます。 指定したデータベースが、既にディストリビューション データベースとして有効な場合は、エラーが返されます。  
  
`[ @data_folder = ] 'data_folder'_`ディストリビューションデータベースのデータファイルを格納するために使用するディレクトリの名前を指定します。 *data_folder*は**nvarchar (255)** ,、既定値は NULL です。 NULL の場合、その [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのデータ ディレクトリ、たとえば `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data` が使用されます。  
  
`[ @data_file = ] 'data_file'`データベースファイルの名前を指定します。 *data_file*は**nvarchar (255)** ,、既定値は**database**です。 NULL の場合、ストアドプロシージャはデータベース名を使用してファイル名を構築します。  
  
`[ @data_file_size = ] data_file_size`初期データファイルのサイズをメガバイト (MB) 単位で示します。 *data_file_size i*s **int**,、既定値は 5 mb です。  
  
`[ @log_folder = ] 'log_folder'`データベースログファイルのディレクトリの名前を指定します。 *log_folder*は**nvarchar (255)** ,、既定値は NULL です。 NULL の場合、の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスのデータディレクトリが使用されます (たとえば、 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data`)。  
  
`[ @log_file = ] 'log_file'`ログファイルの名前を指定します。 *log_file*は**nvarchar (255)** ,、既定値は NULL です。 NULL の場合、ストアドプロシージャはデータベース名を使用してファイル名を構築します。  
  
`[ @log_file_size = ] log_file_size`ログファイルの初期サイズをメガバイト (MB) 単位で示します。 *log_file_size*は**int**,、既定値は 0 MB,、で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]許容される最小のログファイルサイズを使用してファイルサイズが作成されることを意味します。  
  
`[ @min_distretention = ] min_distretention`トランザクションがディストリビューションデータベースから削除されるまでの最小保有期間を時間単位で示します。 *min_distretention*は**int**,、既定値は0時間です。  
  
`[ @max_distretention = ] max_distretention`トランザクションを削除するまでの最大保有期間を時間単位で示します。 *max_distretention*は**int**,、既定値は72時間です。 ディストリビューションの最長保持時間より古い、レプリケートされたコマンドを受け取っていないサブスクリプションには、非アクティブのマークが付きます。このようなサブスクリプションは再初期化する必要があります。 アクティブでないサブスクリプションに対しては RAISERROR 21011 が発行されます。 値**0**は、レプリケートされたトランザクションがディストリビューションデータベースに格納されないことを意味します。  
  
`[ @history_retention = ] history_retention`履歴を保持する時間数を指定します。 *history_retention*は**int**,、既定値は48時間です。  
  
`[ @security_mode = ] security_mode`ディストリビューターに接続するときに使用するセキュリティモードを示します。 *security_mode*は**int**,、既定値は1です。 **0**は[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証を指定します。**1** Windows 統合認証を指定します。  
  
`[ @login = ] 'login'`ディストリビューションデータベースを作成するためにディストリビューターに接続するときに使用されるログイン名を指定します。 *Security_mode*が**0**に設定されている場合は、これが必要です。 *login* のデータ型は **sysname** で、既定値は NULL です。  
  
`[ @password = ] 'password'`ディストリビューターに接続するときに使用するパスワードを入力します。 *Security_mode*が**0**に設定されている場合は、これが必要です。 *パスワード*は**sysname**,、既定値は NULL です。  
  
`[ @createmode = ] createmode`*createmode*は**int**,、既定値は 1,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**1** (既定値)|データベースを作成するか、既存のデータベースを使用してから、 **instdist .sql**ファイルを適用して、ディストリビューションデータベースにレプリケーションオブジェクトを作成します。|  
|**2**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
 
`[ @deletebatchsize_xact = ] deletebatchsize_xact`MSRepl_Transactions テーブルから有効期限が切れたトランザクションのクリーンアップ中に使用されるバッチサイズを指定します。 *deletebatchsize_xact*は**int**,、既定値は5000です。 このパラメーターは、SQL Server 2017 で初めて導入され、SQL Server 2012 SP4 および SQL Server 2016 SP2 のリリースが導入されました。  

`[ @deletebatchsize_cmd = ] deletebatchsize_cmd`MSRepl_Commands テーブルから有効期限が切れたコマンドのクリーンアップ中に使用されるバッチサイズを指定します。 *deletebatchsize_cmd*は**int**,、既定値は2000です。 このパラメーターは、SQL Server 2017 で初めて導入され、SQL Server 2012 SP4 および SQL Server 2016 SP2 のリリースが導入されました。 
 
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_adddistributiondb**は、すべての種類のレプリケーションで使用されます。 ただし、このストアド プロシージャは、ディストリビューター側でのみ動作します。  
  
 **Sp_adddistributiondb**を実行する前に[sp_adddistributor](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)を実行してディストリビューターを構成する必要があります。  
  
 **Sp_adddistributiondb**を実行する前に**sp_adddistributor**を実行します。  
  
## <a name="example"></a>例  
  
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
  
## <a name="permissions"></a>アクセス許可  
 **Sp_adddistributiondb**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [パブリッシングとディストリビューションの構成](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [ディストリビューションの構成](../../relational-databases/replication/configure-distribution.md)  
  
  
