---
title: CERT_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CERT_ID
- CERT_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], certificates
- CERT_ID function
- IDs [SQL Server], certificates
- certificates [SQL Server], IDs
ms.assetid: 59cc06f5-272e-4936-8afe-afba7aba8eea
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 10f97749970337435b14ff0d1dc14df42ad48daf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040133"
---
# <a name="certid-transact-sql"></a>CERT_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

この関数は、証明書の ID 値を返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
Cert_ID ( 'cert_name' )  
```  
  
## <a name="arguments"></a>引数  
**'** *cert_name* **'**  

データベースの証明書の名前。
  
## <a name="return-types"></a>戻り値の型
 **int**  
  
## <a name="remarks"></a>Remarks  
[sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) カタログ ビューでは、証明書名を表示します。
  
## <a name="permissions"></a>アクセス許可  
証明書に関する適切なアクセス許可が必要です。また、証明書に対する呼び出し元の VIEW DEFINITION アクセス許可が拒否されていない必要があります。 証明書のアクセス許可の詳細については、「[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md#permissions)」を参照してください。
  
## <a name="examples"></a>使用例  
次の例では、`ABerglundCert3` という名前の証明書の ID を返します。
  
```sql
SELECT Cert_ID('ABerglundCert3');  
GO  
```  
  
## <a name="see-also"></a>参照
[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)
  
  
