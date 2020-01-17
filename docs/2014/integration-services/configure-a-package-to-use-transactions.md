---
title: トランザクションを使用するパッケージの構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], configuring packages to use
ms.assetid: 8bf14957-27b4-456b-81d9-e1a0e0ca94b7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 16d1f0f4c24f18327ee31da1fb85a74d19588384
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060858"
---
# <a name="configure-a-package-to-use-transactions"></a>トランザクションを使用するようにパッケージを構成する
  トランザクションを使用するようにパッケージを構成する場合、次の 2 つのオプションがあります。  
  
-   パッケージで 1 つのトランザクションを使用する。 この場合、このトランザクションを *開始* するのはパッケージ自体で、パッケージ内の個々のタスクやコンテナーはこの 1 つのトランザクションに参加します。  
  
-   パッケージで複数のトランザクションを使用する。 この場合、パッケージでトランザクションがサポートされますが、トランザクションを実際に開始するのはパッケージ内のタスクやコンテナーになります。  
  
 次の手順では、これらの 2 つのオプションを構成する方法について説明します。  
  
## <a name="configuring-a-single-transaction"></a>1 つのトランザクションの構成  
 このオプションでは、パッケージ自体が 1 つのトランザクションを開始します。 パッケージの TransactionOption プロパティを設定して、このトランザクションを開始するパッケージを構成する`Required`します。  
  
 次に、この 1 つのトランザクションに特定のタスクやコンテナーを参加させます。 そのタスクまたはコンテナーの TransactionOption プロパティを設定する、タスクまたはコンテナーがトランザクションに参加させる`Supported`します。  
  
#### <a name="to-configure-a-package-to-use-a-single-transaction"></a>1 つのトランザクションを使用するようにパッケージを構成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、トランザクションを使用するように構成するパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。  
  
4.  制御フローのデザイン画面の背景で任意の場所を右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **プロパティ**ウィンドウ、TransactionOption プロパティを設定`Required`します。  
  
6.  **[制御フロー]** タブのデザイン画面で、トランザクションに登録するタスクまたはコンテナーを右クリックし、 **[プロパティ]** をクリックします。  
  
7.  **プロパティ**ウィンドウ、TransactionOption プロパティを設定`Supported`します。  
  
    > [!NOTE]  
    >  トランザクションに接続を登録するには、トランザクションで接続を使用するタスクを登録します。 詳細については、「[Integration Services (SSIS) の接続](connection-manager/integration-services-ssis-connections.md)」を参照してください。  
  
8.  トランザクションに登録する各タスクおよびコンテナーに対して、手順 6. と 7. を繰り返します。  
  
## <a name="configuring-multiple-transactions"></a>複数のトランザクションの構成  
 このオプションでは、パッケージでトランザクションがサポートされますが、パッケージ自体はトランザクションを開始しません。 パッケージの TransactionOption プロパティを設定してトランザクションをサポートするためにパッケージを構成する`Supported`します。  
  
 次に、トランザクションを開始するかトランザクションに参加するように、パッケージ内の目的のタスクおよびコンテナーを構成します。 そのタスクまたはコンテナーの TransactionOption プロパティを設定するタスクまたはトランザクションを開始するためのコンテナーを構成する`Required`します。  
  
#### <a name="to-configure-a-package-to-use-multiple-transactions"></a>複数のトランザクションを使用するようにパッケージを構成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、複数のトランザクションを使用するように構成するパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。  
  
4.  制御フローのデザイン画面の背景で任意の場所を右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **プロパティ**ウィンドウ、TransactionOption プロパティを設定`Supported`します。  
  
    > [!NOTE]  
    >  パッケージでトランザクションがサポートされますが、トランザクションは、パッケージ内のタスクまたはコンテナーによって開始されます。  
  
6.  **[制御フロー]** タブのデザイン画面で、トランザクションを開始するパッケージ内のタスクまたはコンテナーを右クリックし、 **[プロパティ]** をクリックします。  
  
7.  **プロパティ**ウィンドウ、TransactionOption プロパティを設定`Required`します。  
  
8.  トランザクションがコンテナーによって開始される場合、トランザクションに登録するタスクまたはコンテナーを右クリックし、 **[プロパティ]** をクリックします。  
  
9. **プロパティ**ウィンドウ、TransactionOption プロパティを設定`Supported`します。  
  
    > [!NOTE]  
    >  トランザクションに接続を登録するには、トランザクションで接続を使用するタスクを登録します。 詳細については、「[Integration Services &#40;SSIS&#41; の接続](connection-manager/integration-services-ssis-connections.md)」を参照してください。  
  
10. トランザクションを開始する各タスクおよびコンテナーに対して、手順 6. ～ 9. を繰り返します。  
  
## <a name="see-also"></a>参照  
 [Integration Services のトランザクション](integration-services-transactions.md)  
  
  
