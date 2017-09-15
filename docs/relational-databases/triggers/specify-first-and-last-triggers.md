---
title: "最初と最後のトリガーの指定 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- first triggers [SQL Server]
- last triggers
- DML triggers, first or last triggers
- INSTEAD OF triggers
- AFTER triggers
ms.assetid: 9e6c7684-3dd3-46bb-b7be-523b33fae4d5
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 99935796043bf8ea14c32a2f98867ca2c7612a2d
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="specify-first-and-last-triggers"></a>最初と最後のトリガーの指定
  テーブルに関連付けられている AFTER トリガーの 1 つを、INSERT、DELETE、および UPDATE の各トリガー動作に対して起動される、最初の AFTER トリガーまたは最後の AFTER トリガーのいずれかに指定できます。 最初と最後のトリガーの間で起動される AFTER トリガーは、任意の順序で実行されます。  
  
 AFTER トリガーの順序を指定するには、 **sp_settriggerorder** ストアド プロシージャを使用します。 **sp_settriggerorder** には次のオプションがあります。  
  
|オプション|説明|  
|------------|-----------------|  
|**First**|DML トリガーが、トリガー動作に対して起動される最初の AFTER トリガーであることを指定します。|  
|**Last**|DML トリガーが、トリガー動作に対して起動される最後の AFTER トリガーであることを指定します。|  
|**なし**|DML トリガーを起動する特定の順番がないことを指定します。 主に最初または最後のトリガーのいずれかの順序をリセットするときに使用します。|  
  
 次の例は、 **sp_settriggerorder**を使用する例を示しています。  
  
```  
sp_settriggerorder @triggername = 'MyTrigger', @order = 'first', @stmttype = 'UPDATE'  
```  
  
> [!IMPORTANT]  
>  最初のトリガーと最後のトリガーは、2 つの異なる DML トリガーである必要があります。  
  
 テーブルでは、INSERT、UPDATE、および DELETE の各トリガーを同時に定義することができます。 各ステートメントはその型ごとに、固有の最初と最後のトリガーを持つことができますが、最初と最後に同じトリガーを持つことはできません。  
  
 1 つのテーブルに定義された最初のトリガーまたは最後のトリガーが、FOR UPDATE、FOR DELETE、または FOR INSERT などのトリガー動作に対応していない場合は、それらの動作に対する最初のトリガーまたは最後のトリガーを設定できません。  
  
 INSTEAD OF トリガーは最初のトリガーまたは最後のトリガーとして指定できません。 INSTEAD OF トリガーは基になるテーブルが更新される前に起動されるためです。 INSTEAD OF トリガーによって基になるテーブルが更新された場合、テーブルで定義された AFTER トリガーが起動される前に更新が発生します。 たとえば、ビュー上の INSTEAD OF INSERT トリガーによってベース テーブルにデータが挿入され、ベース テーブル自体に INSTEAD OF INSERT トリガーおよび 3 つの AFTER INSERT トリガーが含まれる場合、挿入操作の代わりに、ベース テーブルにある INSTEAD OF INSERT トリガーが起動されます。また、ベース テーブルでの挿入操作の後、ベース テーブルにある AFTER トリガーが起動されます。 詳しくは、「 [DML Triggers](../../relational-databases/triggers/dml-triggers.md)」をご覧ください。  
  
 ALTER TRIGGER ステートメントによって最初のトリガーまたは最後のトリガーが変更された場合、 **First** 属性または **Last** 属性が削除され、順序の値が **None**に設定されます。 **sp_settriggerorder**を使用して順序をリセットする必要があります。  
  
 OBJECTPROPERTY 関数は、トリガーが最初のトリガーであるか、または最後のトリガーであるかを、 **ExecIsFirstTrigger** プロパティおよび **ExecIsLastTrigger**プロパティを使用して示します。  
  
 レプリケーションは、テーブルが即時更新サブスクリプションまたはキュー更新サブスクリプションに含まれる場合、自動的に最初のトリガーを生成します。 レプリケーションのトリガーは最初のトリガーであることが必要です。 レプリケーションでは、最初のトリガーを持つテーブルを即時更新サブスクリプションまたはキュー更新サブスクリプションに含めるよう設定すると、エラーが発生します。 テーブルをサブスクリプションに含めた後、トリガーを最初のトリガーに設定すると、 **sp_settriggerorder** はエラーを返します。 レプリケーション トリガーに ALTER を使用したり、 **sp_settriggerorder** を使用してレプリケーション トリガーを最後のトリガーまたは順序なしのトリガーに変更すると、サブスクリプションは正しく動作しません。  
  
## <a name="see-also"></a>参照  
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_settriggerorder &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md)  
  
  