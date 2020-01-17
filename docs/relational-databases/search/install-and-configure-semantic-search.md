---
title: セマンティック検索のインストールと構成 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], installing
- semantic search [SQL Server], configuring
ms.assetid: 2cdd0568-7799-474b-82fb-65d79df3057c
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: cac6ecd59b270feecea3590c33c9dc8c41f1edcc
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73638039"
---
# <a name="install-and-configure-semantic-search"></a>セマンティック検索のインストールと構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  統計的セマンティック検索の前提条件と、これらをインストールまたは確認する方法について説明します。  
  
## <a name="install-semantic-search"></a>セマンティック検索のインストール  
  
###  <a name="HowToCheckInstalled"></a> セマンティック検索がインストールされているかどうかを確認する  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md) メタデータ関数の **IsFullTextInstalled** プロパティに対してクエリを実行します。  
  
 戻り値 1 は、データベースに対してフルテキスト検索とセマンティック検索がインストールされていることを示します。戻り値 0 は、フルテキスト検索とセマンティック検索がインストールされていないことを示します。  
  
```sql  
SELECT SERVERPROPERTY('IsFullTextInstalled');  
GO  
```  
  
###  <a name="BasicsSemanticSearch"></a> セマンティック検索のインストール  
 セマンティック検索をインストールするには、SQL Server のセットアップ時に、 **[インストールする機能]** ページで **[検索のためのフルテキスト抽出とセマンティック抽出]** を選択します。  
  
 セマンティック検索はフルテキスト検索に依存します。 この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 2 つのオプション機能は一緒にインストールされます。  
  
## <a name="install-the-semantic-language-statistics-database"></a>セマンティック言語統計データベースをインストールする  
 セマンティック検索は、別途、"セマンティック言語統計データベース" と呼ばれる外部の機能に依存しています。 このデータベースには、セマンティック検索で必要な統計的言語モデルが含まれています。 1 つのセマンティック言語統計データベースには、セマンティック インデックス作成でサポートされるすべての言語の言語モデルが含まれています。  
  
###  <a name="HowToCheckDatabase"></a> セマンティック言語統計データベースがインストールされているかどうかを確認する  
 カタログ ビュー [sys.fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md) に対してクエリを実行します。  
  
 実行対象のインスタンスにセマンティック言語統計データベースがインストールされ登録されている場合、クエリ結果には、そのデータベースに関する単一行から成る情報が格納されています。  
  
```sql  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
###  <a name="HowToInstallModel"></a> セマンティック言語統計データベースをインストール、アタッチ、および登録する  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ プログラムでは、セマンティック言語統計データベースはインストールされません。 セマンティック インデックス作成の前提条件であるセマンティック言語統計データベースをセットアップするには、次の手順を実行します。  
  
 **1.セマンティック言語統計データベースをインストールします。**  
 
 1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール メディアでセマンティック言語統計データベースを見つけるか、Web からダウンロードします。  
  
        1.  **のインストール メディアで** SemanticLanguageDatabase.msi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] という名前の Windows インストーラー パッケージを見つけます。  
  
        2.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] ダウンロード センターの「[Microsoft® SQL Server® 2016 Semantic Language Statistics](https://www.microsoft.com/download/details.aspx?id=52681)」ページからインストーラー パッケージをダウンロードします。  
  
2.  **SemanticLanguageDatabase.msi** Windows インストーラー パッケージを実行して、データベースおよびログ ファイルを抽出します。  
  
     抽出先のディレクトリは必要に応じて変更できます。 既定では、Program Files フォルダー内の **Microsoft Semantic Language Database** という名前のフォルダーにファイルが抽出されます。 MSI ファイルには、圧縮データベース ファイルおよびログ ファイルが格納されます。  
  
3.  抽出されたデータベース ファイルとログ ファイルを、ファイル システム内の適切な場所に移動します。  
  
     ファイルを既定の場所に残した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の別のインスタンスのデータベースの別のコピーを抽出できません。  
  
    > [!IMPORTANT]  
    >  セマンティック言語統計データベースの抽出時に、ファイル システム内の既定の場所にあるデータベース ファイルおよびログ ファイルに制限付きの権限が割り当てられます。 そのため、データベースを既定の場所に残した場合、ユーザーによってはデータベースにアタッチする権限がない可能性があります。 データベースをアタッチしようとしたときにエラーが発生した場合は、ファイルを移動するか、ファイル システムの権限を確認し、必要に応じて修正してください。  
  
 **2.セマンティック言語統計データベースをアタッチします。**
   
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用するか、[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md) を **FOR ATTACH** 構文で呼び出して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにデータベースをアタッチします。 詳細については、「[データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)」を参照してください。  
  
 既定では、データベースの名前が **semanticsdb**になります。 データベースをアタッチする際、必要に応じて、別の名前を付けてください。 この名前は、後続の手順でデータベースを登録する際に必要になります。  
  
```sql  
CREATE DATABASE semanticsdb  
            ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb.mdf' )  
            LOG ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb_log.ldf' )  
            FOR ATTACH;  
