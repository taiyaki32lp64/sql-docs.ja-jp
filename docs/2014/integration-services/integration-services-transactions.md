---
title: Integration Services のトランザクション | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], transactions
- transactions [Integration Services], about transactions in packages
- tasks [Integration Services], transactions
- transactions [Integration Services]
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b0359ca10e7279f4a80bec082a8e049f4641c9b2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767634"
---
# <a name="integration-services-transactions"></a>Integration Services のトランザクション
  パッケージではトランザクションを使用して、タスクがアトミック単位で実行するデータベース処理をバインドし、この処理によってデータの整合性を保ちます。 すべての種類の [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] コンテナー (パッケージ、For ループ コンテナー、Foreach ループ コンテナー、シーケンス コンテナー、タスクをカプセル化するタスク ホスト) でトランザクションを使用するように設定できます。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、トランザクションを設定するオプションとして、**NotSupported**、**Supported**、**Required** の 3 つが用意されています。  
  
-   **Required** は、親コンテナーで既に開始されているトランザクションがない限り、コンテナーでトランザクションを開始するように指定します。 開始されているトランザクションが存在する場合は、トランザクションが結合されます。 たとえば、トランザクションをサポートするように設定されていないパッケージに **Required** オプションが設定されたシーケンス コンテナーが含まれている場合、シーケンス コンテナーは固有のトランザクションを開始します。 パッケージが **Required** オプションを使用するように設定されている場合、シーケンス コンテナーはパッケージのトランザクションを結合します。  
  
-   **Supported** は、コンテナーがトランザクションを開始せず、親コンテナーが開始したトランザクションを結合するように指定します。 たとえば、4 つの SQL 実行タスクがあるパッケージでトランザクションが開始され、4 つのタスクすべてに **Supported** オプションが設定されている場合、いずれかのタスクが失敗すると、SQL 実行タスクで実行されたデータベース更新すべてがロールバックされます。 パッケージでトランザクションが開始されない場合、4 つの SQL 実行タスクはトランザクションによってバインドされないため、失敗したタスクで実行されたデータベース更新以外はロールバックされません。  
  
-   **NotSupported** は、コンテナーがトランザクションを開始せず、既存のトランザクションも結合しないように指定します。 親コンテナーで開始されたトランザクションは、トランザクションをサポートしないように設定された子コンテナーに影響を与えません。 たとえば、トランザクションを開始するように設定されたパッケージに **NotSupported** オプションが設定された For ループ コンテナーが含まれていた場合、For ループのタスクが失敗してもロールバックは行われません。  
  
 トランザクションの設定は、コンテナーの TransactionOption プロパティで設定します。 このプロパティは、 **の [** プロパティ [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]] ウィンドウを使用して、またはプログラムによって設定できます。  
  
> [!NOTE]  
>  `TransactionOption` プロパティは、コンテナーによって要求された `IsolationLevel` プロパティの値が適用されるかどうかに影響します。 詳細については、の説明を参照して、`IsolationLevel`プロパティのトピック「[パッケージ プロパティの設定](set-package-properties.md)します。  
  
### <a name="to-configure-a-package-to-use-transactions"></a>パッケージでトランザクションを使用するように設定するには  
  
-   [トランザクションを使用するようにパッケージを構成する](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
## <a name="external-resources"></a>外部リソース  
  
-   www.mssqltips.com のブログ [「SQL Server Integration Services (SSIS) でトランザクションを使用する方法」](https://go.microsoft.com/fwlink/?LinkId=157783)  
  
## <a name="see-also"></a>参照  
 [トランザクションの継承](../../2014/integration-services/inherited-transactions.md)   
 [複数のトランザクション](../../2014/integration-services/multiple-transactions.md)  
  
  
