---
title: OPENROWSET (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8be3fe8cbf30121ec2895f59306c925a422d5c39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938125"
---
# <a name="ltsource-data-querygt---openrowset"></a>&lt;ソース データ クエリ&gt;-OPENROWSET
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  外部プロバイダーへのクエリでは、ソース データ クエリを置き換えます。 INSERT、SELECT FROM PREDICTION JOIN、および SELECT FROM NATURAL PREDICTION JOIN ステートメントをサポートして**OPENROWSET**します。  
  
## <a name="syntax"></a>構文  
  
```  
  
OPENROWSET(provider_name,provider_string,query_syntax)  
```  
  
## <a name="arguments"></a>引数  
 *provider_name*  
 OLE DB プロバイダー名。  
  
 *provider_string*  
 指定されたプロバイダーの OLE DB 接続文字列。  
  
 *query_syntax*  
 行セットを返すクエリ構文です。  
  
## <a name="remarks"></a>コメント  
 データ マイニング プロバイダーを使用して、データ ソース オブジェクトへの接続を確立*provider_name*と*provider_string、* で指定されたクエリを実行および*query_syntax*ソース データから行セットを取得します。  
  
## <a name="examples"></a>使用例  
 次の例からデータを取得する、PREDICTION JOIN ステートメント内で使用できる、[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]を使用してデータベースを[!INCLUDE[tsql](../includes/tsql-md.md)]SELECT ステートメント。  
  
```  
OPENROWSET  
(  
'SQLOLEDB.1',  
'Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security     Info=False;Initial Catalog=AdventureWorksDW2012;Data Source=localhost',  
'SELECT TOP 1000 * FROM vTargetMail'  
)  
```  
  
## <a name="see-also"></a>関連項目  
 [&#60;ソース データ クエリ&#62;](../dmx/source-data-query.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
