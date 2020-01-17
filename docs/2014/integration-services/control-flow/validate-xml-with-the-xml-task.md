---
title: XML タスクを使った XML の検証 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- XML validation
- XML, validating
ms.assetid: 224fc025-c21f-4d43-aa9d-5ffac337f9b0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 76d84c3ea8da6d564db01fba3d02ac15a72fffc3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62829599"
---
# <a name="validate-xml-with-the-xml-task"></a>Validate XML with the XML Task
  XML タスクの `ValidationDetails` プロパティを有効にして、XML ドキュメントを検証し、詳細なエラー出力を取得します。  
  
 次のスクリーン ショットは、 **XML タスク エディター** と、XML 検証で詳細なエラー出力を取得するのに必要な設定を示しています。  
  
 ![XML タスク エディターの XML タスク　プロパティ](../media/xmltaskproperties.jpg "XML タスク エディターの XML タスク プロパティ")  
  
 `ValidationDetails` プロパティが利用できるようになる前は、XML タスクによる XML 検証では、true や false のみの結果が返され、エラーやその場所に関する情報は返されませんでした。 次に、設定`ValidationDetails`を true に、出力ファイルに行番号と位置を含むすべてのエラーに関する詳細情報が含まれています。 この情報を使って、XML ドキュメントのエラーを把握、特定、修正できます。  
  
 この XML 検証機能は、大きなサイズの XML ドキュメントや大量のエラーにも、簡単に規模を変更して対応できます。 出力ファイル自体が XML 形式なので、出力に対するクエリの実行と分析が可能です。 たとえば、出力に大量のエラーが含まれている場合、このトピックで説明する方法で [!INCLUDE[tsql](../../../includes/tsql-md.md)] クエリを使用して、エラーをグループ化することができます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) 導入された、`ValidationDetails`プロパティ[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Service Pack 2。 使用可能なプロパティも[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]と SQL Server 2016 でします。  
  
## <a name="sample-output-for-xml-thats-valid"></a>有効な XML のサンプル出力  
 有効な XML ファイルの検証結果が記載されたサンプル出力ファイルを次に示します。  
  
```xml  
  
<root xmlns:ns="https://schemas.microsoft.com/xmltools/2002/xmlvalidation">  
    <metadata>  
        <result>true</result>  
        <errors>0</errors>  
        <warnings>0</warnings>  
        <startTime>2015-05-28T10:27:22.087</startTime>  
        <endTime>2015-05-28T10:29:07.007</endTime>  
        <xmlFile>d:\Temp\TestData.xml</xmlFile>  
        <xsdFile>d:\Temp\TestSchema.xsd</xsdFile>  
    </metadata>  
    <messages />  
</root>  
```  
  
## <a name="sample-output-for-xml-thats-not-valid"></a>無効な XML のサンプル出力  
 少数のエラーのある XML ファイルの検証結果が記載されたサンプル出力ファイルを次に示します。 \<error> 要素のテキストは、読みやすくするために折り返されています。  
  
```xml  
  
<root xmlns:ns="https://schemas.microsoft.com/xmltools/2002/xmlvalidation">  
    <metadata>  
        <result>false</result>  
        <errors>2</errors>  
        <warnings>0</warnings>  
        <startTime>2015-05-28T10:45:09.538</startTime>  
        <endTime>2015-05-28T10:45:09.558</endTime>  
        <xmlFile>C:\Temp\TestData.xml</xmlFile>  
        <xsdFile>C:\Temp\TestSchema.xsd</xsdFile>  
    </metadata>  
    <messages>  
        <error line="5" position="26">The 'ApplicantRole' element is invalid - The value 'wer3' is invalid  
    according to its datatype 'ApplicantRoleType' - The Enumeration constraint failed.</error>  
        <error line="16" position="28">The 'Phone' element is invalid - The value 'we3056666666' is invalid  
     according to its datatype 'phone' - The Pattern constraint failed.</error>  
    </messages>  
</root>  
```  
  
## <a name="analyze-xml-validation-output-with-a-transact-sql-query"></a>XML 検証の出力を Transact-SQL クエリで分析する  
 XML 検証の出力に大量のエラーが含まれている場合、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] クエリを使用して [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]に出力を読み込むことができます。 そのうえで、WHERE、GROUP BY、ORDER BY、JOINなどの T-SQL 言語の機能をフル活用して、エラー一覧を分析できます。  
  
```sql  
DECLARE @xml XML;  
  
SELECT @xml = XmlDoc     
FROM OPENROWSET (BULK N'C:\Temp\XMLValidation_2016-02-212T10-41-00.xml', SINGLE_BLOB) AS Tab(XmlDoc);  
  
-- Query # 1, flat list of errors  
-- convert to relational/rectangular  
;WITH XMLNAMESPACES ('https://schemas.microsoft.com/xmltools/2002/xmlvalidation' AS ns), rs AS  
(  
SELECT col.value('@line','INT') AS line  
     , col.value('@position','INT') AS position  
     , col.value('.','VARCHAR(1024)') AS error  
FROM @XML.nodes('/root/messages/error') AS tab(col)  
)  
SELECT * FROM rs;  
-- WHERE error LIKE '%whatever_string%'  
  
-- Query # 2, count of errors grouped by the error message  
-- convert to relational/rectangular  
;WITH XMLNAMESPACES ('https://schemas.microsoft.com/xmltools/2002/xmlvalidation' AS ns), rs AS  
(  
SELECT col.value('@line','INT') AS line  
     , col.value('@position','INT') AS position  
     , col.value('.','VARCHAR(1024)') AS error  
FROM @XML.nodes('/root/messages/error') AS tab(col)  
)  
SELECT COALESCE(error,'Total # of errors:') AS [error], COUNT(*) AS [counter]  
FROM rs  
GROUP BY GROUPING SETS ((error), ())  
ORDER BY 2 DESC, COALESCE(error, 'Z');  
  
```  
  
 次に示すのは、前に示したテキストの 2 つ目のサンプル クエリの結果を [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で表示した画面です。  
  
 ![Management Studio で XML エラーをグループ化するクエリ](../media/queryforxmlerrors.jpg "Management Studio で XML エラーをグループ化するクエリ")  
  
## <a name="see-also"></a>参照  
 [XML タスク](xml-task.md)   
 [XML タスク エディター ([全般] ページ)](../xml-task-editor-general-page.md)  
  
  
