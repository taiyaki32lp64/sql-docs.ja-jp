---
title: sys.all_parameters (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- all_parameters_TSQL
- sys.all_parameters
- all_parameters
- sys.all_parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_parameters catalog view
ms.assetid: eecbb68e-9b4c-4243-94e2-8096a9cc7892
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 63231301109f83243b431244028fddffb8cc6fe7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001326"
---
# <a name="sysallparameters-transact-sql"></a>sys.all_parameters (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  すべてのパラメーターが属するユーザー定義またはシステム オブジェクトの和集合を示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|このパラメーターが所属するオブジェクトの ID。|  
|**name**|**sysname**|パラメーターの名前。 オブジェクト内で一意です。 オブジェクトがスカラー関数の場合は、パラメーター名は空の文字列の戻り値を表す行にします。|  
|**parameter_id**|**int**|パラメーターの ID。 オブジェクト内で一意です。 場合は、オブジェクトがスカラー関数、 **parameter_id**戻り値 0 を = です。|  
|**system_type_id**|**tinyint**|パラメーターのシステム型の ID。|  
|**user_type_id**|**int**|ユーザーが定義されているパラメーターの型の ID。<br /><br /> 型の名前を返すには、この列で [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)カタログ ビューに結合します。|  
|**max_length**|**smallint**|(バイト単位)、パラメーターの最大長。<br /><br /> -1 = 列のデータ型は**varchar (max)** 、 **nvarchar (max)** 、 **varbinary (max)** 、または**xml**します。|  
|**有効桁数 (precision)**|**tinyint**|パラメーターが数値ベースの場合の有効桁数。数値ではない場合は 0 です。|  
|**scale**|**tinyint**|数値に基づく場合、パラメーターの小数点以下桁数それ以外の場合、0 を返します。|  
|**is_output**|**bit**|1 = パラメーターが出力 (または、返す)。それ以外の場合、0 を返します。|  
|**is_cursor_ref**|**bit**|1 = パラメーターは、カーソル参照パラメーター。|  
|**has_default_value**|**bit**|1 = パラメーターには既定値があります。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] このカタログ ビュー内の CLR オブジェクトの既定値のみが保持されます。そのため、この列は値 0 を常に[!INCLUDE[tsql](../../includes/tsql-md.md)]オブジェクト。 内のパラメーターの既定値を表示する、[!INCLUDE[tsql](../../includes/tsql-md.md)]オブジェクト、クエリ、**定義**の列、 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)カタログ ビュー、またはを使用して、 [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)システム関数。|  
|**is_xml_document**|**bit**|1 = 内容が完全な XML ドキュメントです。<br /><br /> 0 = 内容がドキュメントの一部か、列のデータ型でない**xml**します。|  
|**default_value**|**sql_variant**|場合**has_default_value**は 1 です。 この列の値は NULL それ以外の場合、は、パラメーターの既定の値。|  
|**xml_collection_id**|**int**|パラメーターを評価するために使用される XML スキーマ コレクションの ID。<br /><br /> パラメーターのデータ型がある場合、0 以外の場合**xml** XML が型指定されたとします。<br /><br /> 0 = XML スキーマ コレクションが存在しないか、パラメーターが XML ではありません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server のシステム カタログよく寄せられる質問のクエリを実行します。](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [sys.system_parameters &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)  
  
  
