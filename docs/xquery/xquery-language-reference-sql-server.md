---
title: XQuery 言語リファレンス (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
helpviewer_keywords:
- XQuery
- XQuery, about XQuery
- xml data type [SQL Server], XQuery
- XML [SQL Server], XQuery
- queries [XML in SQL Server], XQuery
ms.assetid: 8a69344f-2990-4357-8160-cb26aac95b91
author: rothja
ms.author: jroth
ms.openlocfilehash: 87edbeaac26ca1c332efe981901cbf0bc57fed30
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945967"
---
# <a name="xquery-language-reference-sql-server"></a>XQuery 言語リファレンス (SQL Server)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../includes/tsql-md.md)] クエリに使用される XQuery 言語のサブセットをサポート、 **xml**データ型。 この実装は、2004 年 7 月に公開された XQuery のワーキング ドラフトに従っています。 この言語は W3C (World Wide Web Consortium) によって開発が進められており、マイクロソフトをはじめとする主要なすべてのデータベース ベンダーが参加しています。 W3C 仕様は W3C 勧告になる前に改訂されることがあるので、この実装は最終的な勧告とは異なる可能性があります。 このトピックでは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] でサポートされる XQuery サブセットのセマンティクスと構文について概説します。  
  
 詳細については、次を参照してください。、 [W3C XQuery 1.0 Language Specification](https://go.microsoft.com/fwlink/?LinkId=48846)します。  
  
 XQuery は構造化または半構造化された XML データに対するクエリ実行できる言語です。 **Xml**データ型のサポートされている、[!INCLUDE[ssDE](../includes/ssde-md.md)]ドキュメントをデータベースに格納されているし、XQuery を使用してクエリを実行します。  
  
 XQuery は既存の XPath クエリ言語に基づいており、優れた反復処理や結果の並べ替え、必要な XML を構築する機能を実現するためのサポートが追加されています。 XQuery は XQuery データ モデルで動作します。 これは XML ドキュメントおよび XQuery の結果を抽象化したモデルで、XQuery の結果は型指定することも、型指定しないこともできます。 型情報は W3C XML Schema 言語によって提供される型に基づきます。 型指定情報を使用できない場合は、XQuery によりデータが型指定されていないものとして処理されます。 この処理方法は、XPath Version 1.0 で XML が処理される方法と同様です。  
  
 変数またはの列に格納されている XML インスタンスを照会する**xml**種類を使用する、 [xml データ型メソッド](../t-sql/xml/xml-data-type-methods.md)します。 変数を宣言する例: **xml**を入力しを使用してクエリを実行、 **query()** のメソッド、 **xml**データ型。  
  
```sql
DECLARE @x xml  
SET @x = '<ROOT><a>111</a></ROOT>'  
SELECT @x.query('/ROOT/a')  
```  
  
 次の例では、クエリがの Instructions 列に対して指定された**xml** AdventureWorks データベースの ProductModel テーブルの型。  
  
```sql
SELECT Instructions.query('declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";           
    /AWMI:root/AWMI:Location[@LocationID=10]  
') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 XQuery には、名前空間の宣言が含まれています。 `declare namespace``AWMI=...`、およびクエリ式、`/AWMI:root/AWMI:Location[@LocationID=10]`します。  
  
 Instructions 列に対して XQuery を指定することに注意してください。 **xml**型。 [Query() メソッド](../t-sql/xml/query-method-xml-data-type.md)xml データの型は、XQuery を指定して使用します。  
  
 次の表は、[!INCLUDE[ssDE](../includes/ssde-md.md)]での XQuery の実装を理解する際に役立つ関連トピックを示しています。  
  
|トピック|説明|  
|-----------|-----------------|  
|[XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)|サポートについて説明します、 **xml**のデータ型の[!INCLUDE[ssDE](../includes/ssde-md.md)]とメソッドのこのデータ型に対して使用できます。 **Xml**データ入力フォームの入力の XQuery データ モデルの XQuery 式が実行されます。|  
|[XML スキーマ コレクション &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)|データベースに格納されている XML インスタンスを型指定する方法について説明します。 つまり、XML スキーマ コレクションを関連付けることができます、 **xml**型の列。 この列に格納されているすべてのインスタンスは、コレクションのスキーマに対して検証と型指定が行われます。また、これらのインスタンスにより、XQuery の型情報が提供されます。|  
|||  
  
> [!NOTE]  
>  このセクションの構成は、W3C (World Wide Web Consortium) XQuery ワーキング ドラフト仕様に基づいています。 このセクションで提供する図の一部は、その仕様から引用したものです。 ここでは、Microsoft XQuery の実装と W3C 仕様を比較し、Microsoft XQuery と W3C がどのように異なるかを説明し、サポートしていない W3C 機能を示します。 W3C の仕様は[ http://www.w3.org/TR/2004/WD-xquery-20040723](https://go.microsoft.com/fwlink/?LinkId=48846)します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[XQuery の基礎](../xquery/xquery-basics.md)|XQuery の概念の基本的な概要について説明し、式の評価 (静的コンテキストと動的コンテキスト)、アトミック化、有効なブール値、XQuery 型システム、シーケンス型の照合、およびエラー処理についても説明します。|  
|[XQuery 式](../xquery/xquery-expressions.md)|XQuery 原始式、パス式、シーケンス式、算術式、比較式、論理式、XQuery の構築、FLWOR 式、条件式、量化式、およびシーケンス型のさまざまな式について説明します。|  
|[モジュールとプロローグ&#40;XQuery&#41;](../xquery/modules-and-prologs-xquery.md)|XQuery プロローグについて説明します。|  
|[xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)|サポートされている XQuery 関数の一覧について説明します。|  
|[xml データ型に対する XQuery の演算子](../xquery/xquery-operators-against-the-xml-data-type.md)|サポートされている XQuery 演算子について説明します。|  
|[xml データ型に対する XQuery のその他のサンプル](../xquery/additional-sample-xqueries-against-the-xml-data-type.md)|XQuery の追加サンプルを提供します。|  
  
## <a name="see-also"></a>参照  
 [XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XML スキーマ コレクション &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [XML ドキュメントの一括インポートと一括エクスポートの例 &#40;SQL Server&#41;](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
  
