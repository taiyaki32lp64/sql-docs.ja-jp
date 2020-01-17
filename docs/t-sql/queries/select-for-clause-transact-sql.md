---
title: FOR 句 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FOR
- FOR CLAUSE
- FOR_TSQL
- FOR_CLAUSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- XML option [SQL Server]
- BROWSE option
- FOR clause [Transact-SQL]
ms.assetid: 08a6f084-8f73-4f2a-bae4-3c7513dc99b9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ad3852f0bb935371fd141cc4ceb98f90c7aa9c19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904354"
---
# <a name="select---for-clause-transact-sql"></a>SELECT - FOR 句 (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

FOR 句を使用し、クエリ結果に次のいずれかのオプションを指定します。
  
-   **[FOR BROWSE]** を指定し、ブラウズ モード カーソルでクエリ結果を表示している間、更新を許可します。  
  
-   **[FOR XML]** を指定し、XML としてクエリ結果を書式設定します。  
  
-   **[FOR JSON]** を指定し、JSON としてクエリ結果を書式設定します。  

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```
[ FOR { BROWSE | <XML> | <JSON>} ]  
  
<XML> ::=  
XML   
{   
    { RAW [ ( 'ElementName' ) ] | AUTO }   
    [   
        <CommonDirectivesForXML>   
        [ , { XMLDATA | XMLSCHEMA [ ( 'TargetNameSpaceURI' ) ] } ]   
        [ , ELEMENTS [ XSINIL | ABSENT ]   
    ]  
  | EXPLICIT   
    [   
        <CommonDirectivesForXML>   
        [ , XMLDATA ]   
    ]  
  | PATH [ ( 'ElementName' ) ]   
    [  
        <CommonDirectivesForXML>   
        [ , ELEMENTS [ XSINIL | ABSENT ] ]  
    ]  
}   
  
<CommonDirectivesForXML> ::=   
[ , BINARY BASE64 ]  
[ , TYPE ]  
[ , ROOT [ ( 'RootName' ) ] ]  
  
<JSON> ::=  
JSON   
{   
    { AUTO | PATH }   
    [   
        [ , ROOT [ ( 'RootName' ) ] ]  
        [ , INCLUDE_NULL_VALUES ]  
        [ , WITHOUT_ARRAY_WRAPPER ]  
    ]  
  
}
```
  
## <a name="for-browse"></a>FOR BROWSE

 BROWSE  
 DB-Library ブラウズ モード カーソルでデータを表示しているときに、更新が許可されます。 テーブルに **timestamp** 列が含まれる場合、テーブルに一意なインデックスがある場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に送られる SELECT ステートメントの最後に FOR BROWSE オプションがある場合、アプリケーションの中でテーブルを参照できます。  
  
> [!NOTE]
> \<lock_hint> HOLDLOCK は、FOR BROWSE オプションを含む SELECT ステートメントでは使用できません。
  
 FOR BROWSE は、UNION 演算子によって結合された SELECT ステートメントでは使えません。  
  
> [!NOTE]
> テーブルの一意なインデックス キー列が NULL 値を許容し、かつそのテーブルが外部結合の内部にある場合、そのインデックスはブラウズ モードではサポートされません。  
  
 ブラウズ モードを使用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルの行をスキャンし、テーブルのデータを 1 回に 1 行ずつ更新できます。 アプリケーションのブラウズ モードで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルにアクセスするには、次の 2 つのオプションのいずれかを使用する必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルのデータにアクセスするために使用する SELECT ステートメントは **FOR BROWSE** キーワードで終了する必要があります。 **FOR BROWSE** オプションをオンにしてブラウズ モードを使用すると、一時テーブルが作成されます。  
  
-   **NO_BROWSETABLE** オプションを使用してブラウズ モードをオンにするには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行する必要があります。  
  
    ```sql
    SET NO_BROWSETABLE ON  
    ```  
  
     **NO_BROWSETABLE** オプションをオンにすると、すべての SELECT ステートメントは **FOR BROWSE** オプションがステートメントに追加されたかのように動作します。 ただし、**NO_BROWSETABLE** オプションでは、**FOR BROWSE** オプションが通常結果をアプリケーションに送信する際に使用する一時テーブルが作成されません。  
  
 外部結合ステートメントが関与する SELECT クエリを使用してブラウズ モードで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルのデータにアクセスしようとしたときに、外部結合ステートメントの内部のテーブルに一意のインデックスが定義されている場合、この一意のインデックスはブラウズ モードでサポートされません。 ブラウズ モードで一意のインデックスがサポートされるのは、すべての一意のインデックス キー列が NULL 値を使用できる場合のみです。 次の条件に当てはまる場合は、ブラウズ モードで一意のインデックスがサポートされません。  
  
