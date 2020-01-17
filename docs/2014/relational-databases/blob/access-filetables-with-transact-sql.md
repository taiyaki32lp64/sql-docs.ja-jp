---
title: Transact SQL を使用した FileTable へのアクセス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], accessing files with T-SQL
ms.assetid: 3c4a5ffb-c521-4696-99cb-2b03cffc9c02
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b56bba0567a96b7bdd7b75ad191d553ffa019930
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010428"
---
# <a name="access-filetables-with-transact-sql"></a>Transact SQL を使用した FileTable へのアクセス
  [!INCLUDE[tsql](../../includes/tsql-md.md)] データ操作言語 (DML) コマンドによる FileTable の操作について説明します。  
  
##  <a name="BasicsInsert"></a> FileTable での INSERT 操作  
 FileTable で **INSERT** 操作を行う場合は、次の点に注意してください。  
  
-   ファイル属性のすべての列には NOT NULL 制約があります。 明示的に値が設定されなかった場合は、適切な既定値が使用されます。  
  
-   INSERT ステートメントで **name**、**path_locator**、**parent_path_locator**、またはファイル属性を設定する場合、システム定義の制約が適用されます。  
  
-   アプリケーションは、[GetPathLocator &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getpathlocator-transact-sql) 関数にファイル システム パスを渡すことで、ファイルまたはディレクトリの **path_locator** を取得できます。  
  
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
  
## <a name="see-also"></a>関連項目  
 [FileTable へのファイルの読み込み](load-files-into-filetables.md)   
 [FileTable 内のディレクトリとパスの操作](work-with-directories-and-paths-in-filetables.md)   
 [ファイル I/O API を使用した FileTable へのアクセス](access-filetables-with-file-input-output-apis.md)   
 [FileTable DDL、関数、ストアド プロシージャ、およびビュー](../views/views.md)  
  
  
