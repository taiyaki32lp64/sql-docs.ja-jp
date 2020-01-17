---
title: 複数のトランザクション |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], multiple
- multiple transactions
ms.assetid: c3664a94-be89-40c0-a3a0-84b74a7fedbe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: da0f932acb2ab97204aeb27c9e077c7fae154987
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057399"
---
# <a name="multiple-transactions"></a>複数のトランザクション
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージでは、関連しないトランザクションをパッケージに含めることができます。 入れ子になったコンテナー階層の中間にあるコンテナーでトランザクションがサポートされない場合、階層の上位または下位にあるコンテナーがトランザクションをサポートするように構成されている場合はそのコンテナーで別個のトランザクションが開始されます。 トランザクションは、入れ子になったコンテナー階層において最も内側のタスクから順にパッケージにコミットまたはロールバックされます。 ただし、内側のトランザクションがコミットされた後、その外側のトランザクションが中止された場合は、内側のトランザクションをロールバックできません。  
  
## <a name="illustration-of-multiple-transactions"></a>複数のトランザクションの図  
 たとえば、パッケージにシーケンス コンテナーが含まれていて、このコンテナーは、それぞれの 2 つの SQL 実行タスクを含む 2 つの Foreach ループ コンテナーを保持しているとします。 シーケンス コンテナーはトランザクションをサポートします。Foreach ループ コンテナーはトランザクションをサポートしませんが、SQL 実行タスクはサポートします。 この例では、各 SQL 実行タスクでそれぞれのトランザクションが開始され、シーケンス タスクのトランザクションが中止されてもロールバックされません。  
  
 この場合、シーケンス コンテナーの TransactionOption プロパティ、Foreach ループ コンテナー、および SQL 実行タスクを次のように設定します。  
  
-   シーケンス コンテナーの TransactionOption プロパティを **[Required]** に設定します。  
  
-   Foreach ループ コンテナーの TransactionOption プロパティを **[NotSupported]** に設定します。  
  
-   SQL 実行タスクの TransactionOption プロパティを **[Required]** に設定します。  
  
 次の図は、パッケージ内の 5 つの関連しないトランザクションを示しています。 1 つのトランザクションはシーケンス コンテナーによって開始され、4 つのトランザクションは SQL 実行タスクによって開始されます。  
  
 ![複数のトランザクションの実装](media/mw-dts-trans2.gif "複数のトランザクションの実装")  
  
## <a name="related-tasks"></a>Related Tasks  
 [トランザクションを使用するようにパッケージを構成する](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