-   外部結合ステートメントを含む SELECT クエリを使用して、ブラウズ モードで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルのデータにアクセスしようとした場合。  
  
-   外部結合ステートメントの内部に存在するテーブルに一意のインデックスが定義されている場合。  
  
 ブラウズ モードでこの動作を再現するには、以下の手順を行います。  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で、SampleDB という名前のデータベースを作成します。  
  
2.  SampleDB データベースに tleft テーブルと tright テーブルを作成し、両方に c1 という単一列が含まれるようにします。 tleft テーブルの c1 列に一意のインデックスを定義し、この列が NULL 値を許容するように設定します。 このためには、適切なクエリ ウィンドウで次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行します。  
  
    ```sql
    CREATE TABLE tleft(c1 INT NULL UNIQUE) ;  
    GO   
    CREATE TABLE tright(c1 INT NULL) ;  
    GO  
    ```  
  
3.  tleft テーブルと tright テーブルに複数の値を挿入します。 tleft テーブルに NULL 値を挿入します。 このためには、クエリ ウィンドウで次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行します。  
  
    ```sql
    INSERT INTO tleft VALUES(2) ;  
    INSERT INTO tleft VALUES(NULL) ;  
    INSERT INTO tright VALUES(1) ;  
    INSERT INTO tright VALUES(3) ;  
    INSERT INTO tright VALUES(NULL) ;  
    GO  
    ```  
  
4.  **NO_BROWSETABLE** オプションをオンにします。 このためには、クエリ ウィンドウで次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行します。  
  
    ```sql
    SET NO_BROWSETABLE ON ;  
    GO  
    ```  
  
5.  SELECT クエリで外部結合ステートメントを使用して、tleft テーブルと tright テーブルのデータにアクセスします。 tleft テーブルが外部結合ステートメントの内部に存在することを確認します。 このためには、クエリ ウィンドウで次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行します。  
  
    ```sql
    SELECT tleft.c1   
    FROM tleft   
    RIGHT JOIN tright   
    ON tleft.c1 = tright.c1   
    WHERE tright.c1 <> 2 ;
    ```  
  
     [結果] ペインに、次の出力が表示されます。  
  
     c1  
  
     ---\-  
  
     NULL  
  
     NULL  
  
 ブラウズ モードで SELECT クエリを実行してテーブルにアクセスすると、右外部結合ステートメントの定義に従い、SELECT クエリの結果セットに tleft テーブルの c1 列の NULL 値が 2 つ格納されます。 したがって、結果セットではテーブルの NULL 値、および右外部結合ステートメントによって提供された NULL 値を区別できません。 結果セットの NULL 値を無視しなければならない場合、正しくない結果が返されることがあります。  
  
> [!NOTE]
> 一意のインデックスに含まれる列で NULL 値を使用できない場合は、結果セットの NULL 値がすべて右外部結合ステートメントによって提供されます。  
  
## <a name="for-xml"></a>FOR XML

 XML  
 クエリの結果を XML ドキュメントとして返します。 XML モードとして、RAW、AUTO、EXPLICIT のいずれか 1 つを指定する必要があります。 XML データと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の詳細については、「[FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)」を参照してください。  
  
 RAW [ **('** _ElementName_ **')** ]  
 クエリの結果を取得し、結果セット内の各行を、要素タグとして汎用識別子 \<row /> が指定されている XML 要素に変換します。 必要に応じて、その行要素に名前を指定することもできます。 結果の XML 出力では、指定した *ElementName* が、行ごとに生成される行要素として使用されます。 詳細については、「 [FOR XML での RAW モードの使用](../../relational-databases/xml/use-raw-mode-with-for-xml.md)」を参照してください。
  
 AUTO  
 クエリの結果を単純な入れ子の XML ツリーで返します。 FROM 句に含まれる各テーブルは、そのうち少なくとも 1 つの列が SELECT 句の一覧に示され、XML 要素として表されます。 SELECT 句に一覧されている列は、該当する要素属性にマップされます。 詳細については、「 [FOR XML での AUTO モードの使用](../../relational-databases/xml/use-auto-mode-with-for-xml.md)」を参照してください。  
  
 EXPLICIT  
 結果として得られる XML ツリーの形状を明示的に定義することを指定します。 このモードを使用する場合は、目的の入れ子に関する追加の情報を明示的に指定できるように、クエリを特別な方法で記述する必要があります。 詳細については、「 [FOR XML での EXPLICIT モードの使用](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)」を参照してください。  
  
 XMLDATA  
 インライン XDR スキーマを返します。ただし、結果にルート要素は追加されません。 XMLDATA を指定すると、XDR スキーマはドキュメントに追加されます。  
  
