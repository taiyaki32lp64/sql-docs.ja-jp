---
title: sys.syscharsets (TRANSACT-SQL) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syscharsets
- syscharsets
- sys.syscharsets_TSQL
- syscharsets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syscharsets system table
- sys.syscharsets compatibility view
ms.assetid: f16d987c-bd19-4668-9ef7-785b8fb9ff5b
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4332159765791addfdfcc32a9d19d29836f2460c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053545"
---
# <a name="syssyscharsets-transact-sql"></a>sys.syscharsets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  1 つの行を含みます。 各文字を設定し、並べ替え順序の定義で使用するための、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]します。 マークされている並べ替え順序のいずれかが**sysconfigures**として既定の並べ替え順序。 実際はこの並べ替え順だけが使用されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**type**|**smallint**|この行で表されるエンティティの種類。<br /><br /> 1001 = 文字セット。<br /><br /> 2001 = 並べ替え順|  
|**id**|**tinyint**|文字セットまたは並べ替え順を表す一意な ID。 並べ替え順と文字セットは、同じ ID 番号を共有できません。 1 ～ 240 の ID は、[!INCLUDE[ssDE](../../includes/ssde-md.md)]が使用するために予約されています。|  
|**csid**|**tinyint**|文字セットを表す行の場合、このフィールドは使用されません。 並べ替え順を表す行の場合は、その並べ替え順が適用される文字セットの ID になります。 この ID を持つ文字セットの行がこのテーブルに存在すると見なされます。|  
|**status**|**smallint**|内部システム状態の情報ビット。|  
|**name**|**sysname**|文字の一意の名前は、セットまたは並べ替え順。 このフィールドは文字 A ~ Z または a ~ z、数字 0 - 9、およびアンダーのみを含める必要があります。文字で始まる必要があります。|  
|**description**|**nvarchar (255)**|文字の機能の説明 (オプション) は、セットまたは並べ替え順。|  
|**binarydefinition**|**varbinary(6000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**definition**|**image**|文字の内部の定義は、セットまたは並べ替え順。 このフィールドのデータの構造は、種類によって異なります。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビューへのシステム テーブルのマッピング&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
