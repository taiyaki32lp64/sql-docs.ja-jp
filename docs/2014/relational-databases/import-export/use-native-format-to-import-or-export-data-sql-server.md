---
title: ネイティブ形式を使用したデータのインポートまたはエクスポート (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- native data format [SQL Server]
- data formats [SQL Server], native
ms.assetid: eb279b2f-0f1f-428f-9b8f-2a7fc495b79f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a2e91899172dfc6d640df0c33c77e32de3c1c21c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011657"
---
# <a name="use-native-format-to-import-or-export-data-sql-server"></a>ネイティブ形式を使用したデータのインポートまたはエクスポート (SQL Server)
  ネイティブ形式は、拡張文字や 2 バイト文字セット (DBCS) の文字を含まないデータ ファイルを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンス間でデータを一括転送する場合に推奨します。  
  
> [!NOTE]  
>  拡張文字や DBCS 文字を含んだデータ ファイルを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンス間でデータを一括転送するには、Unicode ネイティブ形式を使用する必要があります。 詳細については、「 [Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)」をご覧ください。  
  
 ネイティブ形式ではデータベースのネイティブ データ型が維持されます。 ネイティブ形式は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブル間でデータを高速に転送できるようにデザインされています。 フォーマット ファイルを使用する場合は、転送元と転送先のテーブルは同じである必要はありません。 データ転送は、次の 2 つの手順で行われます。  
  
1.  転送元テーブルからデータ ファイルへのデータの一括エクスポート  
  
2.  データ ファイルから転送先テーブルへのデータの一括インポート  
  
 同一のテーブル間でネイティブ形式を使用すると、文字形式との間でデータ型の不必要な変換を防ぐことができ、時間と領域を節約できます。 ただし、最適な転送速度を実現するために、データの形式設定に関するチェックはほとんど行われません。 読み込まれたデータに関する問題を回避するには、次の制限事項の一覧を参照してください。  
  
## <a name="restrictions"></a>制限  
 データをネイティブ形式で正常にインポートするには、次の条件を満たすようにします。  
  
-   データ ファイルがネイティブ形式です。  
  
-   インポート先のテーブルは、(正しい列数、データ型、長さ、NULL 状態などが含まれた) データ ファイルと互換性を持つ必要があります。または、フォーマット ファイルを使用して、各フィールドを対応する各列にマップする必要があります。  
  
    > [!NOTE]  
    >  インポート先のテーブルと一致しないファイルからデータをインポートすると、インポート操作が成功する場合もありますが、多くの場合、インポート先のテーブルに挿入されるデータ値が不適切な値になります。 これは、インポート元のファイルのデータが、インポート先のテーブルの形式を使用して解釈されるためです。 そのため、インポート先のテーブルと一致しない場合には、不適切な値が挿入されることになります。 ただし、このような不一致が原因で、データベース内で論理的または物理的に不一致が発生することはありません。  
  
     フォーマット ファイルの使用方法については、「[データのインポートまたはエクスポート用のフォーマット ファイル &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)」を参照してください。  
  
 インポートが正常な場合、インポート先のテーブルは破損しません。  
  
## <a name="how-bcp-handles-data-in-native-format"></a>bcp によるネイティブ形式でのデータ処理のしくみ  
 ここでは、**bcp** ユーティリティによるネイティブ形式でのデータのエクスポートとインポートのしくみについて、特別な考慮事項を説明します。  
  
-   非文字データ  
  
     bcp ユーティリティでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部バイナリ データ形式を使用して、非文字データをテーブルからデータ ファイルに書き込みます。  
  
-   `char` データまたは `varchar` データ  
  
     それぞれの先頭に`char`または`varchar`フィールド、 **bcp**プレフィックスの長さを追加します。  
  
    > [!IMPORTANT]  
    >  ネイティブ モードを使用すると、**bcp** ユーティリティは、既定では、文字をデータ ファイルにコピーする前に、それらの文字を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 文字から OEM 文字に変換します。 **bcp** ユーティリティでは、データ ファイルの文字を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに一括インポートする前に、それらの文字を ANSI 文字に変換します。 このような変換が行われている間、拡張文字のデータが失われる場合があります。 拡張文字については、Unicode ネイティブ形式を使用するか、コード ページを指定します。  
  
-   `sql_variant` データ  
  
     `sql_variant` データが SQLVARIANT としてネイティブ形式のデータ ファイルに格納されている場合、そのデータのすべての特性が保持されます。 各データ値のデータ型を記録するメタデータが、そのデータ値と一緒に格納されます。 このメタデータを使用して、インポート先の `sql_variant` 列に同じデータ型でデータ値を再作成します。  
  
     インポート先の列のデータ型が `sql_variant` でない場合、各データ値は、暗黙的なデータ変換の通常の規則に従ってインポート先の列のデータ型に変換されます。 データ変換中にエラーが発生すると、現在のバッチがロールバックされます。 `char` 列間で転送される `varchar` 値と `sql_variant` 値で、コード ページの変換問題が生じている可能性があります。  
  
     詳細については、「[データ型の変換 &#40;データベース エンジン&#41;](/sql/t-sql/data-types/data-type-conversion-database-engine)」を参照してください。  
  
## <a name="command-options-for-native-format"></a>ネイティブ形式用のコマンド オプション  
 ネイティブ形式のデータは、**bcp**、BULK INSERT、または INSERT ...SELECT \* FROM OPENROWSET(BULK...)。**bcp** コマンドまたは BULK INSERT ステートメントの場合は、コマンド ラインでデータ形式を指定できます。 INSERT ...SELECT * FROM OPENROWSET(BULK...) ステートメントの場合は、フォーマット ファイルでデータ形式を指定する必要があります。  
  
 ネイティブ形式は、次のコマンド ライン オプションでサポートされています。  
  
|コマンド|オプション|説明|  
|-------------|------------|-----------------|  
|**bcp**|**-n**|により、 **bcp**データのネイティブ データ型を使用するためのユーティリティ<sup>。1</sup>|  
|BULK INSERT|DATAFILETYPE **='** native **'**|ネイティブ データ型またはワイド ネイティブ データ型のデータが使用されます。 フォーマット ファイルでデータ型を指定している場合、DATAFILETYPE は必要ありません。|  
  
 <sup>1</sup>ネイティブ読み込めません (**-n**) の旧バージョンと互換性のある形式にデータを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]クライアントを使用して、 **-v**スイッチします。 詳細については、「 [以前のバージョンの SQL Server からのネイティブ形式データおよび文字形式データのインポート](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)」をご覧ください。  
  
 詳細については、[bcp ユーティリティ](../../tools/bcp-utility.md)、「[BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)」、または「[OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)」を参照してください。  
  
> [!NOTE]  
>  また、フォーマット ファイルでフィールドごとに形式を指定することもできます。 詳細については、「[データのインポートまたはエクスポート用のフォーマット ファイル &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、**bcp** を使用してネイティブ データを一括エクスポートする方法と、BULK INSERT を使用して同じデータを一括インポートする方法を説明します。  
  
### <a name="sample-table"></a>サンプル テーブル  
 次の例を実行するには、**dbo** スキーマに基づいて、**myTestNativeData** という名前のテーブルを **AdventureWorks** サンプル データベース内に作成する必要があります。 このテーブルを作成しないと、例を実行できません。 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] クエリ エディターで、次のコードを実行します。  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestNativeData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 このテーブルを作成し、上記のコードにより生成された内容を表示するには、次のステートメントを実行します。  
  
```  
INSERT INTO myTestNativeData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestNativeData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestNativeData  
  
```  
  
### <a name="using-bcp-to-bulk-export-native-data"></a>bcp を使用したネイティブ データの一括エクスポート  
 テーブルからデータ ファイルにデータをエクスポートするには、 **bcp** で **out** オプションと次の修飾子を組み合わせて使用します。  
  
|修飾子|説明|  
|----------------|-----------------|  
|**-n**|ネイティブ データ型を指定します。|  
|**-T**|**bcp** ユーティリティが統合セキュリティを使用した信頼関係接続を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続することを指定します。 **-T** を指定しない場合、正常にログインするには **-U** と **-P** を指定する必要があります。|  
  
 次の例では、ネイティブ形式のデータを `myTestNativeData` テーブルから `myTestNativeData-n.Dat` という名前の新しいデータ ファイルに一括エクスポートします。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows コマンド プロンプトで、次のように入力します。  
  
```  
bcp AdventureWorks..myTestNativeData out C:\myTestNativeData-n.Dat -n -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-native-data"></a>BULK INSERT を使用したネイティブ データの一括インポート  
 次の例では、BULK INSERT を使用して、`myTestNativeData-n.Dat` データ ファイルのデータを `myTestNativeData` テーブルにインポートします。 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] クエリ エディターで、次のコードを実行します。  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestNativeData   
    FROM 'C:\myTestNativeData-n.Dat'   
   WITH (DATAFILETYPE='native');   
GO  
SELECT Col1,Col2,Col3 FROM myTestNativeData  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **一括インポートまたは一括エクスポートのデータ形式を使用するには**  
  
-   [以前のバージョンの SQL Server からのネイティブ形式データおよび文字形式データのインポート](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode 文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>関連項目  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [データ型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [sql_variant &#40;Transact-SQL&#41;](/sql/t-sql/data-types/sql-variant-transact-sql)   
 [以前のバージョンの SQL Server からのネイティブ形式データおよび文字形式データのインポート](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
  
