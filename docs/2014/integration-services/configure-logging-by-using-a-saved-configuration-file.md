---
title: 保存されている構成ファイルを使用してログの構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], logs
- logs [Integration Services], containers
ms.assetid: e5fdbbcb-94ca-4912-aa7c-0d89cebbd308
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b2adc326ef2e0bb593b0532a51a9a677821ae0e2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060602"
---
# <a name="configure-logging-by-using-a-saved-configuration-file"></a>保存されている構成ファイルを使用してログ記録を構成する
  この手順では、以前に保存したログ構成ファイルを読み込んでパッケージ内の新しいコンテナーのログ記録を構成する方法について説明します。  
  
 既定では、パッケージに含まれるすべてのコンテナーは、親コンテナーと同じログ構成を使用します。 たとえば、Foreach ループ内のタスクは、Foreach ループと同じログ構成を使用します。  
  
### <a name="to-configure-logging-for-a-container"></a>コンテナーのログ記録を構成するには  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  次に、 **[SSIS]** メニューの **[ログ記録]** をクリックします。  
  
3.  パッケージ ツリー ビューを展開し、構成するコンテナーを選択します。  
  
4.  **[プロバイダーとログ]** タブで、コンテナーに対して使用するログを選択します。  
  
    > [!NOTE]  
    >  ログは、パッケージ レベルでのみ作成できます。 詳しくは、「 [SQL Server Data Tools でパッケージのログ記録を有効にする](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md)」をご覧ください。  
  
5.  **[詳細]** タブをクリックし、 **[読み込み]** をクリックします。  
  
6.  使用するログ構成ファイルを参照し、 **[開く]** をクリックします。  
  
7.  必要に応じて、 **[イベント]** 列のチェック ボックスをオンにして、ログ記録を行う異なるログ エントリを選択することもできます。 **[詳細設定]** をクリックして、このエントリのログ記録を行うための情報の種類を選択します。  
  
    > [!NOTE]  
    >  最初にログ構成を作成するときに使用されたコンテナーでは使用できない追加のログ エントリが新しいコンテナーに含まれている場合があります。 これらの追加のログ エントリをログに記録するには、手動で選択する必要があります。  
  
8.  **[保存]** をクリックして、ログ構成の更新バージョンを保存します。  
  
9. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; のログ記録](performance/integration-services-ssis-logging.md)  
  
  
