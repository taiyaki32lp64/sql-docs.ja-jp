---
title: Unicode 文字形式を使用したデータのインポートまたはエクスポート (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], Unicode character
- Unicode [SQL Server], bulk importing and exporting
ms.assetid: 74342a11-c1c0-4746-b482-7f3537744a70
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34e8f4a5b49c9e023c224e62c23326864ef26f65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011650"
---
# <a name="use-unicode-character-format-to-import-or-export-data-sql-server"></a>Unicode 文字形式を使用したデータのインポートまたはエクスポート (SQL Server)
  拡張文字や DBCS 文字を含むデータ ファイルを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンス間でデータを一括転送する場合は、Unicode 文字形式を使用することをお勧めします。 Unicode 文字データ形式を使用すると、操作を実行するクライアントで使用しているコード ページとは異なるコード ページを使用して、サーバーからデータをエクスポートできます。 このような場合、Unicode 文字形式を使用すると、次の利点があります。  
  
-   転送元のデータと転送先のデータが Unicode データ型の場合、Unicode 文字形式を使用するとすべての文字データが保持されます。  
  
-   転送元のデータと転送先のデータが Unicode 以外のデータ型の場合、Unicode 文字形式を使用すると、転送先のデータで表現できない転送元のデータに含まれる拡張文字の損失を最小限に抑えられます。  
  
 Unicode 文字形式のデータ ファイルは、Unicode ファイルの規則に従います。 ファイルの先頭の 2 バイトは、16 進数の 0xFFFE です。 これらのバイトは、バイト順マークとしての役割を果たし、高位のバイトをファイルの先頭に格納するか、最後に格納するかを指定します。  
  
> [!IMPORTANT]  
>  Unicode 文字データ ファイルを操作するフォーマット ファイルの場合、すべての入力フィールドが Unicode テキスト文字列 (つまり、固定サイズの Unicode 文字列または終端文字が指定された Unicode 文字列) でなければなりません。  
  
 Unicode 文字形式のデータ ファイルに格納されている `sql_variant` データの動作は、`nchar` データではなく `char` データとして格納されている点を除いて、文字形式のデータ ファイルの場合と同様になります。 文字形式の詳細については、「 [Collation and Unicode Support](../collations/collation-and-unicode-support.md)」を参照してください。  
  
 Unicode 文字形式に用意されている既定以外のフィールド ターミネータまたは行ターミネータを使用するには、「[フィールド ターミネータと行ターミネータの指定 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)」を参照してください。  
  
## <a name="command-options-for-unicode-character-format"></a>Unicode 文字形式のコマンド オプション  
 Unicode 文字形式のデータは**bcp**、BULK INSERT、または INSERT ...SELECT \* FROM OPENROWSET(BULK...)。**bcp** コマンドまたは BULK INSERT ステートメントの場合は、コマンド ラインでデータ形式を指定できます。 INSERT ...SELECT * FROM OPENROWSET(BULK...) ステートメントの場合は、フォーマット ファイルでデータ形式を指定する必要があります。  
  
 Unicode 文字形式は、次のコマンド ライン オプションでサポートされています。  
  
|コマンド|オプション|説明|  
|-------------|------------|-----------------|  
|**bcp**|**-w**|Unicode 文字形式を使用します。|  
|BULK INSERT|DATAFILETYPE **='** widechar **'**|データの一括インポート時に Unicode 文字形式を使用します。|  
  
 詳細については、[bcp ユーティリティ](../../tools/bcp-utility.md)、[BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)」、または「[OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)」を参照してください。  
  
> [!NOTE]  
>  また、フォーマット ファイルでフィールドごとに形式を指定することもできます。 詳細については、「[データのインポートまたはエクスポート用のフォーマット ファイル &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例は、 **bcp** を使用して Unicode 文字データを一括エクスポートする方法と、BULK INSERT を使用して Unicode 文字データを一括インポートする方法を示しています。  
  
### <a name="sample-table"></a>サンプル テーブル  
 次の例を実行するには、 `myTestUniCharData` スキーマに基づいて、 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] という名前のテーブルを `dbo` サンプル データベース内に作成する必要があります。 このテーブルを作成しないと、例を実行できません。 このテーブルを作成するには、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] クエリ エディターで、次のコードを実行します。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestUniCharData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 このテーブルを作成し、上記のコードにより生成された内容を表示するには、次のステートメントを実行します。  
  
```  
INSERT INTO myTestUniCharData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3')   
        ,(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestUniCharData;  
  
```  
  
### <a name="using-bcp-to-bulk-export-unicode-character-data"></a>bcp を使用した Unicode 文字データの一括エクスポート  
 テーブルからデータ ファイルにデータをエクスポートするには、 **bcp** で **out** オプションと次の修飾子を組み合わせて使用します。  
  
|修飾子|説明|  
|----------------|-----------------|  
|**-w**|Unicode 文字形式を指定します。|  
|**-t** `,`|コンマ (`,`) をフィールド ターミネータとして指定します。<br /><br /> 注:既定のフィールド ターミネータは、タブの Unicode 文字 (\t) です。 詳細については、「 [フィールド ターミネータと行ターミネータの指定 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)」を参照してください。|  
|**-T**|**bcp** ユーティリティが統合セキュリティを使用した信頼関係接続を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続することを指定します。 **-T** を指定しない場合、正常にログインするには **-U** と **-P** を指定する必要があります。|  
  
 次の例では、Unicode 文字形式のデータを `myTestUniCharData` テーブルから `myTestUniCharData-w.Dat` という名前の新しいデータ ファイルに一括エクスポートします。このデータ ファイルでは、フィールド ターミネータとしてコンマ (`,`) が使用されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows コマンド プロンプトで、次のように入力します。  
  
```  
bcp AdventureWorks2012..myTestUniCharData out C:\myTestUniCharData-w.Dat -w -t, -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-unicode-character-data"></a>BULK INSERT を使用した Unicode 文字データの一括インポート  
 次の例では、`BULK INSERT` を使用して、`myTestUniCharData-w.Dat` データ ファイルのデータを `myTestUniCharData` テーブルにインポートします。 既定以外のフィールド ターミネータ (`,`) は、ステートメントで宣言する必要があります。 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] クエリ エディターで、次のコードを実行します。  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestUniCharData   
   FROM 'C:\myTestUniCharData-w.Dat'   
   WITH (  
      DATAFILETYPE='widechar',  
      FIELDTERMINATOR=','  
   );   
GO  
SELECT Col1,Col2,Col3 FROM myTestUniCharData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **一括インポートまたは一括エクスポートのデータ形式を使用するには**  
  
-   [以前のバージョンの SQL Server からのネイティブ形式データおよび文字形式データのインポート](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>関連項目  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [データ型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Collation and Unicode Support](../collations/collation-and-unicode-support.md)  
  
  
