---
title: FileTable へのファイルの読み込み | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], migrating files
- FileTables [SQL Server], bulk loading
- FileTables [SQL Server], loading files
ms.assetid: dc842a10-0586-4b0f-9775-5ca0ecc761d9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 43e5a9a6adcca7504aa90825ecd10e53e669c7e2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010009"
---
# <a name="load-files-into-filetables"></a>FileTable へのファイルの読み込み
  FileTable にファイルを読み込むまたは移行する方法について説明します。  
  
##  <a name="BasicsLoadNew"></a> FileTable へのファイルの読み込みまたは移行  
 FileTable へのファイルの読み込みや移行の方法は、ファイルが現在格納されている場所によって異なります。  
  
|ファイルの現在の場所|移行のオプション|  
|-------------------------------|---------------------------|  
|ファイルは現在、ファイル システム内に格納されている。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にはファイルに関する情報がありません。|FileTable は Windows ファイル システムにおいてフォルダーとして表示されるため、ファイルの移動またはコピーに使用できる任意の方法で、ファイルを新しい FileTable に簡単に読み込むことができます。 これらの方法には、Windows エクスプローラー、コマンド ライン オプション (xcopy、robocopy)、およびカスタム スクリプトまたはアプリケーションが含まれます。<br /><br /> 既存のフォルダーを FileTable に変換することはできません。|  
|ファイルは現在、ファイル システム内に格納されている。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、ファイルへのポインターが格納されたメタデータのテーブルが含まれています。|まず、前の項目で示したいずれかの方法を使用して、ファイルを移動またはコピーします。<br /><br /> 次に、ファイルの新しい場所を指すように既存のメタデータのテーブルを更新します。<br /><br /> 詳細については、「[例:ファイルを FileTable にファイル システムから移行](#HowToMigrateFiles)このトピックの「します。|  
  
###  <a name="HowToLoadNew"></a> 方法:FileTable にファイルを読み込む  
 ファイルを FileTable に読み込むには、次の方法を使用できます。  
  
-   Windows エクスプローラーで、基になるフォルダーから新しい FileTable フォルダーにファイルをドラッグ アンド ドロップします。  
  
-   コマンド プロンプト、バッチ ファイル、またはスクリプトでコマンド ライン オプション (MOVE、COPY、XCOPY、ROBOCOPY など) を使用します。  
  
-   **System.IO** 名前空間のメソッドを使用してファイルの移動またはコピーを実行するカスタム アプリケーションを C# または Visual Basic.NET で作成します。  
  
###  <a name="HowToMigrateFiles"></a> 例: ファイルをファイル システムから FileTable に移行する  
 このシナリオでは、ファイルはファイル システムに格納されていて、このファイルへのポインターを含むメタデータのテーブルが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に配置されています。 ここでは、ファイルを FileTable に移動した後、メタデータ内の各ファイルの元の UNC パスを FileTable の UNC パスに置き換えます。 この操作を行うには、[GetPathLocator &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getpathlocator-transact-sql) 関数を使用します。  
  
 この例では、既存のデータベース テーブルがあることを想定して`PhotoMetadata`、写真に関するデータを格納します。 このテーブルには、.jpg ファイルへの実際の UNC パスを含む `varchar`(512) 型の `UNCPath` 列があります。  
  
 画像ファイルをファイル システムから FileTable に移行するには、次の操作を実行する必要があります。  
  
1.  ファイルを格納する新しい FileTable を作成します。 この例では、`dbo.PhotoTable` というテーブル名を使用しますが、テーブルを作成するコードは示されていません。  
  
2.  xcopy または同様のツールを使用して、ディレクトリ構造を保ったまま .jpg ファイルを FileTable のルート ディレクトリにコピーします。  
  
3.  次のようなコードを使用して、`PhotoMetadata` テーブル内のメタデータを修正します。  
  
```sql  
--  Add a path locator column to the PhotoMetadata table.  
ALTER TABLE PhotoMetadata ADD pathlocator hierarchyid;  
  
-- Get the root path of the Photo directory on the File Server.  
DECLARE @UNCPathRoot varchar(100) = '\\RemoteShare\Photographs';  
  
-- Get the root path of the FileTable.  
DECLARE @FileTableRoot varchar(1000);  
SELECT @FileTableRoot = FileTableRootPath('dbo.PhotoTable');  
  
-- Update the PhotoMetadata table.  
  
-- Replace the File Server UNC path with the FileTable path.  
UPDATE PhotoMetadata  
    SET UNCPath = REPLACE(UNCPath, @UNCPathRoot, @FileTableRoot);  
  
-- Update the pathlocator column to contain the pathlocator IDs from the FileTable.  
UPDATE PhotoMetadata  
    SET pathlocator = GetPathLocator(UNCPath);  
```  
  
##  <a name="BasicsBulkLoad"></a> FileTable へのファイルの一括読み込み  
 FileTable の一括操作は通常のテーブルの動作と同じですが、次の制限があります。  
  
 FileTable には、ファイル/ディレクトリ名前空間の整合性を確保するためにシステムによって定義された制約があります。 これらの制約は、FileTable に一括で読み込まれるデータに対しても検証されます。 一部の一括挿入操作ではテーブル制約の無視が許可されるため、次の要件が適用されます。  
  
-   制約が適用される一括読み込み操作は、FileTable でも他のテーブルに対する操作と同じように実行できます。 このカテゴリには以下の操作が含まれます。  
  
    -   CHECK_CONSTRAINTS 句を含む bcp  
  
    -   CHECK_CONSTRAINTS 句を含む BULK INSERT  
  
    -   INSERT INTO ... IGNORE_CONSTRAINTS 句を含まない SELECT * FROM OPENROWSET(BULK ...)。  
  
-   FileTable のシステム定義の制約が無効化されない限り、制約が適用されない一括読み込み操作は失敗します。 このカテゴリには以下の操作が含まれます。  
  
    -   CHECK_CONSTRAINTS 句を含まない bcp  
  
    -   CHECK_CONSTRAINTS 句を含まない BULK INSERT  
  
    -   INSERT INTO ... SELECT * FROM OPENROWSET(BULK ...) (IGNORE_CONSTRAINTS 句を含む)。  
  
###  <a name="HowToBulkLoad"></a>方法:FileTable へのファイルの一括読み込みを行う  
 ファイルを FileTable に一括読み込みするには、次の方法を使用できます。  
  
-   **bcp**  
  
    -   **CHECK_CONSTRAINTS** 句を指定して呼び出します。  
  
    -   FileTable 名前空間を無効にし、 **CHECK_CONSTRAINTS** 句を指定せずに呼び出します。 次に、FileTable 名前空間を再有効化します。  
  
-   **BULK INSERT**  
  
    -   **CHECK_CONSTRAINTS** 句を指定して呼び出します。  
  
    -   FileTable 名前空間を無効にし、 **CHECK_CONSTRAINTS** 句を指定せずに呼び出します。 次に、FileTable 名前空間を再有効化します。  
  
-   **INSERT INTO ...SELECT \* FROM OPENROWSET(BULK ...)**  
  
    -   **IGNORE_CONSTRAINTS** 句を指定して呼び出します。  
  
    -   FileTable 名前空間を無効にし、 **IGNORE_CONSTRAINTS** 句を指定せずに呼び出します。 次に、FileTable 名前空間を再有効化します。  
  
 FileTable 制約の無効化の詳細については、「 [FileTable の管理](manage-filetables.md)」を参照してください。  
  
###  <a name="disabling"></a>方法:一括読み込みのための FileTable の制約を無効化する  
 システム定義の制約を一時的に無効化すると、制約の適用というオーバーヘッドなしで、FileTable へのファイルの一括読み込みを行うことができます。 詳細については、「 [FileTable の管理](manage-filetables.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Transact SQL を使用した FileTable へのアクセス](access-filetables-with-transact-sql.md)   
 [ファイル I/O API を使用した FileTable へのアクセス](access-filetables-with-file-input-output-apis.md)  
  
  
