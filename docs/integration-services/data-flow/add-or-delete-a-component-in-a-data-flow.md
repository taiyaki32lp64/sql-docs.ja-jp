---
title: データ フローでコンポーネントを追加または削除する | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- adding components
- components [Integration Services], data flow
ms.assetid: d99124f9-0994-4f40-a48e-fdca6a4383e7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6123a670053f5e6fa4b9c7196c9bc503b97c855b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293505"
---
# <a name="add-or-delete-a-component-in-a-data-flow"></a>データ フローでコンポーネントを追加または削除する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  データ フロー コンポーネントとは、データ フロー内の変換元、変換、および変換先のことです。 コンポーネントをデータ フローに追加するには、データ フロー タスクを事前にパッケージ制御フローに含める必要があります。  
  
 次の手順では、パッケージのデータ フローでコンポーネントを追加または削除する方法について説明します。  
  
### <a name="to-add-a-component-to-a-data-flow"></a>データ フローにコンポーネントを追加するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックし、コンポーネントを追加するデータ フローが含まれているデータ フロー タスクをダブルクリックします。  
  
4.  ツールボックスで、 **[データ フローの変換元]** 、 **[データ フロー変換]** 、または **[データ フローの変換先]** を展開し、次にデータ フロー アイテムを **[データ フロー]** タブのデザイン画面にドラッグします。  
  
5.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="to-delete-a-component-from-a-data-flow"></a>データ フローからコンポーネントを削除するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックし、コンポーネントを削除するデータ フローが含まれているデータ フロー タスクをダブルクリックします。  
  
4.  データ フロー コンポーネントを右クリックし、 **[削除]** をクリックします。  
  
5.  削除操作を確認します。  
  
6.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [データ フロー内でコンポーネントを連結する](../../integration-services/data-flow/connect-components-in-a-data-flow.md)   
 [データ フローのデバッグ](../../integration-services/troubleshooting/debugging-data-flow.md)   
 [データ フロー](../../integration-services/data-flow/data-flow.md)  
  
  
