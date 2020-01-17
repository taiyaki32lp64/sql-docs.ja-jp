---
title: sys.assembly_modules (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.assembly_modules
- sys.assembly_modules_TSQL
- assembly_modules
- assembly_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_modules catalog view
ms.assetid: 5f9e644e-8065-49a2-b53d-db7df98f70d8
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 68e91d6935549bc8dd421361c092c3ad1fb01905
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118169"
---
# <a name="sysassemblymodules-transact-sql"></a>sys.assembly_modules (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  各関数、プロシージャ、または共通言語ランタイム (CLR) アセンブリで定義されているトリガーの 1 つの行を返します。 このカタログ ビューは、CLR ストアド プロシージャ、CLR トリガー、または CLR 関数を基になる実装にマップします。 種類が TA、AF、PC、FS、および FT のオブジェクトには、関連するアセンブリ モジュールがあります。 オブジェクトとアセンブリの間の関連を見つけるには、このカタログ ビューを他のカタログ ビューに結合します。 たとえば、CLR ストアド プロシージャを作成するときで表される 1 つの行**sys.objects**、1 つの行**sys.procedures** (から継承する**sys.objects**)、および1 つの行**sys.assembly_modules**します。 ストアド プロシージャ自体が内のメタデータによって表される**sys.objects**と**sys.procedures**します。 プロシージャの基になる CLR 実装への参照がある**sys.assembly_modules**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|SQL オブジェクトのオブジェクト ID 番号。 データベース内で一意です。|  
|**assembly_id**|**int**|このモジュールの作成元のアセンブリの ID。|  
|**assembly_class**|**sysname**|このモジュールを定義するアセンブリ内のクラスの名前です。|  
|**assembly_method**|**sysname**|内のメソッドの名前、 **assembly_class**このモジュールを定義します。<br /><br /> 集計関数 (AF) の場合は NULL です。|  
|**null_on_null_input**|**bit**|モジュールは、任意の NULL 入力に対して NULL 出力を生成するように宣言されています。|  
|**execute_as_principal_id**|**int**|コンテキストの実行が発生したデータベース プリンシパルの ID、EXECUTE AS で指定された CLR 関数、ストアド プロシージャまたはトリガーの句。<br /><br /> NULL = EXECUTE AS CALLER。 既定値です。<br /><br /> 指定したデータベース プリンシパルの ID = EXECUTE AS SELF、EXECUTE AS *user_name*、または EXECUTE AS *login_name*します。<br /><br /> -2 = EXECUTE AS OWNER。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
