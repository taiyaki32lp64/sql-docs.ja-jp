---
title: 文字形式を使用したデータのインポートまたはエクスポート (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], character
- character formats [SQL Server]
ms.assetid: d925e66a-1a73-43cd-bc06-1cbdf8174a4d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab658be26dc8ccbdd4e760d0b1bc835ace3b2c38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011666"
---
# <a name="use-character-format-to-import-or-export-data-sql-server"></a>文字形式を使用したデータのインポートまたはエクスポート (SQL Server)
  後で別のプログラムで使われるテキスト ファイルにデータを一括エクスポートする場合や、別のプログラムにより生成されたテキスト ファイルからデータを一括インポートする場合は、文字形式の使用をお勧めします。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスと、拡張文字や DBCS 文字を含まない Unicode 文字データを含むデータ ファイル間でデータの一括転送を行う場合は、Unicode 文字形式を使用します。 詳細については、「 [Unicode 文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)」をご覧ください。  
  
 文字形式では、すべての列に文字データ形式が使用されます。 データがスプレッドシートなどの別のプログラムで使用されるとき、または Oracle など別のデータベース ベンダーの製品から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにデータをコピーする必要があるときは、文字形式で情報を格納すると便利です。  
  
## <a name="considerations-for-using-character-format"></a>文字形式の使用に関する注意点  
 文字形式を使用するときは、以下の点を考慮してください。  
  
-   **bcp** ユーティリティは、特に指定しない限り、文字データ フィールド間の区切りにはタブ文字を、レコードの終わりには改行文字を使用します。 別のターミネータの指定方法の詳細については、「[フィールド ターミネータと行ターミネータの指定 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)」を参照してください。  
  
-   既定では、キャラクター モードのデータの一括エクスポートまたは一括インポートを行う前に、次の変換が実行されます。  
  
    |一括操作の方向|変換|  
    |---------------------------------|----------------|  
    |[エクスポート]|データを文字表現に変換します。 明示的に要求された場合は、データが文字の列ごとに要求されたコード ページに変換されます。 コード ページが指定されていない場合は、文字データはクライアント コンピューターの OEM コード ページを使用して変換されます。|  
    |[インポート]|必要に応じて、文字データをネイティブ表現に変換し、クライアントのコード ページから目的の列のコード ページに変換します。|  
  
-   変換中に拡張文字が失われないようにするには、Unicode 文字形式を使用するか、コード ページを指定します。  
  
-   `sql_variant` データが文字形式ファイルに保存される場合は、メタデータなしで保存されます。 各データ値は、暗黙的なデータ変換の規則に従って `char` 形式に変換されます。 `sql_variant` 型の列にインポートされるときは、`char` 型のデータとしてインポートされます。 `sql_variant` 型以外のデータ型の列にインポートされるときは、暗黙の変換を使用して `char` から変換されます。 詳細については、「[データ型の変換 &#40;データベース エンジン&#41;](/sql/t-sql/data-types/data-type-conversion-database-engine)」を参照してください。  
  
-   **Bcp**ユーティリティ エクスポート`money`コンマの区切り記号などの任意の桁区切り記号のされず、小数点後以下 4 桁の文字形式データ ファイルとしての値。 たとえば、値 1,234,567.123456 を含む `money` 型の列は、文字列 1234567.1235 としてデータ ファイルに一括エクスポートされます。  
  
## <a name="command-options-for-character-format"></a>文字形式のコマンド オプション  
 使用してテーブルに文字形式のデータをインポートできます**bcp**、BULK INSERT または INSERT.SELECT \* FROM OPENROWSET(BULK...)。**bcp** コマンドまたは BULK INSERT ステートメントの場合は、コマンド ラインでデータ形式を指定できます。 INSERT ...SELECT * FROM OPENROWSET(BULK...) ステートメントの場合は、フォーマット ファイルでデータ形式を指定する必要があります。  
  
 文字形式は、次のコマンド ライン オプションでサポートされています。  
  
|コマンド|オプション|説明|  
|-------------|------------|-----------------|  
|**bcp**|**-c**|により、 **bcp**ユーティリティが文字データを使用する<sup>。1</sup>|  
|BULK INSERT|DATAFILETYPE **='char'**|データの一括インポート時に文字形式を使用します。|  
  
 <sup>1</sup>文字を読み込めません ( **-c**) の旧バージョンと互換性のある形式にデータを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]クライアントを使用して、 **-v**スイッチします。 詳細については、「 [以前のバージョンの SQL Server からのネイティブ形式データおよび文字形式データのインポート](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)」をご覧ください。  
  
 詳細については、[bcp ユーティリティ](../../tools/bcp-utility.md)、「[BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)」、または「[OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)」を参照してください。  
  
