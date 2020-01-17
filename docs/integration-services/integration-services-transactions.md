---
title: Integration Services のトランザクション | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], transactions
- transactions [Integration Services], about transactions in packages
- tasks [Integration Services], transactions
- transactions [Integration Services]
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 90855baaa61e242488a7fb6a91a52e34d77e5f48
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284410"
---
# <a name="integration-services-transactions"></a>Integration Services のトランザクション

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  パッケージではトランザクションを使用して、タスクがアトミック単位で実行するデータベース処理をバインドし、この処理によってデータの整合性を保ちます。 すべての種類の [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] コンテナー (パッケージ、For ループ コンテナー、Foreach ループ コンテナー、シーケンス コンテナー、タスクをカプセル化するタスク ホスト) でトランザクションを使用するように設定できます。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、トランザクションを設定するオプションとして、**NotSupported**、**Supported**、**Required** の 3 つが用意されています。  
  
-   **Required** は、親コンテナーで既に開始されているトランザクションがない限り、コンテナーでトランザクションを開始するように指定します。 開始されているトランザクションが存在する場合は、トランザクションが結合されます。 たとえば、トランザクションをサポートするように設定されていないパッケージに **Required** オプションが設定されたシーケンス コンテナーが含まれている場合、シーケンス コンテナーは固有のトランザクションを開始します。 パッケージが **Required** オプションを使用するように設定されている場合、シーケンス コンテナーはパッケージのトランザクションを結合します。  
  
-   **Supported** は、コンテナーがトランザクションを開始せず、親コンテナーが開始したトランザクションを結合するように指定します。 たとえば、4 つの SQL 実行タスクがあるパッケージでトランザクションが開始され、4 つのタスクすべてに **Supported** オプションが設定されている場合、いずれかのタスクが失敗すると、SQL 実行タスクで実行されたデータベース更新すべてがロールバックされます。 パッケージでトランザクションが開始されない場合、4 つの SQL 実行タスクはトランザクションによってバインドされないため、失敗したタスクで実行されたデータベース更新以外はロールバックされません。  
  
-   **NotSupported** は、コンテナーがトランザクションを開始せず、既存のトランザクションも結合しないように指定します。 親コンテナーで開始されたトランザクションは、トランザクションをサポートしないように設定された子コンテナーに影響を与えません。 たとえば、トランザクションを開始するように設定されたパッケージに **NotSupported** オプションが設定された For ループ コンテナーが含まれていた場合、For ループのタスクが失敗してもロールバックは行われません。  
  
 トランザクションの設定は、コンテナーの TransactionOption プロパティで設定します。 このプロパティは、 **の [** プロパティ [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]] ウィンドウを使用して、またはプログラムによって設定できます。  
  
> [!NOTE]  
>  **TransactionOption** プロパティは、コンテナーによって要求された **IsolationLevel** プロパティの値が適用されるかどうかに影響します。 詳細については、 **「パッケージのプロパティの設定」** の [IsolationLevel](../integration-services/set-package-properties.md)プロパティの説明を参照してください。  
  
## <a name="configure-a-package-to-use-transactions"></a>トランザクションを使用するようにパッケージを構成する
トランザクションを使用するようにパッケージを構成する場合、次の 2 つのオプションがあります。  
  
-   パッケージで 1 つのトランザクションを使用する。 この場合、このトランザクションを *開始* するのはパッケージ自体で、パッケージ内の個々のタスクやコンテナーはこの 1 つのトランザクションに参加します。  
  
-   パッケージで複数のトランザクションを使用する。 この場合、パッケージでトランザクションがサポートされますが、トランザクションを実際に開始するのはパッケージ内のタスクやコンテナーになります。  
  
 次の手順では、これらの 2 つのオプションを構成する方法について説明します。  
  
### <a name="configure-a-package-to-use-a-single-transaction"></a>1 つのトランザクションを使用するようにパッケージを構成する  
 このオプションでは、パッケージ自体が 1 つのトランザクションを開始します。 このトランザクションを開始するようにパッケージを構成するには、パッケージの TransactionOption プロパティを **[必須]** に設定します。  
  
 次に、この 1 つのトランザクションに特定のタスクやコンテナーを参加させます。 トランザクションにタスクまたはコンテナーを参加させるには、該当するタスクまたはコンテナーの TransactionOption プロパティを **[Supported (サポートあり)]** に設定します。  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、トランザクションを使用するように構成するパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。  
  
