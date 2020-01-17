---
title: sp_help_spatial_geometry_index (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_index
- sp_help_spatial_geometry_index_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_index procedure
ms.assetid: f1bcefb1-09c8-4b49-8c51-5d471065849f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e2e5d935fc3d6db5d243ec4b76841f13a60e5a11
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304856"
---
# <a name="sp_help_spatial_geometry_index-transact-sql"></a>sp_help_spatial_geometry_index (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  **Geometry**空間インデックスについて、指定された一連のプロパティの名前と値を返します。 結果はテーブル形式で返されます。 プロパティのコアセットとインデックスのすべてのプロパティのどちらを返すかを選択できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_spatial_geometry_index [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput'   
     [ , [ @query_sample = ] 'query_sample']   
```  
  
## <a name="arguments"></a>引数  
 「[空間インデックスストアドプロシージャの引数とプロパティ」を](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)参照してください。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 「[空間インデックスストアドプロシージャの引数とプロパティ」を](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 プロシージャにアクセスするには、ユーザーに PUBLIC ロールが割り当てられている必要があります。 サーバーとオブジェクトに対する読み取りアクセス権限が必要です。  
  
## <a name="remarks"></a>Remarks  
 NULL 値を含むプロパティは、返されるセットに含まれません。  
  
## <a name="example"></a>例  
 次の例では、`sp_help_spatial_geometry_index` を使用して、 **\@qs**で指定されたクエリサンプルのテーブル**geometry_col**で定義されている空間インデックス**SIndx_SpatialTable_geometry_col2**を調査します。 この例では、指定したインデックスのコアプロパティのみが返されます。  
  
```  
declare @qs geometry  
        ='POLYGON((-90.0 -180.0, -90.0 180.0, 90.0 180.0, 90.0 -180.0, -90.0 -180.0))';  
exec sp_help_spatial_geometry_index 'geometry_col', 'SIndx_SpatialTable_geometry_col2', 0, @qs;  
```  
  
## <a name="see-also"></a>参照  
 [空間インデックスストアドプロシージャ](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index_xml](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)   
 [空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [空間データ &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
