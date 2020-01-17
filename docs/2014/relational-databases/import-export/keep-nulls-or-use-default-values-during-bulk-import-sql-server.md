---
title: 一括インポート中の NULL の保持または既定値の使用 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], null values
- bulk importing [SQL Server], default values
- data formats [SQL Server], null values
- bulk rowset providers [SQL Server]
- bcp utility [SQL Server], null values
- BULK INSERT statement
- default values
- OPENROWSET function, bulk importing
- data formats [SQL Server], default values
ms.assetid: 6b91d762-337b-4345-a159-88abb3e64a81
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5999a7f3a952cd0392136a96bf3bf166c8e6b155
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011902"
---
# <a name="keep-nulls-or-use-default-values-during-bulk-import-sql-server"></a>一括インポート中の NULL の保持または既定値の使用 (SQL Server)
  既定では、データをテーブルにインポートするとき、 **bcp** コマンドと BULK INSERT ステートメントによって、テーブルの列に対して定義されているすべての既定値が監視されます。 たとえば、データ ファイルに NULL フィールドがある場合は、NULL 値の代わりにその列の既定値が読み込まれます。 **bcp** コマンドと BULK INSERT ステートメントの両方で、NULL 値を保持することを指定することもできます。  
  
 これに対し、通常の INSERT ステートメントでは、既定値が挿入されるのではなく、NULL 値が保持されます。 INSERT ...SELECT * FROM OPENROWSET(BULK...) ステートメントでは、通常の INSERT と同じ基本的な動作に加えて、既定値を挿入するためのテーブル ヒントがサポートされます。  
  
> [!NOTE]  
>  テーブル列をスキップするサンプル フォーマット ファイルについては、「[フォーマット ファイルを使用したテーブル列のスキップ &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)」を参照してください。  
  
## <a name="sample-table-and-data-file"></a>サンプル テーブルとデータ ファイル  
 このトピックに記載されている例を実行するには、サンプル テーブルとデータ ファイルを作成する必要があります。  
  
### <a name="sample-table"></a>サンプル テーブル  
 以下の例を実行するには、 **dbo** スキーマに基づいて、 **MyTestDefaultCol2** という名前のテーブルを **AdventureWorks** サンプル データベース内で作成する必要があります。 このテーブルを作成するには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] クエリ エディターで次のコードを実行します。  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE MyTestDefaultCol2   
(Col1 smallint,  
Col2 nvarchar(50) DEFAULT 'Default value of Col2',  
Col3 nvarchar(50)   
);  
GO  
  
```  
  
 2 番目のテーブル列 `Col2`には既定値があることに注意してください。  
  
### <a name="sample-format-file"></a>サンプル フォーマット ファイル  
 一括インポートの一部の例では、`MyTestDefaultCol2-f-c.Fmt` テーブルに対応している XML 以外のフォーマット ファイル `MyTestDefaultCol2` を使用します。 このフォーマット ファイルを作成するには、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows コマンド プロンプトで、次のように入力します。  
  
```  
bcp AdventureWorks..MyTestDefaultCol2 format nul -c -f C:\MyTestDefaultCol2-f-c.Fmt -t, -r\n -T  
  
```  
  
 フォーマット ファイルの作成方法の詳細については、「[フォーマット ファイルの作成 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)」を参照してください。  
  
### <a name="sample-data-file"></a>サンプル データ ファイル  
 この例では、2 番目のフィールドに値を含まないサンプル データ ファイル `MyTestEmptyField2-c.Dat`を使用します。 `MyTestEmptyField2-c.Dat` データ ファイルには、以下のレコードが含まれています。  
  
```  
1,,DataField3  
2,,DataField3  
  
```  
  
## <a name="keeping-null-values-with-bcp-or-bulk-insert"></a>bcp または BULK INSERT を使用した NULL 値の保持  
 以下の修飾子は、一括インポート操作中、テーブル列の既定値がある場合にその既定値を継承するのではなく、データ ファイルの空のフィールドにそのフィールドの NULL 値を保持することを指定しています。  
  
|コマンド|Qualifier|修飾子の種類|  
|-------------|---------------|--------------------|  
|**bcp**|`-k`|スイッチ|  
|BULK INSERT|KEEPNULLS<sup>1</sup>|引数|  
  
 <sup>1</sup> BULK insert では、既定の値が使用可能な場合、テーブル列必要がありますを定義する null 値を許可します。  
  
> [!NOTE]  
>  上記の修飾子は、一括インポート コマンドによるテーブルでの DEFAULT 定義の確認を無効にします。 ただし、同時に実行するすべての INSERT ステートメントでは、DEFAULT 定義が必要です。  
  
 詳細については、「[bcp ユーティリティ](../../tools/bcp-utility.md)」と「[BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)」を参照してください。  
  
### <a name="examples"></a>使用例  
 以下の例では、 **bcp** または BULK INSERT を使用して一括インポートを行い、NULL 値を保持します。  
  
 2 番目のテーブル列 **Col2**には、既定値があります。 データ ファイルの対応するフィールドには、空の文字列が含まれています。 既定では、 **bcp** または BULK INSERT を使用して、このデータ ファイルから **MyTestDefaultCol2** テーブルにデータをインポートすると、 **Col2** の既定値が挿入され、以下の結果が生成されます。  
  
||||  
|-|-|-|  
|`1`|`Default value of Col2`|`DataField3`|  
|`2`|`Default value of Col2`|`DataField3`|  
  
 挿入する"`NULL`「の代わりに」`Default value of Col2`"を使用する必要がある、`-k`スイッチまたは KEEPNULL オプションを次に示すよう**bcp**と BULK INSERT の例。  
  
#### <a name="using-bcp-and-keeping-null-values"></a>bcp の使用および NULL 値の保持  
 次の例では、 **bcp** コマンドで NULL 値を保持する方法について説明します。 **bcp** コマンドには、次のスイッチがあります。  
  
|スイッチ|説明|  
|------------|-----------------|  
|`-f`|コマンドでフォーマット ファイルが使用されていることを指定します。|  
|`-k`|一括コピー操作時、空の列には、挿入される列の既定値ではなく、NULL 値が保持されます。|  
|`-T`|bcp ユーティリティが信頼関係接続を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続することを指定します。|  
  
 Windows のコマンド プロンプトで、次のように入力します。  
  
```  
bcp AdventureWorks..MyTestDefaultCol2 in C:\MyTestEmptyField2-c.Dat -f C:\MyTestDefaultCol2-f-c.Fmt -k -T  
  
