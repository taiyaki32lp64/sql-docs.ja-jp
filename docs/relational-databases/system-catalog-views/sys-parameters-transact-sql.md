---
title: sys.parameters (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.parameters_TSQL
- sys.parameters
- parameters
- parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.parameters catalog view
- table-valued parameters,sys.parameters
ms.assetid: 24e2764b-c8e5-4322-97a4-7407d8b8a92b
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8f91339990e5d12d1b2b674ea9fd124fc4161424
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125352"
---
# <a name="sysparameters-transact-sql"></a>sys.parameters (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  パラメーターを受け入れるオブジェクトのパラメーターごとに 1 行のデータを保持します。 オブジェクトがスカラー関数の場合、戻り値を説明する単一行も含まれます。 その行がある、 **parameter_id** 0 の値。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|このパラメーターが所属するオブジェクトの ID。|  
|**name**|**sysname**|パラメーターの名前。 オブジェクト内で一意です。<br /><br /> オブジェクトがスカラー関数の場合は、パラメーター名は空の文字列の戻り値を表す行にします。|  
|**parameter_id**|**int**|パラメーターの ID。 オブジェクト内で一意です。<br /><br /> 場合は、オブジェクトがスカラー関数、 **parameter_id**戻り値 0 を = です。|  
|**system_type_id**|**tinyint**|パラメーターのシステム型の ID。|  
|**user_type_id**|**int**|ユーザーが定義されているパラメーターの型の ID。<br /><br /> 型の名前を返すには、この列で [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)カタログ ビューに結合します。|  
|**max_length**|**smallint**|(バイト単位)、パラメーターの最大長。<br /><br /> 値列のデータ型の場合は、-1 を = **varchar (max)** 、 **nvarchar (max)** 、 **varbinary (max)** 、または**xml**します。|  
|**有効桁数 (precision)**|**tinyint**|数値に基づく場合は、パラメーターの有効桁数それ以外の場合、0 を返します。|  
|**scale**|**tinyint**|数値に基づく場合は、パラメーターの小数点以下桁数それ以外の場合、0 を返します。|  
|**is_output**|**bit**|1 = パラメーターは OUTPUT または RETURN です。それ以外の場合は 0 です。|  
|**is_cursor_ref**|**bit**|1 = パラメーターはカーソル参照パラメーター。|  
|**has_default_value**|**bit**|1 = パラメーターに既定値。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、このカタログ ビュー内の CLR オブジェクトの既定値のみが保持されます。したがって、[!INCLUDE[tsql](../../includes/tsql-md.md)] オブジェクトに対してこの列の値は 0 になります。 内のパラメーターの既定値を表示する、[!INCLUDE[tsql](../../includes/tsql-md.md)]オブジェクト、クエリ、**定義**の列、 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)カタログ ビュー、またはを使用して、 [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)システム関数。|  
|**is_xml_document**|**bit**|1 = 内容が完全な XML ドキュメントです。<br /><br /> 0 = 内容がドキュメント フラグメント、または列のデータ型でない**xml**します。|  
|**default_value**|**sql_variant**|場合**has_default_value**は 1 です。 この列の値は NULL それ以外の場合、は、パラメーターの既定の値。|  
|**xml_collection_id**|**int**|非ゼロの場合は、パラメーターのデータ型は**xml** XML が型指定されたとします。 この値は、パラメーターの検証 XML スキーマ名前空間を含むコレクションの ID です。<br /><br /> 0 = いいえの XML スキーマ コレクションです。|  
|**is_readonly**|**bit**|1 = パラメーターは読み取り専用です。それ以外の場合、0 を返します。|  
|**is_nullable**|**bit**|1 = パラメーターが null 値を許容します。 (既定値)。<br /><br /> 0 = パラメーターが、許容、ネイティブ コンパイル ストアド プロシージャのより効率的に実行することはありません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server のシステム カタログよく寄せられる質問のクエリを実行します。](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.all_parameters &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-parameters-transact-sql.md)   
 [sys.system_parameters &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)  
  
  
