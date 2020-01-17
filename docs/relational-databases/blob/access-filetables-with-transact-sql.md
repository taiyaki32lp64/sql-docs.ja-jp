---
title: Transact SQL を使用した FileTable へのアクセス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], accessing files with T-SQL
ms.assetid: 3c4a5ffb-c521-4696-99cb-2b03cffc9c02
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c86ab8b3f29699e807c61b571832c106ab235710
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018893"
---
# <a name="access-filetables-with-transact-sql"></a>Transact SQL を使用した FileTable へのアクセス
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[tsql](../../includes/tsql-md.md)] データ操作言語 (DML) コマンドによる FileTable の操作について説明します。  
  
##  <a name="BasicsInsert"></a> FileTable での INSERT 操作  
 FileTable で **INSERT** 操作を行う場合は、次の点に注意してください。  
  
-   ファイル属性のすべての列には NOT NULL 制約があります。 明示的に値が設定されなかった場合は、適切な既定値が使用されます。  
  
-   INSERT ステートメントで **name**、**path_locator**、**parent_path_locator**、またはファイル属性を設定する場合、システム定義の制約が適用されます。  
  
-   アプリケーションは、[GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md) 関数にファイル システム パスを渡すことで、ファイルまたはディレクトリの **path_locator** を取得できます。  
  
##  <a name="BasicsUpdate"></a> FileTable での UPDATE 操作  
 FileTable で **UPDATE** 操作を行う場合は、次の点に注意してください。  
  
-   すべてのユーザー定義データの更新が許可されます。  
  
-   INSERT ステートメントで **name**、 **path_locator**、 **parent_path_locator**、またはファイル属性を設定する場合、システム定義の制約が適用されます。  
  
-   **file_stream** 列の FILESTREAM データは、他の列 (timestamps を含む) に一切影響を及ぼさずに更新することができます。  
  
##  <a name="BasicsDelete"></a> FileTable での DELETE 操作  
 FileTable で **DELETE** 操作を行う場合は、次の点に注意してください。  
  
-   行を削除すると、対応するファイルまたはディレクトリがファイル システムから削除されます。  
  
-   対応するディレクトリに他のファイルまたはディレクトリが存在する場合、行の削除は失敗します。  
  
##  <a name="BasicsConstraints"></a> DML での FileTable の操作の制約  
 システム定義の制約は、ファイル名前空間階層構造の整合性が DML アクションによって損なわれることのないように制御します。 適用される制約は、次のとおりです。  
  
-   ファイルまたはディレクトリの **name** を設定または変更する場合:  
  
    -   ファイルおよびディレクトリに対する Windows の名前付け規則が適用されます。  
  
    -   親ディレクトリ内での名前の一意性が強制されます。  
  
-   **path_locator** あるいは **parent_path_locator**を設定または変更することによってファイル (またはディレクトリ) の場所を設定または変更した場合:  
  
    -   一意性が適用されます。  
  
    -   ディレクトリおよびファイルの階層ツリーの一貫性が強制されます ( **path_locator** 値と **parent_path_locator** 値の一貫性を含む)。  
  
-   **file_stream** 列が null の場合、 **is_directory** の値を true に設定することはできません。 **file_stream** 列のデータは、その行がディレクトリではなくファイルを表していることを示します。  
  
-   ファイル属性列は NULL にできません。 NOT NULL 制約が既定値で適用されます。  
  
-   **last_access_time** の値が **last_write_time** や **creation_time**よりも前に来ることはできません。  
  
## <a name="see-also"></a>参照  
 [FileTable へのファイルの読み込み](../../relational-databases/blob/load-files-into-filetables.md)   
 [FileTable 内のディレクトリとパスの操作](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)   
 [ファイル I/O API を使用した FileTable へのアクセス](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)   
 [FileTable DDL、関数、ストアド プロシージャ、およびビュー](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
  
  
