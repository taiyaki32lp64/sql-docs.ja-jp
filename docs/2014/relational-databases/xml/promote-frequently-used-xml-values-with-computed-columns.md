---
title: 計算列を使用した使用頻度の高い XML 値の昇格 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- promoting properties [XML in SQL Server]
- property promotion [XML in SQL Server]
ms.assetid: f5111896-c2fd-4209-b500-f2baa45489ad
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5b2d167ca9bb2f5a39802bacceb3dd0eb3c96d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68195572"
---
# <a name="promote-frequently-used-xml-values-with-computed-columns"></a>計算列を使用した使用頻度の高い XML 値の昇格
  クエリが主に少数の要素や属性の値に対して行われる場合、対象になる値をリレーショナル列に昇格できます。 XML インスタンス全体を取得する一方で、XML データの一部に対してクエリを実行する場合に昇格が役立ちます。 XML 列に XML インデックスを作成する必要はありません。 代わりに、昇格した列にインデックスを設定できます。 クエリは昇格した列を使用するように記述する必要があります。 クエリ オプティマイザーは、クエリの対象を XML 列から、昇格した列に振り替えないためです。  
  
 昇格した列は、同一のテーブルで計算列にすることができます。また、任意のテーブルでユーザーが管理する独立した列にすることもできます。 これは、各 XML インスタンスから単一の値を昇格するときには十分です。 しかし、複数の値から構成されるプロパティの場合、個々のプロパティ用に個別のテーブルを作成する必要があります。詳細については、次のセクションを参照してください。  
  
## <a name="computed-column-based-on-the-xml-data-type"></a>xml データ型を基にした計算列  
 呼び出すユーザー定義関数を使用して計算列を作成できる`xml`データ型のメソッド。 計算列の型は、XML を含めどの SQL 型でもかまいません。 この例を次に示します。  
  
### <a name="example-computed-column-based-on-the-xml-data-type-method"></a>例: xml データ型のメソッドを基にした計算列  
 書籍の ISBN 番号を取得するユーザー定義関数を作成します。  
  
```  
CREATE FUNCTION udf_get_book_ISBN (@xData xml)  
RETURNS varchar(20)  
BEGIN  
   DECLARE @ISBN   varchar(20)  
   SELECT @ISBN = @xData.value('/book[1]/@ISBN', 'varchar(20)')  
   RETURN @ISBN   
END  
```  
  
 ISBN を保存する計算列をテーブルに追加します。  
  
```  
ALTER TABLE      T  
ADD   ISBN AS dbo.udf_get_book_ISBN(xCol)  
```  
  
 計算列は、通常の方法でインデックスを設定できます。  
  
### <a name="example-queries-on-a-computed-column-based-on-xml-data-type-methods"></a>例: xml データ型のメソッドを基にした計算列へのクエリ  
 ISBN が 0-7356-1588-2 の <`book`> を取得します。  
  
```  
SELECT xCol  
FROM   T  
WHERE  xCol.exist('/book/@ISBN[. = "0-7356-1588-2"]') = 1  
```  
  
 XML 列へのクエリを次のように書き換えると、計算列を使用できます。  
  
```  
SELECT xCol  
FROM   T  
WHERE  ISBN = '0-7356-1588-2'  
```  
  
 返すユーザー定義関数を作成することができます、`xml`データ型とユーザー定義関数を使用して計算列。 ただし、XML 計算列には XML インデックスを作成できません。  
  
## <a name="creating-property-tables"></a>プロパティ テーブルの作成  
 XML データの中から複数の値で構成されるプロパティの一部を 1 つ以上のテーブルに昇格させ、インデックスを作成してクエリの対象をそのテーブルに振り替えることができます。 クエリ ワークロードの大半が少数のプロパティで占められているシナリオが典型的です。 次の操作を実行できます。  
  
-   複数の値から構成されるプロパティを格納するためのテーブルを 1 つ以上作成します。 1 つのプロパティを 1 つのテーブルに保存し、プロパティ テーブルでベース テーブルの主キーを複製すると、ベース テーブルとの逆結合に便利です。  
  
-   プロパティの相対順序を保持する場合、相対順序を保持するための列を別に設ける必要があります。  
  
