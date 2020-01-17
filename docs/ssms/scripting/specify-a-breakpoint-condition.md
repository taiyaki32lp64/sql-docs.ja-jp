---
title: ブレークポイント条件の指定 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoint conditions
ms.assetid: b43d8a2b-99a3-4fb7-8848-99c042ea7ef7
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c0baa1c31db1c3b242bde8e4bda39fda5439ddff
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267711"
---
# <a name="specify-a-breakpoint-condition"></a>ブレークポイント条件の指定
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  ブレークポイント条件は、ブレークポイントに達したときにデバッガーによって評価される [!INCLUDE[tsql](../../includes/tsql-md.md)] 式です。 指定したヒット カウントに達し、指定したブレークポイントの条件が満たされると、デバッガーはブレークポイントに指定されたアクションを実行するか、中断します。  
  
## <a name="specifying-conditions"></a>条件の指定  
 指定する式は、ブール値に評価される有効な Transact-SQL 式である必要があります。 詳細については、「[式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)」を参照してください。  
  
 無効な構文でブレークポイント条件を指定した場合は、警告メッセージがすぐに表示されます。 構文は有効でも無効なセマンティクスの条件を指定すると、最初にブレークポイントにヒットしたときに警告メッセージが表示されます。 どちらの場合にも、無効なブレークポイントにヒットしたときにデバッガーの実行が中断されます。  
  
#### <a name="to-specify-a-condition"></a>条件を指定するには  
  
1.  エディター ウィンドウで、ブレークポイント グリフを右クリックし、ショートカット メニューの **[条件]** をクリックします。  
  
     \- または -  
  
     **[ブレークポイント]** ウィンドウで、ブレークポイント グリフを右クリックし、ショートカット メニューの **[条件]** をクリックします。  
  
2.  **[ブレークポイントの条件]** ダイアログ ボックスで、 **[条件]** ボックスに有効なブール式を入力します。  
  
3.  式が **true** に評価されたときにブレークするようにする場合は、 **[true の場合]** を選択します。式の値が変更されたときにブレークするようにする場合は、 **[変更された場合]** を選択します。  
  
    > [!NOTE]  
    >  デバッガーは、初めてブレークポイントに達するまでブール式を評価しません。 **[変更された場合]** を選択した場合、デバッガーは最初の評価を変更とは見なさないため、最初の評価でブレークすることはありません。  
  
## <a name="see-also"></a>参照  
 [ヒット カウントの指定](../../relational-databases/scripting/specify-a-hit-count.md)   
 [ブレークポイント アクションの指定](../../relational-databases/scripting/specify-a-breakpoint-action.md)  
