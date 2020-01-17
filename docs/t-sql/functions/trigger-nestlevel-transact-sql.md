---
title: TRIGGER_NESTLEVEL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TRIGGER_NESTLEVEL
- TRIGGER_NESTLEVEL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- triggers [SQL Server], number executed
- number of triggers
- TRIGGER_NESTLEVEL function
ms.assetid: 6a33e74a-0cf9-4ae1-a1e4-4a137a3ea39d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6215824f230001cb9d7add20d32c85780a65ede6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098813"
---
# <a name="triggernestlevel-transact-sql"></a>TRIGGER_NESTLEVEL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  トリガーを起動したステートメントに対して実行されたトリガーの数を返します。 TRIGGER_NESTLEVEL は、DML トリガーおよび DDL トリガーで、現在の入れ子レベルを調べるときに使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
TRIGGER_NESTLEVEL ( [ object_id ] , [ 'trigger_type' ] , [ 'trigger_event_category' ] )  
```  
  
## <a name="arguments"></a>引数  
 *object_id*  
 トリガーのオブジェクト ID です。 *object_id* を指定すると、指定したトリガーがステートメントに対して実行された回数が返されます。 *object_id* を指定しない場合は、そのステートメントに対して実行されたすべてのトリガーの実行回数が返されます。  
  
 **'** *trigger_type* **'**  
 AFTER トリガーと INSTEAD OF トリガーのどちらに TRIGGER_NESTLEVEL を適用するかを指定します。 AFTER トリガーの場合は **AFTER** を指定します。 INSTEAD OF トリガーの場合は **IOT** を指定します。 *trigger_type* を指定するときは *trigger_event_category* も指定する必要があります。  
  
 **'** *trigger_event_category* **'**  
 DML トリガーと DDL トリガーのどちらに TRIGGER_NESTLEVEL を適用するかを指定します。 DML トリガーの場合は **DML** を指定します。 DDL トリガーの場合は **DDL** を指定します。 *trigger_event_category* を指定するときは *trigger_type* も指定する必要があります。 **DDL** の場合は **AFTER** だけを指定できます。DDL トリガーは必ず AFTER トリガーであるためです。  
  
## <a name="remarks"></a>Remarks  
 パラメーターを指定しない場合、TRIGGER_NESTLEVEL は呼び出し履歴上のトリガーの合計数を返します。 この合計数にはそのトリガー自身も含まれます。 トリガーがコマンドを実行することにより、別のトリガーが起動されたり、トリガーを起動するセッションを作成するときはパラメーターを省略できます。  
  
 特定の種類のトリガーおよび特定のイベント カテゴリについて、呼び出し履歴上のトリガーの合計数を返すには、*object_id* に値 0 を指定します。  
  
 TRIGGER_NESTLEVEL をトリガーの外部で実行し、かつ、どのパラメーターも NULL でない場合は、0 が返されます。  
  
 任意のパラメーターに明示的に NULL を指定した場合、TRIGGER_NESTLEVEL をトリガーの内部で使用したか外部で使用したかにかかわらず、値 NULL が返されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-testing-the-nesting-level-of-a-specific-dml-trigger"></a>A. 特定の DML トリガーの入れ子レベルを調べる  
  
```  
IF ( (SELECT TRIGGER_NESTLEVEL( OBJECT_ID('xyz') , 'AFTER' , 'DML' ) ) > 5 )  
   RAISERROR('Trigger xyz nested more than 5 levels.',16,-1)  
```  
  
### <a name="b-testing-the-nesting-level-of-a-specific-ddl-trigger"></a>B. 特定の DDL トリガーの入れ子レベルを調べる  
  
```  
IF ( ( SELECT TRIGGER_NESTLEVEL ( ( SELECT object_id FROM sys.triggers  
WHERE name = 'abc' ), 'AFTER' , 'DDL' ) ) > 5 )  
   RAISERROR ('Trigger abc nested more than 5 levels.',16,-1)  
```  
  
### <a name="c-testing-the-nesting-level-of-all-triggers-executed"></a>C. 実行されたすべてのトリガーの入れ子レベルを調べる  
  
```  
IF ( (SELECT trigger_nestlevel() ) > 5 )  
   RAISERROR  
      ('This statement nested over 5 levels of triggers.',16,-1)  
```  
  
## <a name="see-also"></a>参照  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