```  
  
#### <a name="using-bulk-insert-and-keeping-null-values"></a>BULK INSERT の使用および NULL 値の保持  
 次の例では、BULK INSERT ステートメントで KEEPNULLS オプションを使用する方法について説明します。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] クエリ エディターなどのクエリ ツールから、次のコードを実行します。  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT MyTestDefaultCol2  
   FROM 'C:\MyTestEmptyField2-c.Dat'  
   WITH (  
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ',',  
      KEEPNULLS  
   );  
GO  
  
```  
  
## <a name="keeping-default-values-with-insert--select--from-openrowsetbulk"></a>INSERT ...SELECT * FROM OPENROWSET(BULK...)  
 既定では、一括読み込み操作で指定されないすべての列が、INSERT ...SELECT * FROM OPENROWSET(BULK...) を使用してテーブルにインポートできます。ただし、データ ファイルのフィールドが空の場合、対応するテーブル列に既定値があるときはその列で既定値を使用することを指定できます。 既定値を使用するには、次のテーブル ヒントを指定します。  
  
|コマンド|修飾子|修飾子の種類|  
|-------------|---------------|--------------------|  
|INSERT ...SELECT * FROM OPENROWSET(BULK...)|WITH(KEEPDEFAULTS)|テーブル ヒント|  
  
> [!NOTE]  
>  詳細については、「[INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)」、「[SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)」、「[OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)」、「[テーブル ヒント &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)」を参照してください。  
  
### <a name="examples"></a>使用例  
 次の INSERT ...SELECT * FROM OPENROWSET(BULK...) の例では、データを一括インポートし、既定値を保持します。  
  
 この例を実行するには、 **MyTestDefaultCol2** サンプル テーブルと `MyTestEmptyField2-c.Dat` データ ファイルを作成し、 `MyTestDefaultCol2-f-c.Fmt`というフォーマット ファイルを使用する必要があります。 これらのサンプルの作成については、このトピックの前半の「サンプル テーブルとデータ ファイル」を参照してください。  
  
 2 番目のテーブル列 **Col2**には、既定値があります。 データ ファイルの対応するフィールドには、空の文字列が含まれています。 INSERT ...SELECT \* FROM OPENROWSET(BULK...) によって、このデータ ファイルのフィールドが **MyTestDefaultCol2** テーブルにインポートされるときに、既定では、**Col2** には既定値ではなく NULL が挿入されます。 この既定の動作により、以下の結果が生成されます。  
  
||||  
|-|-|-|  
|`1`|`NULL`|`DataField3`|  
|`2`|`NULL`|`DataField3`|  
  
 "`Default value of Col2`" ではなく既定値 "`NULL`" を挿入するには、次の例で説明するように、KEEPDEFAULTS テーブル ヒントを使用する必要があります。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] クエリ エディターなどのクエリ ツールから、次のコードを実行します。  
  
```  
USE AdventureWorks;  
GO  
INSERT INTO MyTestDefaultCol2  
    WITH (KEEPDEFAULTS)  
    SELECT *  
      FROM OPENROWSET(BULK  'C:\MyTestEmptyField2-c.Dat',  
      FORMATFILE='C:\MyTestDefaultCol2-f-c.Fmt'       
      ) as t1 ;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [データの一括インポート時の ID 値の保持 &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [一括エクスポートまたは一括インポートのデータの準備 &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **フォーマット ファイルを作成するには**  
  
-   [フォーマット ファイルの作成 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [データの一括インポートでのフォーマット ファイルの使用 &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [フォーマット ファイルを使用したテーブル列とデータ ファイル フィールドのマッピング &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [フォーマット ファイルを使用したデータ フィールドのスキップ &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [フォーマット ファイルを使用したテーブル列のスキップ &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **一括インポートまたは一括エクスポートのデータ形式を使用するには**  
  
-   [以前のバージョンの SQL Server からのネイティブ形式データおよび文字形式データのインポート](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode 文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **bcp を使用した互換性のためのデータ形式を指定するには**  
  
-   [フィールド ターミネータと行ターミネータの指定 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
-   [bcp を使用したデータ ファイルのプレフィックス長の指定 &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [bcp を使用したファイル ストレージ型の指定 &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [テーブル ヒント &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)  
  
  
