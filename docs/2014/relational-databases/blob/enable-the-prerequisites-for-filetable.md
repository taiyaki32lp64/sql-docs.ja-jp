---
title: FileTable の前提条件の有効化 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], prerequisites
ms.assetid: 6286468c-9dc9-4eda-9961-071d2a36ebd6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b4e4679a6022a37a72ce7083d3467bbbccd69f45
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010163"
---
# <a name="enable-the-prerequisites-for-filetable"></a>FileTable の前提条件の有効化
  FileTable を作成および使用するための前提条件を有効にする方法について説明します。  
  
##  <a name="EnablePrereq"></a> FileTable の前提条件の有効化  
 FileTable を作成および使用するための前提条件を有効にするには、次の項目を有効にします。  
  
-   **インスタンス レベル:**  
  
    -   [インスタンス レベルでの FILESTREAM の有効化](#BasicsFilestream)  
  
-   **データベース レベル:**  
  
    -   [データベース レベルでの FILESTREAM ファイル グループの指定](#filegroup)  
  
    -   [データベース レベルでの非トランザクション アクセスの有効化](#BasicsNTAccess)  
  
    -   [データベース レベルでの FileTable のディレクトリ指定](#BasicsDirectory)  
  
##  <a name="BasicsFilestream"></a> インスタンス レベルでの FILESTREAM の有効化  
 FileTable は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の FILESTREAM 機能を拡張します。 したがって、FileTable を作成および使用するには、ファイル I/O アクセス用の FILESTREAM を Windows レベルおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで事前に有効にする必要があります。  
  
###  <a name="HowToFilestream"></a>方法:インスタンス レベルで FILESTREAM を有効にする  
 FILESTREAM を有効にする方法の詳細については、「 [FILESTREAM の有効化と構成](enable-and-configure-filestream.md)」をご覧ください。  
  
 `sp_configure` を呼び出し、FILESTREAM をインスタンス レベルで有効にするには、filestream_access_level オプションを 2 に設定する必要があります。 詳細については、「 [filestream access level サーバー構成オプション](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md)」を参照してください。  
  
###  <a name="firewall"></a>方法:FILESTREAM がファイアウォールを通過できるようにする  
 FILESTREAM がファイアウォールを通過できるようにする方法については、「 [Configure a Firewall for FILESTREAM Access](configure-a-firewall-for-filestream-access.md)」をご覧ください。  
  
##  <a name="filegroup"></a> データベース レベルでの FILESTREAM ファイル グループの指定  
 データベースに FileTable を作成するには、データベースに FILESTREAM ファイル グループが必要です。 この前提条件の詳細については、「 [FILESTREAM が有効なデータベースを作成する方法](create-a-filestream-enabled-database.md)」を参照してください。  
  
##  <a name="BasicsNTAccess"></a> データベース レベルでの非トランザクション アクセスの有効化  
 FileTable は、Windows アプリケーションがトランザクションを必要とすることなく FILESTREAM データに対する Windows ファイル ハンドルを取得することを可能にします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に格納されているファイルに対するこの非トランザクション アクセスを可能にするには、FileTable を格納するデータベースごとに、データベース レベルで非トランザクション アクセスのレベルを指定する必要があります。  
  
###  <a name="HowToCheckAccess"></a> 方法:データベースで非トランザクション アクセスが有効かどうかを確認する  
 カタログ ビュー [sys.database_filestream_options &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql) に対してクエリを実行し、**non_transacted_access** 列と **non_transacted_access_desc** 列をチェックします。  
  
```sql  
SELECT DB_NAME(database_id), non_transacted_access, non_transacted_access_desc  
    FROM sys.database_filestream_options;  
GO  
```  
  
###  <a name="HowToNTAccess"></a>方法:データベース レベルで非トランザクション アクセスを有効にする  
 使用できる非トランザクション アクセスのレベルは、FULL、READ_ONLY、および OFF です。  
  
 **Transact-SQL を使用して非トランザクション アクセスのレベルを指定する**  
 -   **新しいデータベースを作成**するときに、**NON_TRANSACTED_ACCESS** FILESTREAM オプションを使用して [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql) ステートメントを呼び出します。  
  
    ```sql  
    CREATE DATABASE database_name  
        WITH FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' )  
    ```  
  
-   **既存のデータベースを変更**するときに、**NON_TRANSACTED_ACCESS** FILESTREAM オプションを使用して [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql) ステートメントを呼び出します。  
  
    ```sql  
    ALTER DATABASE database_name  
        SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' )  
    ```  
  
 **SQL Server Management Studio を使用して非トランザクション アクセスのレベルを指定する**  
 **[データベースのプロパティ]** ダイアログ ボックスの **[オプション]** ページの **[FILESTREAM 非トランザクション アクセス]** ボックスで、非トランザクション アクセスのレベルを指定できます。 このダイアログ ボックスの詳細については、「[[データベースのプロパティ] &#40;[オプション] ページ&#41;](../databases/database-properties-options-page.md)」を参照してください。  
  
##  <a name="BasicsDirectory"></a> データベース レベルでの FileTable のディレクトリ指定  
 ファイルに対する非トランザクション アクセスをデータベース レベルで有効にする場合、必要に応じて **DIRECTORY_NAME** オプションを使用してディレクトリ名も指定できます。 非トランザクション アクセスを有効にしたときにディレクトリ名を指定しなかった場合は、データベースに FileTable を作成する前にディレクトリ名を指定する必要があります。  
  
 FileTable フォルダー階層において、このデータベース レベルのディレクトリは、インスタンス レベルで FILESTREAM に対して指定された共有名の子になると同時に、データベースに作成された FileTable の親になります。 詳しくは、「 [Work with Directories and Paths in FileTables](work-with-directories-and-paths-in-filetables.md)」をご覧ください。  
  
###  <a name="HowToDirectory"></a>方法:データベース レベルで FileTable のディレクトリを指定する  
 指定する名前は、データベース レベルで存在するディレクトリに対して一意であることが必要です。  
  
 **Transact-SQL を使用して FileTable のディレクトリを指定する**  
 -   **新しいデータベースを作成**するときに、**DIRECTORY_NAME** FILESTREAM オプションを使用して [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql) ステートメントを呼び出します。  
  
    ```sql  
    CREATE DATABASE database_name  
        WITH FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   **既存のデータベースを変更**するときに、**DIRECTORY_NAME** FILESTREAM オプションを使用して [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql) ステートメントを呼び出します。 これらのオプションを使用してディレクトリ名を変更するとき、データベースを排他的にロックして、開いているファイル ハンドルがないことを確認する必要があります。  
  
    ```sql  
    ALTER DATABASE database_name  
        SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   **データベースをアタッチ**するときに、**FOR ATTACH** オプションおよび **DIRECTORY_NAME** FILESTREAM オプションを使用して [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql) ステートメントを呼び出します。  
  
    ```sql  
    CREATE DATABASE database_name  
        FOR ATTACH WITH FILESTREAM ( DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   **データベースを復元**するときに、**DIRECTORY_NAME** FILESTREAM オプションを使用して [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql) ステートメントを呼び出します。  
  
    ```sql  
    RESTORE DATABASE database_name  
        WITH FILESTREAM ( DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
 **SQL Server Management Studio を使用して、FileTable のディレクトリを指定する**  
 **[データベースのプロパティ]** ダイアログ ボックスの **[オプション]** ページの **[FILESTREAM ディレクトリ名]** ボックスで、ディレクトリ名を指定できます。 このダイアログ ボックスの詳細については、「[[データベースのプロパティ] &#40;[オプション] ページ&#41;](../databases/database-properties-options-page.md)」を参照してください。  
  
###  <a name="viewnames"></a>方法:インスタンスの既存のディレクトリ名を表示する  
 インスタンスの既存のディレクトリ名の一覧を表示するには、[ys.database_filestream_options &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql) カタログ ビューに対するクエリを実行し、**filestream_database_directory_name** 列を確認します。  
  
```sql  
SELECT DB_NAME ( database_id ), directory_name  
    FROM sys.database_filestream_options;  
GO  
```  
  
###  <a name="ReqDirectory"></a> データベース レベルのディレクトリの要件と制限  
  
-   **CREATE DATABASE** または **ALTER DATABASE** を呼び出すとき、 **DIRECTORY_NAME**をオプションで設定できます。 **DIRECTORY_NAME**の値を指定しなかった場合、ディレクトリ名は null のままになります。 ただし、データベース レベルで **DIRECTORY_NAME** の値を指定しないと、データベースに FileTable を作成できません。  
  
-   指定するディレクトリ名は、ファイル システムの有効なディレクトリ名に関する要件を満たしている必要があります。  
  
-   データベースに FileTable が含まれている場合、 **DIRECTORY_NAME** を再度 null 値に設定することはできません。  
  
-   データベースをアタッチまたは復元するときに、対象のインスタンスに既に存在する **DIRECTORY_NAME** の値が新しいデータベースにある場合、操作は失敗します。 **CREATE DATABASE FOR ATTACH** または **RESTORE DATABASE** を呼び出すときは、 **DIRECTORY_NAME**に対して一意の値を指定してください。  
  
-   既存のデータベースを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にアップグレードした場合、 **DIRECTORY_NAME** の値は null になります。  
  
-   非トランザクション アクセスをデータベース レベルで有効または無効にするとき、ディレクトリ名が指定されているかどうか、またはディレクトリ名が一意であるかどうかのチェックは行われません。  
  
-   FileTable に対して有効化されていたデータベースを削除すると、データベース レベルのディレクトリとそれ以下のすべての FileTable のすべてのディレクトリ構造が削除されます。  
  
  
