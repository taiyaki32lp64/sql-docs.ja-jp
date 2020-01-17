---
title: ダイアログ ボックスをパラメーター化 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.parameter.f1
ms.assetid: fac02b6d-d247-447a-8940-e8700c7ac350
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7d60820ba7c384347aeeec80d8c41f934078eca8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056872"
---
# <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
  **[パラメーター化]** ダイアログ ボックスでは、新規または既存のパラメーターをタスクのプロパティと関連付けることができます。 このダイアログ ボックスを開くには、[!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーでタスクまたは [制御フロー] タブを右クリックし、 **[パラメーター化]** をクリックします。 次の一覧では、このダイアログ ボックスの UI 要素について説明します。 パラメーターについて詳しくは、「[Integration Services &#40;SSIS&#41; パラメーター](integration-services-ssis-package-and-project-parameters.md)」をご覧ください。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 **プロパティ**  
 パラメーターと関連付けるタスクのプロパティを選択します。 この一覧には、パラメーター化できるすべてのプロパティが表示されます。  
  
 **既存のパラメーターを使用する**  
 タスクのプロパティを既存のパラメーターと関連付けるには、このオプションを選択し、ドロップダウン リストからパラメーターを選択します。  
  
 **パラメーターを使用しない**  
 パラメーターへの参照を削除するには、このオプションを選択します。 パラメーターは削除されません。  
  
 **新しいパラメーターを作成する**  
 タスクのプロパティと関連付ける新しいパラメーターを作成するには、このオプションを選択します。  
  
 **名前**  
 作成するパラメーターの名前を指定します。  
  
 **[説明]**  
 パラメーターの説明を指定します。  
  
 **[値]**  
 パラメーターの既定値を指定します。 これは設計上の既定値とも呼ばれ、後で配置時にオーバーライドできます。  
  
 **Scope**  
 パラメーターのスコープとして、 **[プロジェクト]** または **[パッケージ]** オプションを指定します。 プロジェクト パラメーターは、プロジェクトが受け取る外部入力をプロジェクト内の 1 つまたは複数のパッケージに指定するために使用します。 パッケージ パラメーターを使用すると、パッケージを編集したり再配置したりせずにパッケージ実行を変更できます。  
  
 **機密**  
 チェック ボックスをオンまたはオフにして、パラメーターが機密かどうかを指定します。 機密性の高いパラメーター値はカタログ内で暗号化され、Transact-SQL または SQL Server Management Studio で表示する際は NULL 値として表示されます。  
  
 **必須**  
 パッケージを実行する前に、設計上の既定値以外の値をパラメーターに設定する必要があるかどうかを指定します。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
  
