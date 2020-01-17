---
title: sys.fn_check_object_signatures (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_check_object_signatures_TSQL
- fn_check_object_signatures_TSQL
- fn_check_object_signatures
- sys.fn_check_object_signatures
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_check_object_signatures function
ms.assetid: 47509566-d3d7-46a9-89c1-91b4895d56b9
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1b9054cae2d8b67a96be964ca8dd0f1effe2113a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046310"
---
# <a name="sysfn_check_object_signatures-transact-sql"></a>sys.fn_check_object_signatures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  署名可能なすべてのオブジェクトの一覧を返し、オブジェクトが、指定した証明書または非対称キーで署名されているかどうかを示します。 オブジェクトは、指定された証明書または非対称キーの署名によって署名されて場合、も、オブジェクトの署名が有効かどうかを返します。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
fn_ check_object_signatures (   
    { '@class' } , { @thumbprint }   
  )   
```  
  
## <a name="arguments"></a>引数  
 {0} '\@*class*'}  
 提供される thumbprint の種類を識別します。  
  
-   'certificate'  
  
-   'asymmetric key'  
  
 \@*class* は **sysname** です。  
  
 { \@*thumbprint*}  
 キーの暗号化で使用された証明書の SHA-1 ハッシュ。または、キーの暗号化で使用された非対称キーの GUID。 \@*thumbprint* は **varbinary (20)** です。  
  
## <a name="tables-returned"></a>返されるテーブル  
 次の表に、列を**fn_check_object_signatures**を返します。  
  
|[列]|種類|説明|  
|------------|----------|-----------------|  
|type|**nvarchar(120)**|説明またはアセンブリの型を返します。|  
|entity_id|**int**|評価対象のオブジェクトのオブジェクト ID を返します。|  
|is_signed|**int**|提供された thumbprint でオブジェクトが署名されていない場合は、0 を返します。 提供された thumbprint でオブジェクトが署名されたときに、1 を返します。|  
|is_signature_valid|**int**|Is_signed の値が 1 の場合は、署名が無効である場合に 0 を返します。 署名が有効な場合は、1 を返します。<br /><br /> is_signed の値が 0 の場合は、常に 0 を返します。|  
  
## <a name="remarks"></a>コメント  
 使用**fn_check_object_signatures**を悪意のあるユーザーがオブジェクトに改ざんされていないことを確認します。  
  
## <a name="permissions"></a>アクセス許可  
 証明書または非対称キーに対する VIEW DEFINITION が必要です。  
  
## <a name="examples"></a>使用例  
 次の例は、署名証明書のスキーマを検索、`master`データベース、および返します、 `is_signed` 1 の値と`is_signature_valid`スキーマ署名証明書によって署名されていると、有効になったこれらのオブジェクトの 1 の値署名します。  
  
```  
USE master;  
-- Declare a variable to hold the thumbprint.  
DECLARE @thumbprint varbinary(20) ;  
-- Populate the thumbprint variable with the master database schema signing certificate.  
SELECT @thumbprint = thumbprint   
FROM sys.certificates   
WHERE name LIKE '%SchemaSigningCertificate%' ;  
-- Evaluates the objects signed by the schema signing certificate  
SELECT type, entity_id, OBJECT_NAME(entity_id) AS [object name], is_signed, is_signature_valid  
FROM sys.fn_check_object_signatures ('certificate', @thumbprint) ;  
GO  
  
```  
  
## <a name="see-also"></a>関連項目  
 [IS_OBJECTSIGNED &#40;Transact-SQL&#41;](../../t-sql/functions/is-objectsigned-transact-sql.md)  
  
  
