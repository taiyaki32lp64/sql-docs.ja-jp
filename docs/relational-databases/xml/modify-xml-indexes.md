---
title: XML インデックスの変更 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XML indexes [SQL Server], modifying
- modifying indexes
ms.assetid: 24d50fe1-c6ec-49e6-91a3-9791851ba53d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3a579fcf8809c8c05838dad70126421362cd8048
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042682"
---
# <a name="modify-xml-indexes"></a>XML インデックスの変更
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] DDL ステートメントを使用すると、既存の XML インデックスや XML 以外のインデックスを変更できます。 ただし、一部の ALTER INDEX オプションは XML インデックスに使用できません。 次のオプションは、XML インデックスの変更時には無効です。  
  
-   再構築と設定オプションの IGNORE_DUP_KEY は XML インデックスでは無効です。 再構築オプション ONLINE は、セカンダリ XML インデックスでは OFF に設定されている必要があります。 オプション DROP_EXISTING は、ALTER INDEX ステートメントでは使用できません。  
  
-   ユーザー テーブルの主キー制約に変更があった場合、自動的には XML インデックスに反映されません。 ユーザーが、まず XML インデックスを削除し、次に XML インデックスを再作成する必要があります。  
  
-   ALTER INDEX ALL を指定すると、このオプションは XML 以外のインデックスと XML インデックスの両方に適用されます。 一方の種類のインデックスでは無効なインデックス オプションが指定される場合があります。 その場合、ステートメント全体が失敗します。  
  
## <a name="example-modifying-an-xml-index"></a>例: XML インデックスの変更  
 次の例では、XML インデックスを作成後、 `ALLOW_ROW_LOCKS` オプションを `OFF`に設定してインデックスを変更します。 `ALLOW_ROW_LOCKS` が `OFF`の場合、行はロックされないので、ページレベルおよびテーブルレベルのロックを使用して、指定したインデックスにアクセスできます。  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
-- Create primary XML index.   
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol)  
GO  
-- Note the type 3 is index on XML type.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'  
  
-- Modify and set an index option.  
ALTER INDEX PIdx_T_XmlCol on T   
SET (ALLOW_ROW_LOCKS = OFF)  
```  
  
## <a name="example-disabling-and-enabling-an-xml-index"></a>例: XML インデックスの無効化と有効化  
 既定では、XML インデックスは有効です。 XML インデックスが無効になっている場合、その XML 列に実行されるクエリでは XML インデックスが使用されません。 XML インデックスを有効にするには、 `ALTER INDEX` オプションを指定した `REBUILD` を使用します。  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol ON T(XmlCol)  
GO  
ALTER INDEX PIdx_T_XmlCol on T DISABLE  
Go  
-- Verify index is disabled.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'  
-- Rebuild the index.  
ALTER INDEX PIdx_T_XmlCol on T REBUILD  
Go  
```  
  
## <a name="see-also"></a>参照  
 [XML インデックス &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  
