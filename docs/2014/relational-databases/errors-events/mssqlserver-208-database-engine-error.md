---
title: MSSQLSERVER_208 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 208 (Database Engine error)
ms.assetid: 4b1895f5-3197-4da1-af86-954c93507956
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b87a950c29cf202124e27b319eb56fb6a6e1857d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914917"
---
# <a name="mssqlserver208"></a>MSSQLSERVER_208
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|208|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQ_BADOBJECT|  
|メッセージ テキスト|オブジェクト名 '%.*ls' が無効です。|  
  
## <a name="explanation"></a>説明  
 指定されたオブジェクトが見つかりません。  
  
### <a name="possible-causes"></a>考えられる原因  
 このエラーは次のいずれかの問題が原因で生じている可能性があります。  
  
-   オブジェクトが正しく指定されていない。  
  
-   現在のデータベースまたは指定されたデータベースにオブジェクトが存在しない。  
  
-   オブジェクトは存在するが、ユーザーからアクセスできない。 たとえば、オブジェクトに対する権限がユーザーにない場合や、EXECUTE ステートメント内で作成したオブジェクトに EXECUTE ステートメントのスコープ外からアクセスしている場合などが考えられます。  
  
## <a name="user-action"></a>ユーザーの操作  
 次の情報を確認し、必要に応じてステートメントを修正します。  
  
-   オブジェクト名のスペルが正しいかどうか。  
  
-   現在のデータベース コンテキストが正しいかどうか。 オブジェクトのデータベース名を指定していない場合は、現在のデータベースにオブジェクトが存在する必要があります。 データベース コンテキストの設定の詳細については、「[USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql)」を参照してください。  
  
-   オブジェクトがシステム テーブルに存在するかどうか。 テーブルやその他のスキーマ スコープ オブジェクトが存在するかどうかを確認するには、**sys.objects** カタログ ビューでクエリします。 オブジェクトがシステム テーブルにない場合、そのオブジェクトは削除されたか、ユーザーにオブジェクト メタデータを表示する権限がないかのいずれかです。 オブジェクト メタデータの表示権限の詳細については、「[メタデータ表示の構成](../security/metadata-visibility-configuration.md)」を参照してください。  
  
-   オブジェクトがユーザーの既定のスキーマに含まれているかどうか。 オブジェクトがユーザーの既定のスキーマに含まれていない場合は、*schema_name.object_name* という 2 部構成の形式を使用してオブジェクトを指定する必要があります。 スカラー値関数は、必ず 2 つ以上の要素で構成される名前を使用して呼び出す必要があります。  
  
-   データベースの照合順序で大文字と小文字が区別されるかどうか。  
  
     大文字と小文字が区別される照合順序がデータベースで使用されている場合、オブジェクト名は、大文字と小文字の区別を含め、データベース内のオブジェクトと一致する必要があります。 たとえば、大文字と小文字が区別される照合順序を使用しているデータベースでオブジェクトが **MyTable** と指定されている場合、クエリで **mytable** または **Mytable** と指定してそのオブジェクトを参照すると、エラー 208 が返されます。これはオブジェクト名が一致しないためです。  
  
     データベースの照合順序を確認するには、次のステートメントを実行します。  
  
    ```  
    SELECT collation_name FROM sys.databases WHERE name = 'database_name';  
    ```  
  
     照合順序名に含まれる省略形 CS は、照合順序で大文字と小文字が区別されることを示します。 たとえば、Latin1_General_CS_AS は、大文字と小文字およびアクセントが区別される照合順序です。 CI は、大文字と小文字が区別されない照合順序であることを示します。  
  
-   ユーザーがオブジェクトへのアクセス権限を持っているかどうか。 オブジェクトに対するユーザーの権限を確認するには、**Has_Perms_By_Name** システム関数を使用します。  
  
## <a name="see-also"></a>参照  
 [USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql)   
 [メタデータ表示の構成](../security/metadata-visibility-configuration.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/has-perms-by-name-transact-sql)  
  
  
