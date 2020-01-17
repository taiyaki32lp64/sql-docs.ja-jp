---
title: 選択的セカンダリ XML インデックスの作成、変更、および削除 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
ms.assetid: 45128105-833b-40a9-9cc9-1ae03ac0b52b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b96e0bb7f28349e4d0b0ed5225f9b29e58de982f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62637851"
---
# <a name="create-alter-and-drop-secondary-selective-xml-indexes"></a>選択的セカンダリ XML インデックスの作成、変更、および削除
  新しい選択的セカンダリ XML インデックスの作成や、既存の選択的セカンダリ XML インデックスの変更または削除を行う方法について説明します。  
  
##  <a name="create"></a> 選択的セカンダリ XML インデックスの作成  
  
### <a name="how-to-create-a-secondary-selective-xml-index"></a>操作方法: 選択的セカンダリ XML インデックスの作成  
 **Transact-SQL を使用して選択的セカンダリ XML インデックスを作成する**  
 CREATE SELECTIVE XML INDEX ステートメントを呼び出して選択的セカンダリ XML インデックスを作成します。 詳細については、次を参照してください。 [CREATE XML INDEX&#40;選択的 XML インデックス&#41;] (~ t-sql/statements/create-xml-index-selective-xml-indexes/。  
  
 **例**  
  
 次の例では、パス `'pathabc'`に選択的セカンダリ XML インデックスを作成します。 インデックスを作成するパスは、作成時に CREATE SELECTIVE XML INDEX ステートメントで指定された名前によって識別されます。 詳細については、「[CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-selective-xml-index-transact-sql)」を参照してください。  
  
```sql  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="alter"></a> 選択的セカンダリ XML インデックスの変更  
 ALTER ステートメントは、選択的セカンダリ XML インデックスではサポートされません。 選択的セカンダリ XML インデックスを変更するには、既存のインデックスを削除し、再作成します。  
  
### <a name="how-to-alter-a-secondary-selective-xml-index"></a>操作方法:選択的セカンダリ XML インデックスを変更します。  
 **Transact-SQL を使用して選択的セカンダリ XML インデックスを変更する**  
 1.  DROP INDEX ステートメントを呼び出して既存の選択的セカンダリ XML インデックスを削除します。 詳細については、「[DROP INDEX &#40;選択的 XML インデックス&#41;](../indexes/indexes.md)」を参照してください。  
  
2.  CREATE XML INDEX ステートメントを呼び出すことによって必要なオプションのインデックスを再作成します。 詳細については、次を参照してください。 [CREATE XML INDEX&#40;選択的 XML インデックス&#41;] (~ t-sql/statements/create-xml-index-selective-xml-indexes/。  
  
 **例**  
  
 次の例では、インデックスを削除して再作成することにより、選択的セカンダリ XML インデックスを変更します。  
  
```sql  
DROP INDEX filt_sxi_index_c  
  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="drop"></a> 選択的セカンダリ XML インデックスの削除  
  
### <a name="how-to-drop-a-secondary-selective-xml-index"></a>操作方法: 選択的セカンダリ XML インデックスのドロップ  
 **Transact-SQL を使用して選択的セカンダリ XML インデックスを削除する**  
 DROP INDEX ステートメントを呼び出して選択的セカンダリ XML インデックスを削除します。 詳細については、「[DROP INDEX &#40;選択的 XML インデックス&#41;](../indexes/indexes.md)」を参照してください。  
  
 **例**  
  
 DROP INDEX ステートメントの例を次に示します。  
  
```sql  
DROP INDEX ssxi_index  
ON tbl  
```  
  
  
## <a name="see-also"></a>参照  
 [選択的 XML インデックス &#40;SXI&#41;](selective-xml-indexes-sxi.md)  
  
  
