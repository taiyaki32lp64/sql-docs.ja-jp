---
title: XML データの読み込む | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XML data [SQL Server], loading
- loading XML data
ms.assetid: d1741e8d-f44e-49ec-9f14-10208b5468a7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb3365195e3a64353fb0cbd45e832cd0206f678e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63241288"
---
# <a name="load-xml-data"></a>XML データの読み込み
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] へは、いくつかの方法で XML データを転送できます。 例 :  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの [n]text 型または image 型の列にデータが含まれている場合、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]を使用してテーブルをインポートできます。 ALTER TABLE ステートメントを使用して列の型を XML に変更します。  
  
-   bcp out を使用して別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースからデータの一括コピーを実行し、bcp in を使用して新しいバージョンのデータベースにそのデータの一括挿入を実行できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのリレーショナル列にデータが含まれている場合、新しいテーブルを作成し、[n]text 型の列や行 ID を保存する主キー列 (任意) を含めます。 クライアント側プログラミングを使用して、FOR XML によりサーバーで生成された XML を取得し、`[n]text` 型の列に書き込みます。 その後で、既に説明した技法により、新しいバージョンのデータベースにデータを転送します。 XML を新しいバージョンのデータベースの XML 列に直接書き込むこともできます。  
  
## <a name="bulk-loading-xml-data"></a>XML データの一括読み込み  
 bcp など、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の一括読み込み機能によって XML データをサーバーに一括で読み込むことができます。 OPENROWSET を使用すると、ファイルから XML 列にデータを読み込むことができます。 この点について、次の例で説明します。  
  
##### <a name="example-loading-xml-from-files"></a>例: ファイルからの XML の読み込み  
 この例では、テーブル T に行を挿入する方法を示します。C:\MyFile\xmlfile.xml から CLOB として XML 列の値を読み込み、整数型の列に値 10 を保存します。  
  
```  
INSERT INTO T  
SELECT 10, xCol  
FROM    (SELECT *      
    FROM OPENROWSET (BULK 'C:\MyFile\xmlfile.xml', SINGLE_CLOB)   
 AS xCol) AS R(xCol)  
```  
  
## <a name="text-encoding"></a>テキスト エンコード  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では XML データを Unicode (UTF-16) で保存します。 サーバーから取得する XML データは UTF-16 エンコードで出力されます。 それ以外のエンコードが必要な場合、取得したデータに必要な変換を行う必要があります。 変換した XML データのエンコードが異なる場合があります。 その場合は、注意してデータを読み込む必要があります。 以下に例を示します。  
  
-   Unicode (UCS-2、UTF-16) のテキスト XML は、問題なく XML 列、変数、またはパラメーターに代入できます。  
  
-   基になるコード ページの都合で Unicode ではなく、かつ暗黙のエンコードの場合、データベースの文字列のコード ページは読み込むコード ポイントと同一か、互換性がある必要があります。 必要であれば COLLATE を使用します。 サーバーにそのようなコード ページが存在しない場合、エンコードを修正する明示的な XML 宣言を追加する必要があります。  
  
-   明示的なエンコードを使用するには、コード ページに連動しない `varbinary()` 型を使用するか、適切なコード ページの文字列型を使用します。 次に、データを XML の列、変数、またはパラメーターに割り当てます。  
  
### <a name="example-explicitly-specifying-an-encoding"></a>例: エンコードの明示的な指定  
 明示的な XML 宣言が行われていない XML ドキュメント vcdoc を `varchar(max)` として保存しているとします。 次のステートメントは、エンコード "iso8859-1" を指定した XML 宣言を追加し、この XML ドキュメントを宣言に連結します。バイト表現を保持するために結果を `varbinary(max)` にキャストし、最終的にその結果を XML にキャストします。 その結果、XML プロセッサで、指定したエンコード "iso8859-1" に従ってデータを解析し、対応する文字列値の UTF-16 表現を生成できます。  
  
```  
SELECT CAST(   
CAST (('<?xml version="1.0" encoding="iso8859-1"?>'+ vcdoc) AS VARBINARY (MAX))   
 AS XML)  
```  
  
### <a name="string-encoding-incompatibilities"></a>文字列エンコードの非互換性  
 XML をコピーし、文字列リテラルとして [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のクエリ エディター ウィンドウに貼り付けると、[N]VARCHAR 文字列エンコードの非互換性の問題が発生する可能性があります。 この問題が発生するかどうかは、XML インスタンスのエンコードによって決まります。 多くの場合、XML 宣言の削除が必要になります。 例 :  
  
```  
<?xml version="1.0" encoding="UTF-8"?>  
  <xsd:schema ...  
```  
  
 続いて、N を指定し、XML インスタンスを Unicode 形式のインスタンスにします。 例 :  
  
```  
-- Assign XML instance to a variable.  
DECLARE @X XML  
SET @X = N'...'  
-- Insert XML instance into an xml type column.  
INSERT INTO T VALUES (N'...')  
-- Create an XML schema collection  
CREATE XML SCHEMA COLLECTION XMLCOLL1 AS N'<xsd:schema ... '  
```  
  
## <a name="see-also"></a>関連項目  
 [XML データ &#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  
