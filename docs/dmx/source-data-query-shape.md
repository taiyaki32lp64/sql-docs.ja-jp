---
title: SHAPE (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c928d4c96917479f8c37415d5ebe2db9b7f9eb98
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938115"
---
# <a name="ltsource-data-querygt---shape"></a>&lt;ソース データ クエリ&gt;-図形
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  単一の階層テーブル (つまり、入れ子になったテーブルを持つテーブル)、マイニング モデルのケース テーブルになるには、複数のデータ ソースからクエリを結合します。  
  
 完全な構文、**SHAPE**コマンドが記載されて、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Data Access Components (MDAC) ソフトウェア開発キット (SDK)。  
  
## <a name="syntax"></a>構文  
  
```  
  
SHAPE {<master query>}  
APPEND ({ <child table query> }   
     RELATE <master column> TO <child column>)   
          AS <column table name>  
[  
     ({ <child table query> }   
     RELATE <master column> TO <child column>)   
          AS < column table name>  
...  
]       
```  
  
## <a name="arguments"></a>引数  
 *マスターのクエリ*  
 クエリは親テーブルを返します。  
  
 *子テーブルのクエリ*  
 クエリは、入れ子になったテーブルを返します。  
  
 *マスターの列*  
 Child table query の結果から子の行を識別するために、親テーブル内の列。  
  
 *子の列*  
 Master query の結果から親の行を識別するために、子テーブル内の列。  
  
 *テーブル名の列*  
 入れ子になったテーブルの親テーブルに、列名を新たに追加します。  
  
## <a name="remarks"></a>コメント  
 親テーブルと子テーブルを関連付けられている列で、クエリを注文する必要があります。  
  
## <a name="examples"></a>使用例  
 内で次の例を使用することができます、 [INSERT INTO &#40;DMX&#41; ](../dmx/insert-into-dmx.md)入れ子になったテーブルを含むモデルをトレーニングするステートメント。 2 つのテーブル内で、**SHAPE**から関連するステートメント、 **OrderNumber**列。  
  
```  
SHAPE {  
    OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
```  
  
## <a name="see-also"></a>関連項目  
 [&#60;ソース データ クエリ&#62;](../dmx/source-data-query.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