GO  
```  
  
 このコード例では、データベースを既定の場所から新しい場所に移動済みであることを前提としています。  
  
 **3.セマンティック言語統計データベースを登録します。** 
  
 データベースのアタッチ時に指定した名前を使用して、ストアド プロシージャ [sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql.md) を次のように呼び出します。  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
GO  
```  

##  <a name="reqinstall"></a> セマンティック言語統計データベースの要件と制限  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスでアタッチおよび登録できるセマンティック言語統計データベースは 1 つのみです。  
  
     1 台のコンピューターに存在する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各インスタンスには、それぞれ、セマンティック言語統計データベースの物理コピーが必要です。 個々のコピーをそれぞれのインスタンスにアタッチしてください。  
  
-   登録されている有効なセマンティック言語統計データベースをデタッチし、同じ名前の任意のデータベースに置き換えることはできません。 このような操作を行うと、アクティブなインデックス作成およびそれ以降のインデックス作成が失敗します。  
  
-   セマンティック言語統計データベースは読み取り専用です。 このデータベースはカスタマイズできません。 なんらかの方法でデータベースのコンテンツを変更すると、今後のセマンティック インデックス作成の結果が不明確になります。 このデータの元の状態を復元するには、変更後のデータベースを削除して、データベースの変更されていない新しいコピーをダウンロードおよびアタッチします。  
  
-   セマンティック言語統計データベースはデタッチまたは削除することができます。 アクティブなインデックス作成操作があり、データベースが読み取りロックされている場合、デタッチおよび削除の操作は失敗またはタイムアウトになります。これは、従来と同じ動作です。 データベースが削除された後は、セマンティック インデックス作成操作が失敗します。  
 
##  <a name="HowToUnregister"></a> セマンティック言語統計データベースを削除する  

###  <a name="unregister-detach-and-remove-the-semantic-language-statistics-database"></a>セマンティック言語統計データベースを登録解除、デタッチ、および削除する 

 **1.セマンティック言語統計データベースを登録解除します。**
   
 ストアド プロシージャ [sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql.md) を呼び出します。 セマンティック言語統計データベースは 1 つのインスタンスにつき 1 つしか存在しないため、データベースの名前を指定する必要はありません。  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
 **2.セマンティック言語統計データベースをデタッチします。**  
 
 ストアド プロシージャ [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) を呼び出し、データベース名を指定します。  
  
```sql  
USE master;  
GO  
  
EXEC sp_detach_db @dbname = N'semanticsdb';  
GO  
```  
  
 **3.セマンティック言語統計データベースを削除します。**  
 
 データベースの登録を解除し、デタッチした後は、データベース ファイルを簡単に削除できます。 アンインストール プログラムはありません。また、コントロール パネルの **[プログラムと機能]** のエントリもありません。  
  
## <a name="install-optional-support-for-newer-document-types"></a>新しいドキュメントの種類のオプション サポートをインストールする  
  
###  <a name="office"></a> Microsoft Office およびその他の Microsoft ドキュメントの種類の最新のフィルターをインストールする  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] の最新のワード ブレーカーとステマーがインストールされますが、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office ドキュメントおよびその他の [!INCLUDE[msCoName](../../includes/msconame-md.md)] ドキュメントの種類の最新のフィルターはインストールされません。 これらのフィルターは、最新バージョンの [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office およびその他の [!INCLUDE[msCoName](../../includes/msconame-md.md)] アプリケーションで作成されたドキュメントのインデックスを作成するために必要です。 最新のフィルターをダウンロードするには、「 [Microsoft Office 2010 フィルター パック](https://www.microsoft.com/download/details.aspx?id=17062)」を参照してください。 (Office 2013 または Office 2016 用のフィルター パック リリースはありません)。
  
  
