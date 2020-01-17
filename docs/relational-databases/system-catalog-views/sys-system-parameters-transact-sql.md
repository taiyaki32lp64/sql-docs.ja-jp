---
title: sys.system_parameters (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.system_parameters
- sys.system_parameters_TSQL
- system_parameters_TSQL
- system_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_parameters catalog view
ms.assetid: 0d135c5f-68b5-4009-a0da-35e6abfee0ff
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: da8d2bb7be2c3da502065d9ee210c4c1ef8c2094
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108809"
---
# <a name="syssystemparameters-transact-sql"></a>sys.system_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  パラメーターを持つシステム オブジェクトごとに 1 つの行が含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|このパラメーターが所属するオブジェクトの ID。|  
|**name**|**sysname**|パラメーターの名前。 オブジェクト内で一意です。<br /><br /> オブジェクトがスカラー関数の場合は、パラメーター名は空の文字列の戻り値を表す行にします。|  
|**parameter_id**|**int**|パラメーターの ID。 オブジェクト内で一意です。 場合は、オブジェクトがスカラー関数、 **parameter_id**戻り値 0 を = です。|  
|**system_type_id**|**tinyint**|パラメーターのシステム型の ID。|  
|**user_type_id**|**int**|ユーザーが定義されているパラメーターの型の ID。<br /><br /> 型の名前を返すには、この列で [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)カタログ ビューに結合します。|  
|**max_length**|**smallint**|(バイト単位)、パラメーターの最大長。 値は列のデータ型の場合に達すると-1 になります**varchar (max)** 、 **nvarchar (max)** 、 **varbinary (max)** 、または**xml**します。|  
|**有効桁数 (precision)**|**tinyint**|数値に基づく場合は、パラメーターの有効桁数それ以外の場合、0 を返します。|  
|**scale**|**tinyint**|数値に基づく場合は、パラメーターの小数点以下桁数それ以外の場合、0 を返します。|  
|**is_output**|**bit**|1 = パラメーターが出力 (または、返す)。それ以外の場合、0 を返します。|  
|**is_cursor_ref**|**bit**|1 = パラメーターはカーソル参照パラメーター。|  
|**has_default_value**|**bit**|1 = パラメーターに既定値。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] このカタログ ビュー内の CLR オブジェクトの既定値のみが保持されます。そのため、この列は値 0 を常に[!INCLUDE[tsql](../../includes/tsql-md.md)]オブジェクト。 内のパラメーターの既定値を表示する、[!INCLUDE[tsql](../../includes/tsql-md.md)]オブジェクト、クエリ、**定義**の列、 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)カタログ ビュー、またはを使用して、 [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)システム関数。|  
|**is_xml_document**|**bit**|1 = 内容が完全な XML ドキュメントです。<br /><br /> 0 = 内容がドキュメントの一部か、列のデータ型でない**xml**します。|  
|**default_value**|**sql_variant**|場合**has_default_value**は 1 です。 この列の値は、パラメーターの既定の値。 それ以外の場合は NULL です。|  
|**xml_collection_id**|**int**|非ゼロの場合は、パラメーターのデータ型は**xml** XML が型指定されたとします。 値は、パラメーターの検証 XML スキーマ名前空間を含むコレクションの ID です。<br /><br /> 0 = XML スキーマ コレクションはありません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server のシステム カタログよく寄せられる質問のクエリを実行します。](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [sys.all_parameters &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-parameters-transact-sql.md)  
  
  
