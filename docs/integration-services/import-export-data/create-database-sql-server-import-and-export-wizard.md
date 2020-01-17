---
title: '[データベースの作成] (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs'
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4900f90f4044b32aea673106ad0a7a2a14a8f5cb
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296286"
---
# <a name="create-database-sql-server-import-and-export-wizard"></a>[データベースの作成] (SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


**[変換先の選択]** ページで **[新規]** を選択して新しい SQL Server 変換先データベースを作成する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードに **[データベースの作成]** ダイアログ ボックスが表示されます。 このページでは、新しいデータベースの名前を指定します。 必要に応じて、新しいデータベースとそのログ ファイルの初期サイズと自動拡張の設定を変更することもできます。 

ウィザードの **[データベースの作成]** ダイアログ ボックスでは、新しい SQL Server データベースを作成するために使用できる基本的なオプションのみが提供されます。 新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのすべてのオプションを表示および構成するには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してデータベースを作成するか、ウィザードでデータベースを作成してから構成します。 

> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードの **[データベースの作成]** ダイアログ ボックスではなく、[!INCLUDE[tsql](../../includes/tsql-md.md)] の CREATE DATABASE ステートメントに関する情報をお探しの場合は、「[CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)」をご覧ください。  

## <a name="screen-shot-of-the-create-database-page"></a>[データベースの作成] ページのスクリーン ショット  
以下のスクリーンショットでは、ウィザードの **[データベースの作成]** ダイアログ ボックスを示します。  

![インポートおよびエクスポート ウィザードの [データベースの作成] ページ](../../integration-services/import-export-data/media/create-database.png "インポートおよびエクスポート ウィザードの [データベースの作成] ページ")  

## <a name="provide-a-name-for-the-new-database"></a>新しいデータベースの名前を入力する  
**[名前]**  
 対象になる SQL Server データベースの名前を指定します。
 
### <a name="naming-requirements"></a>名前付けに関する要件
データベースの名前を指定するときは、SQL Server の命名規則に従ってください。  
  
-   データベース名は、SQL Server のインスタンス内で一意でなければなりません。  
  
-   データベース名は 123 文字以下です (これは、SQL Server がデータ ファイルとログ ファイルに 5 文字のサフィックスを追加しても最大 128 文字に収まるようにするためです)。  
  
-   データベース名は、SQL Server での識別子の規則に従う必要があります。 最も重要な要件を次に示します。  
  
    -   1 文字目は、アルファベット、アンダースコア (_)、アット マーク (@)、またはシャープ記号 (#) にする必要があります。  
  
    -   2 文字目以降には、アルファベット、数字、アット マーク、ドル記号 ($)、シャープ記号、アンダースコアを使用できます。  
  
    -   スペースや他の特殊文字を使用することはできません。  
  
これらの要件の詳細については、「 [データベース識別子](../../relational-databases/databases/database-identifiers.md)」をご覧ください。  

## <a name="optionally-specify-data-file-and-log-file-options"></a>必要に応じて、データ ファイルとログ ファイルのオプションを指定します。

> [!TIP]
> **[名前]** フィールドでは新しいデータベースの名前を指定する必要がありますが、通常は、ファイルのサイズとファイルの拡張に関する他の設定は既定値のままにしてかまいません。

### <a name="data-file-options"></a>データ ファイルのオプション  
 **初期サイズ**  
 データ ファイルの初期サイズを MB 単位で指定します。  
  
 **拡張を許可しない**  
 指定した初期サイズを超えるデータ ファイルの拡張を許可するかどうかを示します。  
  
 **比率で拡張する**  
 データ ファイルの拡張を許可する比率を指定します。  
  
 **サイズで拡張する**  
 データ ファイルの拡張を許可するサイズを MB 単位で指定します。  
  
### <a name="log-file-options"></a>ログ ファイルのオプション  
 **初期サイズ**  
 ログ ファイルの初期サイズを MB 単位で指定します。  
  
 **拡張を許可しない**  
 指定した初期サイズを超えるログ ファイルの拡張を許可するかどうかを示します。  
  
 **比率で拡張する**  
 ログ ファイルの拡張を許可する比率を指定します。  
  
 **サイズで拡張する**  
 ログ ファイルの拡張を許可するサイズを MB 単位で指定します。  

### <a name="more-info"></a>詳細
このページに表示されるファイル サイズ オプションの詳細については、「[CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)」をご覧ください。 

## <a name="whats-next"></a>次の操作  
 ウィザードで作成する新しいデータベースの名前を指定して **[OK]** をクリックしすると、 **[データベースの作成]** ダイアログ ボックスは **[変換先の選択]** ページに戻ります。 詳細については、「 [[変換先の選択] (SQL Server インポートおよびエクスポート ウィザード)](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)」をご覧ください。  

