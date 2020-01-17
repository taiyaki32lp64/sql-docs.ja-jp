---
title: sp_help_spatial_geography_histogram (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_histogram_TSQL
- sp_help_spatial_geography_histogram
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geography_histogram
ms.assetid: 5c5bd319-055d-4cd6-8c5a-06354cc056cc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3c2b94b4c76054fb1e9ce6e078f3490ad263a52c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085188"
---
# <a name="sphelpspatialgeographyhistogram-transact-sql"></a>sp_help_spatial_geography_histogram (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  空間インデックスのグリッドのパラメーターのキーの更新が容易になります。  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_spatial_geography_histogram [ @tabname =] 'tabname'   
     [ , [ @colname = ] 'columnname' ]   
     [ , [ @resolution = ] 'resolution' ]  
     [ , [ @sample = ] 'tablesample' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @tabname = ] 'tabname'` 空間インデックスが指定されているテーブルの修飾付きまたは修飾なしの名前です。  
  
 引用符は、修飾されたテーブルが指定されている場合にのみ必要です。 データベース名を含む、完全修飾名が指定されている場合、データベース名は、現在のデータベースの名前である必要があります。 *tabname $* は**sysname**、既定値はありません。  
  
`[ @colname = ] 'columnname'` 指定された空間列の名前です。 *columnname*は、 **sysname**、既定値はありません。  
  
`[ @resolution = ] 'resolution'` 境界ボックスの解像度です。 有効な値は 10 ～ 5000 です。 *解像度*は、 **tinyint**、既定値はありません。  
  
`[ @sample = ] 'sample'` 使用するテーブルの割合です。 有効な値は 0 ~ 100 です。 *tablesample*は、 **float**します。 既定値は 100 です。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 テーブルの値が返されます。 次の表では、テーブルの列の内容について説明します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**cellid**|**int**|開始カウントが 1 の各セルの一意の ID を表します。|  
|**セル**|**geography**|それぞれのセルを表す四角形です。 セルの形は、空間インデックス作成用に使用されたセルの形と同じです。|  
|**row_count**|**bigint**|接しているか、またはセルを含む空間オブジェクトの数を示します。|  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーのメンバーである必要があります、**パブリック**ロール。 サーバーとオブジェクトの読み取りアクセス許可が必要です。  
  
## <a name="remarks"></a>コメント  
 SSMS 空間タブでは、結果がグラフィカルに表示されます。 結果の項目のおおよその数を取得する空間ウィンドウに対して結果を照会できます。  
  
> [!NOTE]  
>  テーブル内のオブジェクトが、テーブル内のセルの合計が実際のオブジェクトの数よりも大きいことがあります、1 つ以上のセルについて説明します。  
  
 境界ボックス、 **geography**型は、地球全体です。  
  
## <a name="examples"></a>使用例  
 次の例では**sp_help_spatial_geography_histogram**上、`Person.Address`テーブルに、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]データベース。  
  
```  
EXEC sp_help_spatial_geography_histogram @tabname = Person.Address, @colname = SpatialLocation, @resolution = 64, @sample = 30;  
```  
  
## <a name="see-also"></a>関連項目  
 [空間インデックス ストアド プロシージャ&#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)  
  
  
