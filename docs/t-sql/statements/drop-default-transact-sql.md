---
title: DROP DEFAULT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_DEFAULT_TSQL
- DROP DEFAULT
dev_langs:
- TSQL
helpviewer_keywords:
- DROP DEFAULT statement
- defaults [SQL Server], removing
ms.assetid: d2d3af25-8877-46ba-95d9-1844961d97ee
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 885336e48d7b8820ac7c1015be6d770b851978af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898076"
---
# <a name="drop-default-transact-sql"></a>DROP DEFAULT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  1 つまたは複数のユーザー定義の既定値を現在のデータベースから削除します。  
  
> [!IMPORTANT]
>  DROP DEFAULT は、次期バージョンの [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では削除される予定です。 新しい開発作業では、DROP DEFAULT の使用は避け、現在これらを使用しているアプリケーションは変更するようにしてください。 代わりに、[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) または [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) の DEFAULT キーワードを使用して作成できるデフォルト定義を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
DROP DEFAULT [ IF EXISTS ] { [ schema_name . ] default_name } [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *IF EXISTS*  
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。  
  
 条件付きでは既に存在する場合にのみ、既定値を削除します。  
  
 *schema_name*  
 デフォルトが所属するスキーマの名前を指定します。  
  
 *default_name*  
 既存の既定値の名前です。 既存のデフォルトの一覧を表示するには、**sp_help** を実行します。 デフォルトは、[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従っている必要があります。 デフォルトのスキーマ名の指定は省略可能です。  
  
## <a name="remarks"></a>Remarks  
 デフォルトが列または別名データ型にバインドされている場合は、デフォルトを削除する前に、**sp_unbindefault** を実行してデフォルトをアンバインドしてください。  
  
 NULL 値が許容される列からデフォルトを削除した後、行を追加しその値を明示的に指定しなかった場合、その位置には NULL が挿入されます。 NOT NULL 列からデフォルトを削除した後、行を追加しその値を明示的に指定しなかった場合は、エラー メッセージが返されます。 これらの行は、通常の INSERT ステートメントの動作の一部として後で追加されます。  
  
## <a name="permissions"></a>アクセス許可  
 DROP DEFAULT を実行するには、少なくとも、デフォルトが属するスキーマに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-dropping-a-default"></a>A. デフォルトを削除する  
 既定値が列または別名データ型にバインドされていない場合は、DROP DEFAULT を使うだけで削除できます。 次の例では、ユーザーが作成したデフォルト `datedflt` を削除します。  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
         WHERE name = 'datedflt'   
            AND type = 'D')  
   DROP DEFAULT datedflt;  
GO  
```  
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、次の構文を使うことができます。  
  
```  
DROP DEFAULT IF EXISTS datedflt;  
GO  
```  
  
### <a name="b-dropping-a-default-that-has-been-bound-to-a-column"></a>B. 列にバインドされた既定値を削除する  
 次の例では、`EmergencyContactPhone` テーブルの `Contact` 列に関連付けられているデフォルトをアンバインドし、デフォルト `phonedflt` を削除します。  
  
```  
USE AdventureWorks2012;  
GO  
   BEGIN   
      EXEC sp_unbindefault 'Person.Contact.Phone'  
      DROP DEFAULT phonedflt  
   END;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_unbindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  