> [!NOTE]  
>  また、フォーマット ファイルでフィールドごとに形式を指定することもできます。 詳細については、「[データのインポートまたはエクスポート用のフォーマット ファイル &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、文字データを **bcp** を使用して一括インポートする方法と、同じデータを bcp INSERT を使用して一括インポートする方法を示しています。  
  
### <a name="sample-table"></a>サンプル テーブル  
 次の例を実行するには、 **dbo** スキーマに基づいて、 **myTestCharData** という名前のテーブルを **AdventureWorks** サンプル データベース内に作成する必要があります。 このテーブルを作成しないと、例を実行できません。 このテーブルを作成するには、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] クエリ エディターで次のコードを実行します。  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestCharData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 このテーブルを作成し、上記のコードにより生成された内容を表示するには、次のステートメントを実行します。  
  
```  
INSERT INTO myTestCharData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestCharData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestCharData  
  
```  
  
### <a name="using-bcp-to-bulk-export-character-data"></a>bcp を使用した文字データの一括エクスポート  
 テーブルからデータ ファイルにデータをエクスポートするには、 **bcp** で **out** オプションと次の修飾子を組み合わせて使用します。  
  
|修飾子|説明|  
|----------------|-----------------|  
|**-c**|文字形式を指定します。|  
|**-t** `,`|コンマ (`,`) をフィールド ターミネータとして指定します。<br /><br /> 注:既定のフィールド ターミネータは、タブ文字 (\t) です。 詳細については、「 [フィールド ターミネータと行ターミネータの指定 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)」を参照してください。|  
|**-T**|**bcp** ユーティリティが統合セキュリティを使用した信頼関係接続を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続することを指定します。 **-T** を指定しない場合、正常にログインするには **-U** と **-P** を指定する必要があります。|  
  
 次の例では、文字形式のデータを `myTestCharData` テーブルから `myTestCharData-c.Dat` という名前の新しいデータ ファイルに一括エクスポートします。このデータ ファイルでは、フィールド ターミネータとしてコンマ (,) が使用されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows コマンド プロンプトで、次のように入力します。  
  
```  
bcp AdventureWorks..myTestCharData out C:\myTestCharData-c.Dat -c -t, -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-character-data"></a>BULK INSERT を使用した文字データの一括インポート  
 次の例では、BULK INSERT を使用して、 `myTestCharData-c.Dat` データ ファイルのデータを `myTestCharData` テーブルにインポートします。 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] クエリ エディターで、次のコードを実行します。  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestCharData   
   FROM 'C:\myTestCharData-c.Dat'   
   WITH (  
      DATAFILETYPE='char',  
      FIELDTERMINATOR=','  
   );   
GO  
SELECT Col1,Col2,Col3 FROM myTestCharData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **一括インポートまたは一括エクスポートのデータ形式を使用するには**  
  
-   [以前のバージョンの SQL Server からのネイティブ形式データおよび文字形式データのインポート](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode 文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [データ型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [以前のバージョンの SQL Server からのネイティブ形式データおよび文字形式データのインポート](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
  
