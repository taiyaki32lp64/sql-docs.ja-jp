---
title: sp_help_spatial_geometry_index_xml (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_index_xml_TSQL
- sp_help_spatial_geometry_index_xml
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_index_xml procedure
ms.assetid: 9668ae6d-9ed5-418e-bb9a-9e7b66f7dd16
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9e7eb2e007191088a0259360924b2f5f931dec0a
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304900"
---
# <a name="sp_help_spatial_geometry_index_xml-transact-sql"></a>sp_help_spatial_geometry_index_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  **Geometry**空間インデックスについて、指定された一連のプロパティの名前と値を返します。 プロパティのコアセットとインデックスのすべてのプロパティのどちらを返すかを選択できます。  
  
 結果は、選択したプロパティの名前と値を表示する XML フラグメントで返されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_spatial_geometry_index [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ]'{ 0 | 1 }]   
     [ , [ @query_sample = ] 'query_sample' ]   
     [ ,.[ @xml_output = ] 'xml_output' ]   
```  
  
## <a name="arguments"></a>引数  
 「[空間インデックスストアドプロシージャの引数とプロパティ」を](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)参照してください。  
  
## <a name="properties"></a>プロパティ  
 「[空間インデックスストアドプロシージャの引数とプロパティ」を](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーは、 **public**ロールのメンバーである必要があります。 サーバーとオブジェクトに対する読み取りアクセス権限が必要です。  
  
## <a name="remarks"></a>Remarks  
 NULL 値を含むプロパティは、XML の戻り値のセットに含まれません。  
  
## <a name="example"></a>例  
 次の例では、`sp_help_spatial_geometry_index_xml` を使用して、 **\@qs**で指定されたクエリサンプルのテーブル**geometry_col**で定義されている空間インデックス**SIndx_SpatialTable_geometry_col2**を調査します。 この例では、選択したプロパティの名前と値を表示する XML フラグメント内の指定されたインデックスのコアプロパティを返します。  
  
 その後、 [XQuery](../../xquery/xquery-basics.md)が結果セットで実行され、特定のプロパティが返されます。  
  
```  
DECLARE @qs geometry  
        ='POLYGON((-90.0 -180.0, -90.0 180.0, 90.0 180.0, 90.0 -180.0, -90.0 -180.0))';  
DECLARE @x xml;  
EXEC sp_help_spatial_geometry_index_xml 'geometry_col', 'SIndx_SpatialTable_geometry_col2', 0, @qs, @x output;  
SELECT @x.value('(/Primary_Filter_Efficiency/text())[1]', 'float');  
```  
  
 [Sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)と同様に、このストアドプロシージャを使用すると、空間インデックスのプロパティにプログラムで簡単にアクセスして、XML 形式で結果セットを報告できます。  
  
## <a name="requirements"></a>の要件  
  
## <a name="see-also"></a>参照  
 [空間インデックスストアドプロシージャの引数とプロパティ](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)   
 [空間インデックスストアドプロシージャ](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)   
 [空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [空間データ &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [XQuery の基礎](../../xquery/xquery-basics.md)   
 [XQuery 言語リファレンス](../../xquery/xquery-language-reference-sql-server.md)  
  
  