-   プロパティ テーブルを管理するためのトリガーを XML 列に作成します。 トリガー内では次のいずれかを行うことができます。  
  
    -   使用`xml`データ型のなどメソッド、 **nodes()** と**value()** を挿入およびプロパティ テーブルの行を削除します。  
  
    -   CLR (共通言語ランタイム) でストリーミング テーブル値関数を作成し、プロパティ テーブルの行を挿入および削除します。  
  
    -   主キーを使用してテーブルどうしを結合し、プロパティ テーブルに SQL アクセスを行うクエリ、およびベース テーブルの XML 列に XML アクセスを行うクエリを記述します。  
  
### <a name="example-create-a-property-table"></a>例: プロパティ テーブルの作成  
 たとえば、著者の名 (ファースト ネーム) を昇格させるとします。 共著の場合もあるので、名は複数の値から構成されるプロパティです。 それぞれの名は、プロパティ テーブルの個別の行に保存されます。 逆結合のため、ベース テーブルの主キーをプロパティ テーブルで複製します。  
  
```  
create table tblPropAuthor (propPK int, propAuthor varchar(max))  
```  
  
### <a name="example-create-a-user-defined-function-to-generate-a-rowset-from-an-xml-instance"></a>例: XML インスタンスから行セットを生成するユーザー定義関数の作成  
 次のテーブル値関数 udf_XML2Table は、主キーの値と XML インスタンスを受け取ります。 <`book`> 要素のすべての著者の名を取得し、主キーと名の組み合わせから構成される行セットを返します。  
  
```  
create function udf_XML2Table (@pk int, @xCol xml)  
returns @ret_Table table (propPK int, propAuthor varchar(max))  
with schemabinding  
as  
begin  
      insert into @ret_Table   
      select @pk, nref.value('.', 'varchar(max)')  
      from   @xCol.nodes('/book/author/first-name') R(nref)  
      return  
end  
```  
  
### <a name="example-create-triggers-to-populate-a-property-table"></a>例: プロパティ テーブルにデータを格納するトリガーの作成  
 次の挿入トリガーを使用して、プロパティ テーブルに行を挿入します。  
  
```  
create trigger trg_docs_INS on T for insert  
as  
      declare @wantedXML xml  
      declare @FK int  
      select @wantedXML = xCol from inserted  
      select @FK = PK from inserted  
  
   insert into tblPropAuthor  
   select * from dbo.udf_XML2Table(@FK, @wantedXML)  
```  
  
 次の削除トリガーを使用して、削除する行の主キーの値を基に、プロパティ テーブルから行を削除します。  
  
```  
create trigger trg_docs_DEL on T for delete  
as  
   declare @FK int  
   select @FK = PK from deleted  
   delete tblPropAuthor where propPK = @FK  
```  
  
 次の更新トリガーを使用して、更新する XML インスタンスに対応するプロパティ テーブルの既存の行を削除し、新しい行を挿入します。  
  
```  
create trigger trg_docs_UPD  
on T  
for update  
as  
if update(xCol) or update(pk)  
begin  
      declare @FK int  
      declare @wantedXML xml  
      select @FK = PK from deleted  
      delete tblPropAuthor where propPK = @FK  
  
   select @wantedXML = xCol from inserted  
   select @FK = pk from inserted  
  
   insert into tblPropAuthor   
      select * from dbo.udf_XML2Table(@FK, @wantedXML)  
end  
```  
  
### <a name="example-find-xml-instances-whose-authors-have-the-same-first-name"></a>例: 著者の名が同一の XML インスタンスの検索  
 XML 列に対するクエリも作成できますが、 プロパティ テーブルで名 "David" を検索し、ベース テーブルとの逆結合を実行して XML インスタンスを返すこともできます。 例:  
  
```  
SELECT xCol   
FROM     T JOIN tblPropAuthor ON T.pk = tblPropAuthor.propPK  
WHERE    tblPropAuthor.propAuthor = 'David'  
```  
  
### <a name="example-solution-using-the-clr-streaming-table-valued-function"></a>例: CLR ストリーミング テーブル値関数を使用したソリューション  
 このソリューションは、次の手順で実行します。  
  
1.  CLR クラス SqlReaderBase を定義します。このクラスは ISqlReader を実装し、XML インスタンスにパス式を適用することでストリーミング テーブル値出力を生成します。  
  