4.  制御フローのデザイン画面の背景で任意の場所を右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[プロパティ]** ウィンドウで、TransactionOption プロパティを **[必須]** に設定します。  
  
6.  **[制御フロー]** タブのデザイン画面で、トランザクションに登録するタスクまたはコンテナーを右クリックし、 **[プロパティ]** をクリックします。  
  
7.  **[プロパティ]** ウィンドウで、TransactionOption プロパティを **[Supported (サポートあり)]** に設定します。  
  
    > [!NOTE]  
    >  トランザクションに接続を登録するには、トランザクションで接続を使用するタスクを登録します。 詳細については、「[Integration Services (SSIS) の接続](../integration-services/connection-manager/integration-services-ssis-connections.md)」を参照してください。  
  
8.  トランザクションに登録する各タスクおよびコンテナーに対して、手順 6. と 7. を繰り返します。  
  
### <a name="configure-a-package-to-use-multiple-transactions"></a>複数のトランザクションを使用するようにパッケージを構成する  
 このオプションでは、パッケージでトランザクションがサポートされますが、パッケージ自体はトランザクションを開始しません。 トランザクションをサポートするようにパッケージを構成するには、パッケージの TransactionOption プロパティを **[Supported (サポートあり)]** に設定します。  
  
 次に、トランザクションを開始するかトランザクションに参加するように、パッケージ内の目的のタスクおよびコンテナーを構成します。 トランザクションを開始するようにタスクまたはコンテナーを構成するには、該当するタスクまたはコンテナーの TransactionOption プロパティを **[必須]** に設定します。   
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、複数のトランザクションを使用するように構成するパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。  
  
4.  制御フローのデザイン画面の背景で任意の場所を右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[プロパティ]** ウィンドウで、TransactionOption プロパティを **[Supported (サポートあり)]** に設定します。  
  
    > [!NOTE]  
    >  パッケージでトランザクションがサポートされますが、トランザクションは、パッケージ内のタスクまたはコンテナーによって開始されます。  
  
6.  **[制御フロー]** タブのデザイン画面で、トランザクションを開始するパッケージ内のタスクまたはコンテナーを右クリックし、 **[プロパティ]** をクリックします。  
  
7.  **[プロパティ]** ウィンドウで、TransactionOption プロパティを **[必須]** に設定します。  
  
8.  トランザクションがコンテナーによって開始される場合、トランザクションに登録するタスクまたはコンテナーを右クリックし、 **[プロパティ]** をクリックします。  
  
