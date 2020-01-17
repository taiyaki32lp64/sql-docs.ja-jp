---
title: APP_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- APP_NAME_TSQL
- APP_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- name checking for current session [SQL Server]
- sessions [SQL Server], application names
- applications [SQL Server], names
- current session application names
- APP_NAME function
ms.assetid: e491e192-9b30-4243-bc19-33c133fe08a8
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 21b49eb9638b4651ff52c6515f6e5f62177fc504
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843440"
---
# <a name="app_name-transact-sql"></a>APP_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

この関数は、現在のセッションのアプリケーション名の値が設定されている場合、その名前を返します。
  
> [!IMPORTANT]  
>  クライアントからアプリケーション名が提供されますが、`APP_NAME` では、アプリケーション名の値はまったく検証されません。 `APP_NAME` をセキュリティ チェックの一部として使用しないでください。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
  
APP_NAME  ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
**nvarchar(128)**
  
## <a name="remarks"></a>Remarks  
`APP_NAME` は、アプリケーションごとに異なるアクションを実行する手段として、異なるアプリケーションを区別するために使用します。 たとえば、アプリケーションごとに異なる日付形式を使用するために、`APP_NAME` で異なるアプリケーションを区別することができます。 また、特定のアプリケーションに対して情報メッセージを返すこともできます。
  
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] でアプリケーション名を設定する場合、 **[データベース エンジンへの接続]** ダイアログ ボックスで **[オプション]** をクリックします。 **[追加の接続パラメーター]** タブ上で、**app** 属性を `;app='application_name'` 形式で指定します。
  
## <a name="example"></a>例  
この例では、このプロセスを開始したクライアント アプリケーションが `SQL Server Management Studio` セッションかどうかを確認します。 その後、US または ANSI 形式で日付の値を指定します。
  
```sql
USE AdventureWorks2012;  
GO  
IF APP_NAME() = 'Microsoft SQL Server Management Studio - Query'  
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 101) + '.';  
ELSE   
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 102) + '.';  
GO  
```  
  
## <a name="see-also"></a>参照
[システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
[関数](../../t-sql/functions/functions.md)
  
  