> [!IMPORTANT]
> XMLDATA ディレクティブは**非推奨**です。 RAW モードと AUTO モードの場合は、XSD 世代を使用してください。 EXPLICIT モードでは、XMLDATA ディレクティブに代わる機能はありません。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  

_不要な改行を非表示にする:_ SQL Server Management Studio (SSMS) を使用し、FOR XML 句を使用するクエリを発行することがあります。 大量の XML が返され、1 つのグリッド セルに表示されることがあります。 XML 文字列は、1 つの SSMS グリッド セルで 1 行に保持できる長さを超えることがあります。 このような場合、SSMS では、XML 文字列全体の長いセグメントの間に改行文字が挿入されることがあります。 行をまたいで分割するべきではない部分文字列の真ん中でそのような改行が発生することがあります。 キャスト AS XMLDATA を使用することで、改行を防ぐことができます。 FOR JSON PATH を使用するときもこの解決策を適用できます。 この手法についてはスタック オーバーフローで論じられています。また、次の Transact-SQL サンプル SELECT ステートメントで確認できます。

- [Using SQL Server FOR XML:Convert Result Datatype to Text/varchar/string whatever?](https://stackoverflow.com/questions/5655332/using-sql-server-for-xml-convert-result-datatype-to-text-varchar-string-whate/5658758#5658758) (SQL Server の FOR XML を使用する: Result データ型をテキスト/可変文字列/文字列に変換する)

    ```sql
    SELECT CAST(
        (SELECT column1, column2
            FROM my_table
            FOR XML PATH('')
        )
            AS VARCHAR(MAX)
    ) AS XMLDATA ;
    ```

<!-- The preceding Stack Overflow example is per MicrosoftDocs/sql-docs Issue 1501.  2019-01-06 -->

 XMLSCHEMA [ **('** _TargetNameSpaceURI_ **')** ]  
 インライン XSD スキーマを返します。 このディレクティブを指定する場合は、必要に応じて、対象名前空間の URI を指定することもできます。指定した場合は、スキーマにある指定した名前空間が返されます。 詳細については、「 [Generate an Inline XSD Schema](../../relational-databases/xml/generate-an-inline-xsd-schema.md)」を参照してください。  
  
 ELEMENTS  
 列を副要素として返します。 指定していない場合は、XML 属性にマップされます。 このオプションは、RAW、AUTO、および PATH モードでのみサポートされます。 詳細については、「 [FOR XML での RAW モードの使用](../../relational-databases/xml/use-raw-mode-with-for-xml.md)」を参照してください。  
  
 XSINIL  
 列の値が NULL の場合、**xsi:nil** 属性が **True** に設定されている要素を作成します。 このオプションは、ELEMENTS ディレクティブでのみ指定できます。 詳細については、以下をご覧ください。

- [XSINIL パラメーターを使用した NULL 値に対する要素の生成](../../relational-databases/xml/generate-elements-for-null-values-with-the-xsinil-parameter.md)。
- [SELECT ステートメントでの FOR XML](../../relational-databases/xml/for-xml-sql-server.md)
  
 ABSENT  
 列の値が NULL の場合、対応する XML 要素を XML 結果に追加しません。 このオプションは、ELEMENTS でのみ指定してください。  
  
 PATH [ **('** _ElementName_ **')** ]  
 結果セットの各行に対して \<row> 要素ラッパーを生成します。 必要に応じて、\<row> 要素ラッパーに要素名を指定することもできます。 FOR XML PATH ( **''** ) ) などの空文字列を指定すると、ラッパー要素は生成されません。 EXPLICIT ディレクティブを使用するよりも、PATH を使用した方が、クエリが単純になる場合があります。 詳細については、「 [FOR XML での PATH モードの使用](../../relational-databases/xml/use-path-mode-with-for-xml.md)」を参照してください。  
  
 BINARY BASE64  
 クエリは、バイナリ データをバイナリ ベース 64 エンコード形式で返します。 RAW モードおよび EXPLICIT モードでバイナリ データを取得する場合は、このオプションを指定する必要があります。 AUTO モードの場合は、これは既定値です。  
  
 TYPE  
 クエリが結果を **xml** 型で返すことを指定します。 詳細については、「 [FOR XML クエリの TYPE ディレクティブ](../../relational-databases/xml/type-directive-in-for-xml-queries.md)」を参照してください。  
  
 ROOT [ **('** _RootName_ **')** ]  
 単一のトップレベル要素を、結果として生成される XML に追加します。 必要に応じて、生成するルート要素名を指定することもできます。 オプションのルート名を指定しない場合は、既定の \<root> 要素が追加されます。  
  
 詳細については、「[FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)」を参照してください。  
  
 **FOR XML の例**  
  
 次の例では、`FOR XML AUTO` を `TYPE` オプションおよび `XMLSCHEMA` オプションと共に指定しています。 `TYPE` オプションを指定しているため、結果セットはクライアントに **xml** 型として返されます。 `XMLSCHEMA` オプションは、返される XML データにインライン XSD スキーマが含まれることを指定し、`ELEMENTS` オプションは、結果の XML が要素中心であることを指定します。  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.BusinessEntityID, FirstName, LastName, PhoneNumber AS Phone  
