---
title: BINARY BASE64 オプションの使用 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, BINARY BASE64 option
ms.assetid: 86a7bb85-7f83-412a-b775-d2c379702fe9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bda0167e1e55c3ded715de96027a153ec5a65de
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63231253"
---
# <a name="use-the-binary-base64-option"></a>BINARY BASE64 オプションの使用
  クエリに BINARY BASE64 オプションを指定すると、バイナリ データが base64 エンコード形式で返されます。 AUTO モードでは、BINARY BASE64 オプションを指定しないと、既定でバイナリ データの URL エンコードがサポートされます。 つまり、バイナリ データではなく、クエリが実行されたデータベースの仮想ルートからの相対 URL への参照が返されます。 この参照は、それ以降の操作で SQLXML ISAPI dbobject クエリを使用して実際のバイナリ データにアクセスするときに使用できます。 クエリで画像を識別するには、主キー列など、十分な情報を提供する必要があります。  
  
 クエリを指定するときに、ビューのバイナリ列に別名を使用すると、その別名がバイナリ データの URL エンコードで返されます。 それ以降の操作では別名は無意味になり、URL エンコードを使用して画像を取得することはできません。 したがって、FOR XML AUTO モードを使用してビューのクエリを実行するときは、別名を使用しないでください。  
  
 たとえば、SELECT クエリで、BLOB (バイナリ ラージ オブジェクト) に任意の列をキャストした場合、列は一時エンティティになります (関連するテーブル名と列名が失われます)。 これにより、AUTO モードのクエリでエラーが発生します。これは XML 階層内でのこの値の配置場所がわからないためです。 例 :  
  
```  
CREATE TABLE MyTable (Col1 int PRIMARY KEY, Col2 binary)  
INSERT INTO MyTable VALUES (1, 0x7);  
```  
  
 次のクエリでは、BLOB (バイナリ ラージ オブジェクト) へのキャストによるエラーが発生します。  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO;  
```  
  
 これを解決するには、BINARY BASE64 オプションを FOR XML 句に追加します。 キャストを削除すると、クエリは予想どおりの結果を作成します。  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO, BINARY BASE64;  
```  
  
 結果を次に示します。  
  
```  
<MyTable Col1="1" Col2="Bw==" />  
```  
  
## <a name="see-also"></a>関連項目  
 [FOR XML での AUTO モードの使用](use-auto-mode-with-for-xml.md)  
  
  
