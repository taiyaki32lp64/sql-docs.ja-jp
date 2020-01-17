---
title: FileTable 内のディレクトリとパスの操作 | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], directories
ms.assetid: f1e45900-bea0-4f6f-924e-c11e1f98ab62
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2f31288df7d03bf527f1ee0a0bcd3b8ed84bba19
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908701"
---
# <a name="work-with-directories-and-paths-in-filetables"></a>FileTable 内のディレクトリとパスの操作
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  FileTable 内でファイルが格納されるディレクトリ構造について説明します。  
  
##  <a name="HowToDirectories"></a> 方法:FileTable 内のディレクトリとパスの操作  
 次の 3 つの関数を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]で FileTable ディレクトリを操作することができます。  
  
|目的|使用する関数|  
|------------------------|-----------------------|  
|特定の FileTable または現在のデータベースの、ルート レベルの UNC パスを取得する。|[FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md)|  
|FileTable 内のファイルまたはディレクトリの絶対 UNC パスまたは相対 UNC パスを取得する。|[GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)|  
|パスを指定して、FileTable 内の指定されたファイルまたはディレクトリのパス ロケーター ID 値を取得する。|[GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md)|  
  
##  <a name="BestPracticeRelativePaths"></a> 方法:相対パスを使用して移植可能なコードを実現する  
 コードとアプリケーションが現在のコンピューターとデータベースから切り離された状態を維持するには、絶対ファイル パスに依存したコードを記述しないでください。 代わりに、以下の例に示すように [FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md) 関数および [GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)関数を併用して、実行時にファイルの完全なパスを取得します。 既定では、 **GetFileNamespacePath** 関数は、データベースのルート パスの下のファイルの相対パスを返します。  
  
```sql  
USE database_name;  
DECLARE @root nvarchar(100);  
DECLARE @fullpath nvarchar(1000);  
  
SELECT @root = FileTableRootPath();  
SELECT @fullpath = @root + file_stream.GetFileNamespacePath()  
    FROM filetable_name  
    WHERE name = N'document_name';  
  
PRINT @fullpath;  
GO  
```  
  
##  <a name="restrictions"></a> 重要な制限  
  
###  <a name="nesting"></a> 入れ子のレベル  
  
> **重要!!** FileTable ディレクトリ内には、15 レベルを超えるサブディレクトリを格納できません。 15 レベルのサブディレクトリを格納した場合、最も深いレベルにファイルを置くことはできません。そのファイルが、さらに深いレベルを表すことになるためです。  
  
###  <a name="fqnlength"></a> 完全なパス名の長さ  
  
> **重要!!** NTFS ファイル システムは、Windows シェルおよび大部分の Windows API の上限である 260 文字よりも長いパス名をサポートします。 そのため、Transact-SQL を使用して、完全なパス名が 260 文字を超えているために Windows エクスプローラーや他の多くの Windows アプリケーションで表示したり開いたりできないファイルを、FileTable のファイル階層内に作成できます。 ただし、Transact-SQL を使用してこれらのファイルに引き続きアクセスできます。  
  
##  <a name="fullpath"></a> FileTable に格納されているアイテムへの完全なパス  
 FileTable 内のファイルまたはディレクトリへの完全なパスには、次の要素が先頭に付きます。  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス レベルでの FILESTREAM ファイル I/O アクセスが有効になっている共有。  
  
2.  データベース レベルで指定された **DIRECTORY_NAME** 。  
  
3.  FileTable レベルで指定された **FILETABLE_DIRECTORY** 。  

 以上を組み合わせた階層は、次のようになります。  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\`  
  
 このディレクトリ階層は、FileTable のファイル名前空間のルートを構成します。 このディレクトリ階層の下に、FileTable の FILESTREAM データがファイルとして格納されます。また、サブディレクトリとしても格納され、ファイルおよびサブディレクトリを格納することができます。  
  
 インスタンス レベルの FILESTREAM 共有の下に作成されたディレクトリ階層は仮想ディレクトリ階層であることに注意してください。 階層は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに格納され、NTFS ファイル システム内には物理的に表示されません。 FILESTREAM 共有の下にあるファイルおよびディレクトリ、および FILESTREAM 共有に含まれる FileTables 内のファイルおよびディレクトリにアクセスするすべての操作は、ファイル システムに埋め込まれた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントによってインターセプトされ、処理されます。  
  
##  <a name="roots"></a> インスタンス レベル、データベース レベル、および FileTable レベルのルート ディレクトリのセマンティクス  
 このディレクトリ階層は次のセマンティクスに従います。  
  
-   インスタンス レベルの FILESTREAM 共有は管理者によって構成され、サーバーのプロパティとして格納されます。 この共有の名前は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して変更できます。 名前変更の操作は、サーバーを再起動するまで有効になりません。  
  
-   新しいデータベースを作成した場合、データベース レベルの **DIRECTORY_NAME** は既定で null です。 管理者は **ALTER DATABASE** ステートメントを使用して、この名前を設定または変更することができます。 名前は、インスタンス内で一意であることが必要です (大文字と小文字は区別されません)。  
  
-   通常、 **FILETABLE_DIRECTORY** 名は、FileTable を作成する際に **CREATE TABLE** ステートメントの中で指定します。 この名前は、 **ALTER TABLE** コマンドを使用して変更することができます。  
  
-   ファイル I/O 操作でこれらのルート ディレクトリの名前を変更することはできません。  
  
-   排他的なファイル ハンドルを使用してこれらのルート ディレクトリを開くことはできません。  
  
##  <a name="is_directory"></a> FileTable スキーマの is_directory 列  
 次の表に、 **is_directory** 列と、FileTable の FILESTREAM データを格納する **file_stream** 列との間のやり取りを示します。  
  
||||  
|-|-|-|  
|*is_directory* **の値**|*file_stream* **の値**|**動作**|  
|FALSE|NULL|これは、システム定義の制約によってキャッチされる無効な組み合わせです。|  
|FALSE|\<値>|アイテムはファイルを表します。|  
|TRUE|NULL|アイテムはディレクトリを表します。|  
|TRUE|\<値>|これは、システム定義の制約によってキャッチされる無効な組み合わせです。|  
  
##  <a name="alwayson"></a> AlwaysOn 可用性グループでの仮想ネットワーク名 (VNN) の使用  
 FILESTREAM データまたは FileTable データを格納するデータベースが AlwaysOn 可用性グループに属する場合、次の処理が行われます。  
  
-   FILESTREAM および FileTable 関数は、コンピューター名ではなく仮想ネットワーク名 (VNN) のやり取りを行います。 関数の詳細については、「[Filestream および FileTable 関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filestream-and-filetable-functions-transact-sql.md)」を参照してください。  
  
-   ファイル システム API を介した FILESTREAM または FileTable データへのすべてのアクセスでは、コンピューター名ではなく VNN を使用する必要があります。 詳細については、「[FILESTREAM および FileTable と AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [FileTable の前提条件の有効化](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)   
 [FileTable の作成、変更、および削除](../../relational-databases/blob/create-alter-and-drop-filetables.md)   
 [Transact SQL を使用した FileTable へのアクセス](../../relational-databases/blob/access-filetables-with-transact-sql.md)   
 [ファイル I/O API を使用した FileTable へのアクセス](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)  
  
  
