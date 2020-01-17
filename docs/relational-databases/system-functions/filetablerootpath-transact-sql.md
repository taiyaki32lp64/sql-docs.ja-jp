---
title: FileTableRootPath (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- FileTableRootPath_TSQL
- FileTableRootPath
dev_langs:
- TSQL
helpviewer_keywords:
- FileTableRootPath function
ms.assetid: 0cba908a-c85c-4b09-b16a-df1cb333c629
author: rothja
ms.author: jroth
ms.openlocfilehash: 10b4aa19b86530213f852ea90f959a1d7ef6c74f
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251231"
---
# <a name="filetablerootpath-transact-sql"></a>FileTableRootPath (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  特定の FileTable または現在のデータベースのルートレベルの UNC パスを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
FileTableRootPath ( [ '[schema_name.]FileTable_name' ], @option )  
```  
  
## <a name="arguments"></a>引数  
 *FileTable_name*  
 FileTable の名前。 *FileTable_name*の型は**nvarchar**です。 これは省略可能なパラメーターです。 既定値は、現在のデータベースです。 *Schema_name*を指定することも省略可能です。 既定のパラメーター値を使用するには、 *FileTable_name*に NULL を渡すことができます。  
  
 *\@ オプション*  
 パスのサーバーコンポーネントをどのように書式設定するかを定義する整数式です。 *\@option*には、次のいずれかの値を指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**0**|サーバー名を次のような NetBIOS 形式に変換して返します。<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDatabase`<br /><br /> これは既定値です。|  
|**1**|次のように、サーバー名を変換せずに返します。<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDatabase`|  
|**2**|次のような、完全なサーバー パスを返します。<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDatabase`|  
  
## <a name="return-type"></a>戻り値の型  
 **nvarchar (4000)**  
  
 データベースが Always On 可用性グループに属している場合、 **FileTableRootPath**関数は、コンピューター名ではなく仮想ネットワーク名 (vnn) を返します。  
  
## <a name="general-remarks"></a>全般的な解説  
 **FileTableRootPath**関数は、次のいずれかの条件に該当する場合に NULL を返します。  
  
-   *FileTable_name*の値が無効です。  
  
-   呼び出し元に、指定されたテーブルまたは現在のデータベースを参照するための十分な権限がない。  
  
-   *Database_directory*の FILESTREAM オプションは、現在のデータベースに対して設定されていません。  
  
 詳しくは、「 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)」をご覧ください。  
  
## <a name="best-practices"></a>ベスト プラクティス  
 コードとアプリケーションが現在のコンピューターとデータベースから切り離された状態を維持するには、絶対ファイル パスに依存したコードを記述しないでください。 代わりに、次の例に示すように、 **FileTableRootPath**関数と**GetFileNamespacePath**関数を一緒に使用して、実行時にファイルの完全なパスを取得します。 既定では、 **GetFileNamespacePath** 関数は、データベースのルート パスの下のファイルの相対パスを返します。  
  
```sql  
USE MyDocumentDatabase;  
  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
@fullPath = varchar(1000);  
  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath()  
FROM DocumentStore  
WHERE Name = N'document.docx';  
```  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 **FileTableRootPath**関数には次のものが必要です。  
  
-   特定の FileTable のルートパスを取得するには、FileTable に対する権限を選択します。  
  
-   現在のデータベースのルートパスを取得するための**db_datareader**以上のアクセス許可。  
  
## <a name="examples"></a>使用例  
 次の例は、 **FileTableRootPath**関数を呼び出す方法を示しています。  
  
```  
USE MyDocumentDatabase;  
-- returns "\\MYSERVER\MSSQLSERVER\MyDocumentDatabase"  
SELECT FileTableRootPath();  
  
-- returns "\\MYSERVER\MSSQLSERVER\MyDocumentDatabase\MyFileTable"  
SELECT FileTableRootPath(N'dbo.MyFileTable');  
  
-- returns "\\MYSERVER\MSSQLSERVER\MyDocumentDatabase\MyFileTable"  
SELECT FileTableRootPath(N'MyFileTable');  
```  
  
## <a name="see-also"></a>関連項目  
 [FileTable 内のディレクトリとパスの操作](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