9. **[プロパティ]** ウィンドウで、TransactionOption プロパティを **[Supported (サポートあり)]** に設定します。  
  
    > [!NOTE]  
    >  トランザクションに接続を登録するには、トランザクションで接続を使用するタスクを登録します。 詳細については、「[Integration Services &#40;SSIS&#41; の接続](../integration-services/connection-manager/integration-services-ssis-connections.md)」を参照してください。  
  
10. トランザクションを開始する各タスクおよびコンテナーに対して、手順 6. ～ 9. を繰り返します。  

## <a name="multiple-transactions-in-a-package"></a>パッケージ内の複数のトランザクション
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージでは、関連しないトランザクションをパッケージに含めることができます。 入れ子になったコンテナー階層の中間にあるコンテナーでトランザクションがサポートされない場合、階層の上位または下位にあるコンテナーがトランザクションをサポートするように構成されている場合はそのコンテナーで別個のトランザクションが開始されます。 トランザクションは、入れ子になったコンテナー階層において最も内側のタスクから順にパッケージにコミットまたはロールバックされます。 ただし、内側のトランザクションがコミットされた後、その外側のトランザクションが中止された場合は、内側のトランザクションをロールバックできません。  
  
### <a name="example-of-multiple-transactions-in-a-package"></a>パッケージ内の複数のトランザクションの例 
 たとえば、パッケージにシーケンス コンテナーが含まれていて、このコンテナーは、それぞれの 2 つの SQL 実行タスクを含む 2 つの Foreach ループ コンテナーを保持しているとします。 シーケンス コンテナーはトランザクションをサポートします。Foreach ループ コンテナーはトランザクションをサポートしませんが、SQL 実行タスクはサポートします。 この例では、各 SQL 実行タスクでそれぞれのトランザクションが開始され、シーケンス タスクのトランザクションが中止されてもロールバックされません。  
  
 この場合、シーケンス コンテナーの TransactionOption プロパティ、Foreach ループ コンテナー、および SQL 実行タスクを次のように設定します。  
  
-   シーケンス コンテナーの TransactionOption プロパティを **[Required]** に設定します。  
  
-   Foreach ループ コンテナーの TransactionOption プロパティを **[NotSupported]** に設定します。  
  
-   SQL 実行タスクの TransactionOption プロパティを **[Required]** に設定します。  
  
 次の図は、パッケージ内の 5 つの関連しないトランザクションを示しています。 1 つのトランザクションはシーケンス コンテナーによって開始され、4 つのトランザクションは SQL 実行タスクによって開始されます。  
  
 ![複数のトランザクションの実装](../integration-services/media/mw-dts-trans2.gif "複数のトランザクションの実装")  
 
## <a name="inherited-transactions"></a>トランザクションの継承
 パッケージでパッケージ実行タスクを使用して、別のパッケージを実行できます。 パッケージ実行タスクで実行される子パッケージでは、独自のパッケージ トランザクションを作成する場合もあれば、親パッケージのトランザクションを継承する場合もあります。  
  
 次の 2 つの条件に該当する場合、パッケージは親パッケージのトランザクションを継承します。  
  
-   パッケージがパッケージ実行タスクによって呼び出される。  
  
-   パッケージを呼び出すパッケージ実行タスクも、親パッケージのトランザクションに参加している。  
  
 子パッケージ自身がトランザクションに参加していなければ、子パッケージのコンテナーやタスクは親パッケージのトランザクションに参加できません。  
  
### <a name="example-of-inherited-transactions"></a>トランザクションの継承フローの例  
 次の図には、3 個のパッケージがあり、すべてトランザクションを使用します。 各パッケージには、複数のタスクが含まれています。 トランザクションの動作がわかりやすいように、パッケージ実行タスクは 1 つだけ示されています。 パッケージ A がパッケージ B および C を実行します。次に、パッケージ B がパッケージ D および E を実行し、パッケージ C がパッケージ F を実行します。  
  
 パッケージとタスクのトランザクション属性は次のとおりです。  
  
-   パッケージ A および C の**TransactionOption** は **Required** に設定されています。  
  
-   パッケージ B と D、およびパッケージ実行タスク B、パッケージ実行タスク D、パッケージ実行タスク F の**TransactionOption** は **Supported** に設定されています。  
  
-   パッケージ E、およびパッケージ実行タスク C、パッケージ実行タスク E の**TransactionOption** は **NotSupported** に設定されています。  
  
 ![トランザクションの継承のフロー](../integration-services/media/mw-dts-executepack.gif "トランザクションの継承のフロー")  
  
 パッケージ B、D、および F のみが親パッケージのトランザクションを継承できます。  
  
 パッケージ B および D は、パッケージ A が開始したトランザクションを継承します。  
  
 パッケージ F はパッケージ C が開始したトランザクションを継承します。  
  
 パッケージ A および C は独自のトランザクションを制御します。  
  
 パッケージ E はトランザクションを使用しません。  
 
  
## <a name="external-resources"></a>外部リソース  
  
-   www.mssqltips.com のブログ [「SQL Server Integration Services (SSIS) でトランザクションを使用する方法」](https://go.microsoft.com/fwlink/?LinkId=157783)  
  
## <a name="see-also"></a>参照  
 [トランザクションの継承](https://msdn.microsoft.com/library/90db5564-d41e-4cfe-8c9e-4e68d41eff1c)   
 [複数のトランザクション](https://msdn.microsoft.com/library/c3664a94-be89-40c0-a3a0-84b74a7fedbe)  
  
  
