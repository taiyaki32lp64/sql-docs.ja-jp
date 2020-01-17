---
title: CDC インスタンスのプロパティを表示する方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4bce9b82-7bbd-41df-b3f4-4b40b8bad474
author: chugugrace
ms.author: chugu
ms.openlocfilehash: eaf4308f05b7a7fb1f450947754736d0cf565b61
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294671"
---
# <a name="how-to-view-the-cdc-instance-properties"></a>CDC インスタンスのプロパティを表示する方法

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  この手順では、インスタンスの操作を管理するために作成するインスタンスの情報を、CDC デザイナー コンソールを使用して表示する方法について説明します。  
  
### <a name="to-view-information-about-a-specific-instance"></a>特定のインスタンスに関する情報を表示するには  
  
1.  **[スタート]** メニューの **[CDC デザイナー コンソール]** をクリックします。  
  
2.  左側のペインで **[Change Data Capture]** を展開し、表示するインスタンスが含まれているサービスを展開します。  
  
3.  操作するインスタンスの名前を選択します。  
  
     インスタンスに関する情報は、CDC デザイナー コンソールの中央部分に表示されます。 この部分は 4 つのタブに分かれています。 タブはいずれも読み取り専用です。  
  
     **ステータス**  
     このタブには、インスタンスの変更データ キャプチャの現在の状態に関する情報が表示されます。 このタブに表示される内容の詳細については、「 **Manage a CDC Instance** 」の「 [ビューアーのタブ](../../integration-services/change-data-capture/manage-a-cdc-instance.md)」を参照してください。  
  
     **Oracle**  
     このタブには、CDC インスタンスと Oracle ソース データベースに関する一般的な情報が表示されます。 このタブに表示される内容の詳細については、「 [Edit the Oracle Database Properties](../../integration-services/change-data-capture/edit-the-oracle-database-properties.md)」を参照してください。  
  
     **テーブル**  
     このタブには、変更データ キャプチャに含まれるテーブルに関する情報が表示されます。 キャプチャされる列も表示されます。 このタブに表示される内容の詳細については、「 [Edit Tables](../../integration-services/change-data-capture/edit-tables.md)」を参照してください。  
  
     **詳細設定**  
     このタブには、プロパティ エディターで定義する詳細プロパティの一覧が表示されます。 このタブに表示される内容の詳細については、「 [Edit the Advanced Properties](../../integration-services/change-data-capture/edit-the-advanced-properties.md)」を参照してください。  
  
  
