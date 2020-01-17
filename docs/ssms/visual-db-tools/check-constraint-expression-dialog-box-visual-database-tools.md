---
title: '[制約式の確認] ダイアログ ボックス (Visual Database Tools) | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.checkconstraintexpression
ms.assetid: beb6ce43-3913-4d66-8826-8e885335b790
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7f1554ee91444462c52dee404d198b35944a7caf
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263671"
---
# <a name="check-constraint-expression-dialog-box-visual-database-tools"></a>[制約式の確認] ダイアログ ボックス (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
テーブルまたは列に CHECK 制約を適用する場合は、SQL 式を含める必要があります。 CHECK 制約式をボックスに入力します。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
式  
式を入力します。  
  
データが単一の条件を満たすかどうかを確認するには単一の制約式を作成し、データが複数の条件を満たすかどうかを確認するにはブール型の演算子を使用した複合式を作成できます。 たとえば、authors テーブルに、5 桁の文字列を必要とする zip 列が含まれていると仮定します。 このとき、次の制約式では、5 桁の数値だけが許可されます。  
  
```  
zip LIKE '[0-9][0-9][0-9][0-9][0-9]'  
```  
  
または、sales テーブルに、0 より大きい値を必要とする qty という列が含まれていると仮定します。 このとき、下に示す制約では、常に正の値だけが許可されます。  
  
```  
qty > 0  
```  
  
または、orders テーブルで、クレジット カードによる注文に使用できるクレジット カードの種類が制限されると仮定します。 このとき、下に示す制約では、クレジット カードでの注文時に、Visa、MasterCard、または American Express のみが許可されます。  
  
```  
NOT (payment_method = 'credit card') OR  
   (card_type IN ('VISA', 'MASTERCARD', 'AMERICAN EXPRESS'))  
```  
  
## <a name="to-define-a-constraint-expression"></a>制約式を定義するには  
プロパティ ページの [制約のチェック] タブで、次の構文を使用して [制約式] ボックスに式を入力します。  
  
<pre>{constant | column_name | function | (subquery)}  
[{operator | AND | OR | NOT}  
{constant | column_name | function | (subquery)}...]</pre>  
  
SQL 構文は、次のパラメーターで構成されています。  
  
|パラメーター|[説明]|  
|-------------|---------------|  
|定数 (constant)|数値データ、文字データなどのリテラル値です。 文字データは単一引用符 (') で囲む必要があります。|  
|column_name|列を指定します。|  
|関数 (function)|組み込み関数です。|  
|演算子 (operator)|算術演算子、ビット処理演算子、比較演算子、または文字列演算子です。|  
|AND|ブール式で 2 つの式を結合するときに使用します。 両方の式が true のとき、結果が返されます。<br /><br />1 つのステートメントで AND と OR が使用されているときは、AND が先に処理されます。 実行順序は、かっこを使用して変更できます。|  
|OR|ブール式で 2 つ以上の条件を結合するときに使用します。 どちらかの条件が true のとき、結果が返されます。<br /><br />1 つのステートメントで AND と OR が使用されているときは、OR は AND の後に処理されます。 実行順序は、かっこを使用して変更できます。|  
|NOT|LIKE、NULL、BETWEEN、IN、EXISTS などのキーワードを含むすべてのブール式を否定します。<br /><br />1 つのステートメントで複数の論理演算子が使用されているときは、NOT が先に処理されます。 実行順序は、かっこを使用して変更できます。|  
  
## <a name="see-also"></a>参照  
[UNIQUE 制約と CHECK 制約](../../relational-databases/tables/unique-constraints-and-check-constraints.md)  
[UNIQUE 制約の作成](../../relational-databases/tables/create-unique-constraints.md)  
  
