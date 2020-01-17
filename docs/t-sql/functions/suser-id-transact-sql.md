---
title: SUSER_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SUSER_ID_TSQL
- SUSER_ID
dev_langs:
- TSQL
helpviewer_keywords:
- users [SQL Server], IDs
- logins [SQL Server], IDs
- SUSER_ID function
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- user IDs [SQL Server]
ms.assetid: 348911ab-b0b6-4867-aee7-e6f42e053a4a
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: e9bad34cf3d195e4038d794fac913bdb3d16bc91
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843560"
---
# <a name="suser_id-transact-sql"></a>SUSER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  ユーザーのログイン ID 番号を返します。  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降では、SUSER_ID は **sys.server_principals** カタログ ビューで **principal_id** として一覧表示されている値を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SUSER_ID ( [ 'login' ] )   
```  
  
## <a name="arguments"></a>引数  
 **'** *login* **'**  
 ユーザーのログイン名を指定します。 *login* は **nchar** です。 *login* が **char** として指定された場合、*login* は暗黙的に **nchar** に変換されます。 *login* には、任意の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続する権限を持つ Windows ユーザーまたはグループを指定できます。 *login* の指定を省略すると、現在のユーザーのログイン ID 番号が返されます。 パラメーターに "NULL" という語が含まれていると、NULL が返されます。  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
## <a name="remarks"></a>Remarks  
 SUSER_ID は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内に明示的に展開されているログインに対してのみ、ID 番号を返します。 この ID は、所有権と権限を追跡するために、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内で使用されます。 この ID は、SUSER_SID から返されるログインの SID と等しくありません。 *login* が SQL Server ログインの場合、SID は GUID にマップされます。 *login* が Windows ログインまたは Windows グループの場合、SID は Windows セキュリティ識別子にマップされます。  
  
 SUSER_SID は、**syslogins** システム テーブルにエントリを持つログインに対してのみ SUID を返します。  
  
 システム関数は、選択リストの中、WHERE 句の中、および式を使用できるすべての場所で使用できます。ただし、パラメーターを指定しない場合であっても、その後に常にかっこを指定する必要があります。  
  
## <a name="examples"></a>使用例  
 次の例では、`sa` ログインのログイン ID 番号を返します。  
  
```  
SELECT SUSER_ID('sa');  
```  
  
## <a name="see-also"></a>参照  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [SUSER_SID &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  
