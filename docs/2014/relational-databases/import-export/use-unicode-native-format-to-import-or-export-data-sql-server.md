---
title: Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- Unicode [SQL Server], bulk importing and exporting
- data formats [SQL Server], Unicode native
ms.assetid: a6213308-f3d5-406e-9029-19d8bb3367f3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b1d115dacc53cb074080931c2ebad88dcaf1c68d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011566"
---
# <a name="use-unicode-native-format-to-import-or-export-data-sql-server"></a>Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート (SQL Server)
  Unicode ネイティブ形式は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール環境間で情報をコピーする必要がある場合に役立ちます。 非文字データに対してネイティブ形式を使用すると、時間を節約でき、文字形式との間でデータ型の不要な変換が行われなくなります。 すべての文字データに対して Unicode 文字形式を使用すると、異なるコード ページを使用している複数のサーバー間でデータを一括転送するときに、拡張文字の損失を防ぐことができます。 Unicode ネイティブ形式のデータ ファイルは、すべての一括インポート方法で読み取ることができます。  
  
 拡張文字や DBCS 文字を含むデータ ファイルを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンス間でデータを一括転送する場合は、Unicode ネイティブ形式を使用することをお勧めします。 非文字データの場合、Unicode ネイティブ形式ではネイティブ (データベース) データ型が使用されます。 `char`、`nchar`、`varchar`、`nvarchar`、`text`、`varchar(max)`、`nvarchar(max)`、`ntext` などの文字データの場合、Unicode ネイティブ形式では Unicode 文字データ形式が使用されます。  
  
 Unicode ネイティブ形式のデータ ファイルに SQLVARIANT として格納される `sql_variant` データは、ネイティブ形式のデータ ファイルに格納される場合と同様に動作します。ただし、`char` と `varchar` の値がそれぞれ `nchar` と `nvarchar` に変換される点を除きます。この場合、影響を受ける列で 2 倍のストレージが必要になります。 元のメタデータは保持され、値はテーブル列に一括インポートされるときに、元の `char` データ型や `varchar` データ型に再び変換されます。  
  
## <a name="command-options-for-unicode-native-format"></a>Unicode ネイティブ形式のコマンド オプション  
 Unicode ネイティブ形式のデータは、**bcp**、BULK INSERT、または INSERT ...SELECT \* FROM OPENROWSET(BULK...)。**bcp** コマンドまたは BULK INSERT ステートメントの場合は、コマンド ラインでデータ形式を指定できます。 INSERT ...SELECT * FROM OPENROWSET(BULK...) ステートメントの場合は、フォーマット ファイルでデータ形式を指定する必要があります。  
  
 Unicode ネイティブ形式は、次のオプションでサポートされています。  
  
|コマンド|オプション|説明|  
|-------------|------------|-----------------|  
|**bcp**|**-N**|により、 **bcp**ネイティブ (データベース) データを使用して Unicode ネイティブ形式を使用するためのユーティリティは、すべての非文字データとすべての文字の Unicode 文字データ形式の型 (`char`、 `nchar`、 `varchar`、`nvarchar`、 `text`、および`ntext`) データ。|  
|BULK INSERT|DATAFILETYPE **='** widenative **'**|データの一括インポート時に Unicode ネイティブ形式を使用します。|  
  
 詳細については、「[bcp ユーティリティ](../../tools/bcp-utility.md)」、「[BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)」、または「[OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)」を参照してください。  
  
> [!NOTE]  
>  また、フォーマット ファイルでフィールドごとに形式を指定することもできます。 詳細については、「[データのインポートまたはエクスポート用のフォーマット ファイル &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、**bcp** を使用してネイティブ データを一括エクスポートする方法と、BULK INSERT を使用して同じデータを一括インポートする方法を説明します。  
  
### <a name="sample-table"></a>サンプル テーブル  
 次の例を実行するには、**dbo** スキーマに基づいて、**myTestUniNativeData** という名前のテーブルを **AdventureWorks** サンプル データベース内に作成する必要があります。 このテーブルを作成しないと、例を実行できません。 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] クエリ エディターで、次のコードを実行します。  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestUniNativeData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 このテーブルを作成し、上記のコードにより生成された内容を表示するには、次のステートメントを実行します。  
  
```  
INSERT INTO myTestUniNativeData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestUniNativeData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestUniNativeData  
  
```  
  
### <a name="using-bcp-to-bulk-export-native-data"></a>bcp を使用したネイティブ データの一括エクスポート  
 テーブルからデータ ファイルにデータをエクスポートするには、 **bcp** で **out** オプションと次の修飾子を組み合わせて使用します。  
  
|修飾子|説明|  
|----------------|-----------------|  
|**-N**|ネイティブ データ型を指定します。|  
|**-T**|**bcp** ユーティリティが統合セキュリティを使用した信頼関係接続を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続することを指定します。 **-T** を指定しない場合、正常にログインするには **-U** と **-P** を指定する必要があります。|  
  
 次の例では、ネイティブ形式のデータを `myTestUniNativeData` テーブルから `myTestUniNativeData-N.Dat` という名前の新しいデータ ファイルに一括エクスポートします。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows コマンド プロンプトで、次のように入力します。  
  
```  
bcp AdventureWorks..myTestUniNativeData out C:\myTestUniNativeData-N.Dat -N -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-native-data"></a>BULK INSERT を使用したネイティブ データの一括インポート  
 次の例では、BULK INSERT を使用して、`myTestUniNativeData-N.Dat` データ ファイルのデータを `myTestUniNativeData` テーブルにインポートします。 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] クエリ エディターで、次のコードを実行します。  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestUniNativeData   
    FROM 'C:\myTestUniNativeData-N.Dat'   
   WITH (DATAFILETYPE='widenative');   
GO  
SELECT Col1,Col2,Col3 FROM myTestUniNativeData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **一括インポートまたは一括エクスポートのデータ形式を使用するには**  
  
-   [以前のバージョンの SQL Server からのネイティブ形式データおよび文字形式データのインポート](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode 文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [データ型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)  
  
  
