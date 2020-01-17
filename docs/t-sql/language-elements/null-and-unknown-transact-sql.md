---
title: NULL と UNKNOWN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 9d491846-4730-4740-a680-77c69fae4a58
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3dba918d0993426111a71785223d0fedd0aba0be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091781"
---
# <a name="null-and-unknown-transact-sql"></a>NULL と UNKNOWN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  NULL は、値が認識できないことを示します。 null 値は、空値または値 0 とは異なります。 2 つの null 値は等しいとは限りません。 2 つの null 値、または null 値と他の値を比較する場合、どの NULL も認識できないので、認識できないことを示す値が返されます。  
  
 null 値は、通常、認識されないデータ、適用できないデータ、または後から追加されるデータを示します。 たとえば、受注時には顧客のミドル名イニシャルはわかりません。  
  
 null 値については、次の点に注意してください。  
  
-   クエリ内で null 値を調べるには、WHERE 句で IS NULL または IS NOT NULL を使用します。  
  
-   INSERT または UPDATE ステートメントに NULL を明示的に記述、または INSERT ステートメントの外に列を置くことで、null 値を列に挿入できます。  
  
-   null 値は、主キーなど、テーブル内のある行と別の行を区別するのに必要な情報として、または、ディストリビューション キーなど、行のディストリビュートに使用される情報に使用することはできません。  
  
 データに null 値がある場合、論理演算子と比較演算子で、TRUE や FALSE の代わりに第 3 の値として UNKNOWN を返すこともできます。 このような 3 値論理が必要な場合、多くのアプリケーション エラーの原因になります。 UNKNOWN を含むブール式の論理演算子は、演算子の結果が UNKNOWN 式に依存しない限り、UNKNOWN を返します。 この動作の例をまとめたものが次の表です。  
  
 次の表では、1 つの式が UNKNOWN を返す 2 つのブール式に AND 演算子を適用した結果を確認できます。  
  
|式 1|式 2|結果|  
|---------------|---------------|------------|  
|TRUE|UNKNOWN|UNKNOWN|  
|UNKNOWN|UNKNOWN|UNKNOWN|  
|FALSE|UNKNOWN|FALSE|  
  
 次の表では、1 つの式が UNKNOWN を返す 2 つのブール式に OR 演算子を適用した結果を確認できます。  
  
|式 1|式 2|結果|  
|---------------|---------------|------------|  
|TRUE|UNKNOWN|TRUE|  
|UNKNOWN|UNKNOWN|UNKNOWN|  
|FALSE|UNKNOWN|UNKNOWN|  
  
## <a name="see-also"></a>参照  
 [AND &#40;Transact-SQL&#41;](../../t-sql/language-elements/and-transact-sql.md)   
 [OR &#40;Transact-SQL&#41;](../../t-sql/language-elements/or-transact-sql.md)   
 [NOT &#40;Transact-SQL&#41;](../../t-sql/language-elements/not-transact-sql.md)   
 [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)  
  
  
