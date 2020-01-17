---
title: XML のセキュリティに関する考慮事項 (SQLXML 4.0) の |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- NESTED mode
- client-side XML formatting
- FOR XML clause, security
- server-side XML formatting
- AUTO mode
- security [SQLXML], FOR XML
ms.assetid: facba279-df93-475b-ad43-0043dc5bae03
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34172dcb60e5f2729d8810f697ef975f042f5233
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010538"
---
# <a name="for-xml-security-considerations-sqlxml-40"></a>FOR XML のセキュリティに関する注意点 (SQLXML 4.0)
  FOR XML AUTO モードでは、XML 階層が生成され、要素名はテーブル名に、属性名は列名にマップされます。 この場合、データベースのテーブルと列の情報が公開されます。 AUTO モード (サーバー側の書式設定) を使用する場合は、テーブルと列の別名をクエリで指定することで、データベース情報を隠すことができます。 これらの別名は、結果の XML ドキュメント内に要素名および属性名として返されます。  
  
 たとえば、次のクエリでは AUTO モードを指定しており、XML の書式設定はサーバーで実行されます。  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 結果の XML ドキュメントでは、要素名と属性名に別名が使用されます。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <C F="Nancy" L="Fuller" />   
  <CE F="Andrew" L="Peacock" />   
  <C F="Janet" L="Leverling" />   
  ...  
</root>  
```  
  
 NESTED モード (クライアント側の書式設定) を使用する場合、結果の XML ドキュメントでは、別名が属性にのみ返され、 ベース テーブルの名前が常に要素名として返されます。 たとえば、次のクエリでは NESTED モードを指定しています。  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 結果の XML ドキュメントでは、ベース テーブルの名前が要素名として返され、テーブルの別名は使用されません。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Person.Contact F="Nancy" L="Fuller" />   
  <Person.Contact F="Andrew" L="Peacock" />   
  <Person.Contact F="Janet" L="Leverling" />   
       ...  
</root>  
```  
  
  