FROM Person.Person AS p  
JOIN Person.PersonPhone AS pph ON p.BusinessEntityID  = pph.BusinessEntityID  
WHERE LastName LIKE 'G%'  
ORDER BY LastName, FirstName   
FOR XML AUTO, TYPE, XMLSCHEMA, ELEMENTS XSINIL;  
```  
  
## <a name="for-json"></a>JSON の

 JSON  
 FOR JSON を指定し、JSON テキストとして書式設定されたクエリ結果を返します。 JSON モードとして自動またはパスも指定する必要があります。 **FOR JSON** 句の詳細については、「[FOR JSON を使用してクエリ結果を JSON として書式設定する &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)」を参照してください。  
  
 AUTO  
 **FOR JSON AUTO** を指定すると、  
            **SELECT** ステートメントの構造に基づいて JSON 出力を自動的に書式設定します。 詳細と例については、「[AUTO モードで自動的に JSON 出力を書式設定する &#40;SQL Server&#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md)」を参照してください。  
  
 PATH  
 JSON 出力の書式設定を   
            **FOR JSON PATH** を指定して完全制御します。 **PATH** モードでは、ラッパー オブジェクトを作成し、複雑なプロパティを入れ子にすることができます。 詳細と例については、「[PATH モードで入れ子になった JSON 出力を書式設定する &#40;SQL Server&#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md)」を参照してください。  
  
 INCLUDE_NULL_VALUES  
 **INCLUDE_NULL_VALUES** オプションと **FOR JSON** 句を指定し、JSON 出力に NULL 値を含めます。 このオプションを指定しない場合、出力では、クエリ結果の NULL 値に対する JSON のプロパティは含まれません。 詳細については、「[INCLUDE_NULL_VALUES オプションを使用して JSON の出力に Null 値を含める &#40;SQL Server&#41;](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md)」を参照してください。  
  
 ROOT [ **('** _RootName_ **')** ]  
 **ROOT** オプションと **FOR JSON** 句を指定し、最上位要素を 1 つ JSON 出力に追加します。 指定しない場合、 **ROOT** オプションでは、JSON の出力はルート要素がないです。 詳細と例については、「[ROOT オプションを使用して JSON 出力にルート ノードを追加する &#40;SQL Server&#41;](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md)」を参照してください。  
  
 WITHOUT_ARRAY_WRAPPER  
 **WITHOUT_ARRAY_WRAPPER** オプションと **FOR JSON** 句を指定すると、JSON 出力を囲んでいる角かっこが既定で削除されます。 このオプションを指定しないと、JSON 出力が角かっこで囲まれます。 **WITHOUT_ARRAY_WRAPPER** オプションを使用すると、単一の JSON オブジェクトを出力として生成できます。  詳細については、「 [WITHOUT_ARRAY_WRAPPER オプションを使用して JSON 出力から角かっこを削除する &#40;SQL Server&#41;](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md)。  
  
 詳細については、「[FOR JSON を使用してクエリ結果を JSON として書式設定する &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照

 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)