2.  CLR クラスを起動するため、アセンブリおよび Transact-SQL ユーザー定義関数を作成します。  
  
3.  ユーザー定義関数を使用して、プロパティ テーブルのメンテナンスに使用する挿入トリガー、更新トリガー、および削除トリガーを定義します。  
  
 まず、ストリーミング CLR 関数を作成します。 `xml`データ型が ADO.NET での SqlXml マネージ クラスとして公開され、サポート、 **CreateReader()** XmlReader を返すメソッド。  
  
> [!NOTE]  
>  このセクションの例のコードでは、XPathDocument および XPathNavigator を使用しています。 この 2 つはすべての XML ドキュメントをメモリに読み込みます。 大きな XML ドキュメントを処理するためにこのサンプルと同様のコードを使用する場合、このコードにはスケーラビリティはありません。 代わりに、メモリの割り当てを少なく抑え、可能な限りストリーミング インターフェイスを使用してください。 パフォーマンスの詳細については、「 [CLR 統合のアーキテクチャ](../../database-engine/dev-guide/architecture-of-clr-integration.md)」を参照してください。  
  
```  
public class c_streaming_xml_tvf {  
   public static ISqlReader streaming_xml_tvf   
(SqlXml xmlDoc, string pathExpression) {  
      return (new TestSqlReaderBase (xmlDoc, pathExpression));  
   }  
}  
  
// Class that implements ISqlReader  
public class TestSqlReaderBase : ISqlReader {  
XPathNodeIterator m_iterator;           
   public SqlChars FirstName;  
// Metadata for current resultset  
private SqlMetaData[] m_rgSqlMetaData;        
  
   public TestSqlReaderBase (SqlXml xmlDoc, string pathExpression) {     
      // Variables for XPath navigation  
      XPathDocument xDoc;  
      XPathNavigator xNav;  
      XPathExpression xPath;  
  
      // Set sql metadata  
      m_rgSqlMetaData = new SqlMetaData[1];  
      m_rgSqlMetaData[0] = new SqlMetaData ("FirstName",    
SqlDbType.NVarChar,50);     
  
      //Set up the Navigator  
      if (!xmlDoc.IsNull)  
          xDoc = new XPathDocument (xmlDoc.CreateReader());  
      else  
          xDoc = new XPathDocument ();  
      xNav = xDoc.CreateNavigator();  
      xPath = xNav.Compile (pathExpression);  
      m_iterator = xNav.Select(xPath);  
   }  
   public bool Read() {  
      bool moreRows = true;  
      if (moreRows = m_iterator.MoveNext())  
         FirstName = new SqlChars (m_iterator.Current.Value);  
      return moreRows;  
   }  
}  
```  
  
 次に、アセンブリ、および CLR 関数 streaming_xml_tvf に対応する [!INCLUDE[tsql](../../includes/tsql-md.md)] ユーザー定義関数 SQL_streaming_xml_tvf (ここには示していません) を作成します。 このユーザー定義関数を使用して、行セットを生成するためのテーブル値関数 CLR_udf_XML2Table を定義します。  
  
```  
create function CLR_udf_XML2Table (@pk int, @xCol xml)  
returns @ret_Table table (FK int, FirstName varchar(max))  
with schemabinding  
as  
begin  
      insert into @ret_Table   
   select @pk, FirstName   
   FROM   SQL_streaming_xml_tvf (@xCol, '/book/author/first-name')  
      return  
end  
```  
  
 最後に、「プロパティ テーブルにデータを格納するトリガーの作成」で示したトリガーを、udf_XML2Table 関数を CLR_udf_XML2Table 関数に置き換えて定義します。 挿入トリガーは次の例のようになります。  
  
```  
create trigger CLR_trg_docs_INS on T for insert  
as  
   declare @wantedXML xml  
   declare @FK int  
   select @wantedXML = xCol from inserted  
   select @FK = PK from inserted  
  
   insert into tblPropAuthor  
      select *  
   from    dbo.CLR_udf_XML2Table(@FK, @wantedXML)  
```  
  
 削除トリガーは CLR を使用しない場合と同じです。 更新トリガーは関数 udf_XML2Table() を CLR_udf_XML2Table() に置き換えます。  
  
## <a name="see-also"></a>関連項目  
 [計算列での XML の使用](use-xml-in-computed-columns.md)  
  
  
