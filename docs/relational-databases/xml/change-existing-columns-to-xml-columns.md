---
title: 既存の列を XML 列に変更する方法 | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- tables [XML]
ms.assetid: 0d951424-9862-41fe-bd46-127f1c059bcb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 605911ebe60c7467db2792737426cc98ce67b52d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113132"
---
# <a name="change-existing-columns-to-xml-columns"></a>既存の列を XML 列に変更する方法

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

**xml** データ型は ALTER TABLE ステートメントでサポートされています。 たとえば、文字列型の列を **xml** データ型に変更できます。 このような場合、列に格納されるドキュメントは正しい形式でなければなりません。 また、列の型を文字列から型指定された xml に変更する場合、列内のドキュメントは指定した XSD スキーマに対して検証されます。  
  
```sql
CREATE TABLE T (Col1 int primary key, Col2 nvarchar(max));
GO  
INSERT INTO T   
  VALUES (1, '<Root><Product ProductID="1"/></Root>');
GO  
ALTER TABLE T   
  ALTER COLUMN Col2 xml;
```  
  
`xml` 型の列は、型指定されていない XML から型指定された XML に変更できます。 例:  
  
```sql
CREATE TABLE T (Col1 int primary key, Col2 xml);
GO  
INSERT INTO T   
  values (1, '<p1:ProductDescription ProductModelID="1"   
xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
            </p1:ProductDescription>');
GO   
-- Make it a typed xml column by specifying a schema collection.  
ALTER TABLE T   
  ALTER COLUMN Col2 xml (Production.ProductDescriptionSchemaCollection);
```  
  
> [!NOTE]  
> このスクリプトは [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースに対して実行されます。これは、XML スキーマ コレクション `Production.ProductDescriptionSchemaCollection`が [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの一部として作成されるからです。  
  
 上記の例では、列に保存されているすべてのインスタンスは指定したコレクションの XSD スキーマで検証と型指定が行われます。 指定したスキーマに適合しない XML インスタンスが列に含まれている場合、 `ALTER TABLE` ステートメントは失敗するので、型指定されていない XML 列を型指定された XML に変更することができません。  
  
> [!NOTE]  
> 大きなテーブルの場合、 **xml** 型の列を変更すると処理の負担が大きくなることがあります。 これは、各ドキュメントについて、形式が正しいか、型指定された XML であるかどうかを検証する必要があるためです。  
  
型指定された XML に関する詳細については、「 [型指定された XML と型指定されていない XML の比較](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)」を参照してください。  
