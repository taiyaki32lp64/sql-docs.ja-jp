---
title: BINARY BASE64 オプションの使用 | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, BINARY BASE64 option
ms.assetid: 86a7bb85-7f83-412a-b775-d2c379702fe9
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions
ms.openlocfilehash: eb192cdb9a7e9ffb43561b3b642f60144861c6df
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2019
ms.locfileid: "71199455"
---
# <a name="use-the-binary-base64-option"></a>BINARY BASE64 オプションの使用

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

クエリに BINARY BASE64 オプションを指定すると、バイナリ データが base64 エンコード形式で返されます。

BINARY BASE64 オプションをクエリ内で指定しない場合、既定では、AUTO モードでバイナリ データの URL エンコードがサポートされます。 データベースの仮想ルートへの相対 URL の参照が返されます。 この参照は、クエリが実行されたデータベースに対するものです。 返された参照は、それ以降の操作で実際のバイナリ データにアクセスするときに使用できます。 このアクセスは SQLXML ISAPI dbobject クエリを使用することで実現されます。 画像を識別するために十分な情報をクエリで指定する必要があります。 そのような情報には、主キーの列が含まれる場合があります。

## <a name="column-alias"></a>列の別名

FOR XML AUTO モードを使用して、ビューに対してクエリを実行するときは、バイナリ列に別名を使用しないでください。 別名を使用する場合、バイナリ データの URL エンコードでその別名が返されます。 それ以降の操作では、別名は無意味になります。 意味のない別名と URL エンコードを使用して画像を取得することはできません。

### <a name="cast-to-a-blob"></a>BLOB に型変換する

SELECT クエリでは、任意の列をバイナリ ラージ オブジェクト (BLOB) に型変換すると、列が一時エンティティになります。 一時的であるため、BLOB は、関連付けられている自身のテーブル名と列名を失います。 この型変換により、AUTO モードのクエリでエラーが発生します。システムでは、XML 階層内でのこの値の配置場所が認識されないためです。

たとえば、次のテーブルと、その中の 1 行について考えてみます。

```sql
CREATE TABLE MyTable (Col1 int PRIMARY KEY, Col2 binary)
INSERT INTO MyTable VALUES (1, 0x7);
```

次のクエリでは、エラーが発生します。このエラーは、BLOB (バイナリ ラージ オブジェクト) に型変換することで引き起こされます。

```sql
SELECT Col1,
CAST(Col2 as image) as Col2
FROM MyTable
FOR XML AUTO;
```

これを解決するには、BINARY BASE64 オプションを FOR XML 句に追加します。 型変換を削除すると、クエリから正しい結果が得られます。

```sql
SELECT Col1,
CAST(Col2 as image) as Col2
FROM MyTable
FOR XML AUTO, BINARY BASE64;
```

次のような正しい結果が予想されます。

```console
<MyTable Col1="1" Col2="Bw==" />
```

## <a name="see-also"></a>参照

[FOR XML での AUTO モードの使用](../../relational-databases/xml/use-auto-mode-with-for-xml.md)
