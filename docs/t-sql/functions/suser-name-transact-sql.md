---
title: SUSER_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SUSER_NAME
- SUSER_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- security identification names [SQL Server]
- logins [SQL Server], users
- identification names for logins [SQL Server]
- users [SQL Server], logins
- SUSER_NAME function
- logins [SQL Server], names
- names [SQL Server], logins
ms.assetid: ae598d9f-9baa-49b8-b1c1-042854206de4
author: VanMSFT
ms.author: vanto
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a9b0e4e37eef574fd50d28e02c4f92ee1805c953
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117619"
---
# <a name="susername-transact-sql"></a>SUSER_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

ユーザーのログイン識別名を返します。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SUSER_NAME ( [ server_user_id ] )   
```  
  
## <a name="arguments"></a>引数  
_server\_user\_id_  
ユーザーのログイン ID 番号です。 _server\_user\_id_ (省略可能) は **int** です。_server\_user\_id_ には、任意の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインまたは [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ユーザーのログイン ID 番号、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続するためのアクセス許可があるグループのログイン ID 番号を指定できます。 _server\_user\_id_ を指定しないと、現在のユーザーのログイン ID 名が返されます。 パラメーターに "NULL" という語が含まれていると、NULL が返されます。  
  
## <a name="return-types"></a>戻り値の型  
**nvarchar(128)**  
  
## <a name="remarks"></a>Remarks  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version 7.0 では、サーバー ユーザー識別番号 (SUID) の代わりにセキュリティ識別番号 (SID) が使用されます。  
  
SUSER_NAME では、**syslogins** システム テーブル内にエントリがあるログインに対してのみログイン名が返されます。  
  
SUSER_NAME は、選択リストの中、WHERE 句の中、また、式を使える所ならどこにでも使用できます。 パラメーターが指定されていない場合でも、SUSER_NAME の後に括弧を使用します。  
  
## <a name="examples"></a>使用例  
次の例では、ログイン識別番号 `1` のユーザーのログイン識別名を返します。  
  
```  
SELECT SUSER_NAME(1);  
```  
  
## <a name="see-also"></a>参照  
[SUSER_ID &#40;Transact-SQL&#41;](../../t-sql/functions/suser-id-transact-sql.md)   
[プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
