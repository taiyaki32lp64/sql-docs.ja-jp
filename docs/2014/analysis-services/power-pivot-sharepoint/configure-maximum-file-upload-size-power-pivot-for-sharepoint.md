---
title: ファイルの最大アップロード サイズ (PowerPivot for SharePoint) の構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ac516c63-1e79-4ae8-bca6-32d3c1a09c00
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3b6e367d0bc73de31f46b8533cded824bdb19504
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071823"
---
# <a name="configure-maximum-file-upload-size-powerpivot-for-sharepoint"></a>アップロードするファイルの最大サイズの構成 (PowerPivot for SharePoint)
  PowerPivot ブックには大量のデータが含まれる場合が多く、SharePoint のアップロードで許容されるファイルの最大サイズを超過することがあります。 最大サイズを超過したファイルをアップロードしようとすると、SharePoint で次のエラーが発生します。  
  
-   "指定されたファイルは、サポートされる最大ファイル サイズを超えています。"  
  
 ファイル サイズを増やすには、まず、Excel Services の [ブックの最大サイズ] を 50 MB に調整します。 これにより、Excel に対するファイルの最大サイズの上限が SharePoint Web アプリケーションに対するファイル サイズの上限 (SharePoint 2010 では既定で 50 MB、SharePoint 2013 では既定で 200 MB) と同じになります。 ファイルのサイズが 50 MB を超える場合は、Excel Services と Web アプリケーションの両方についてファイル サイズの上限を増やします。  
  
 ファイルの最大アップロード サイズを変更するには、SharePoint 管理者である必要があります。  
  
### <a name="configure-maximum-file-size-for-excel-services"></a>Excel Services に対するファイルの最大サイズの構成  
  
1.  サーバーの全体管理で、[アプリケーション構成の管理] の **[サービス アプリケーションの管理]** をクリックします。  
  
2.  Excel Services アプリケーションの名前をクリックします。  
  
3.  **[信頼できるファイル保存場所]** をクリックします。  
  
4.  プロパティを編集する場所をクリックします。 既定では、既定の Web アプリケーションは信頼できるサイトと見なされます。 既定の Web アプリケーションを使用している場合は、 **http://** をクリックして、この場所の構成ページを開きます。  
  
5.  **[ブックのプロパティ]** までスクロールします。  
  
6.  [ブックの最大サイズ] で、ファイル サイズを 10 (既定値) から 50、または使用するファイルに対応できるさらに大きい値に増やします。  
  
     既定では、50 MB が SharePoint Web アプリケーションのファイルの最大アップロード サイズです。 [ブックの最大サイズ] を 50 MB よりも大きい値に設定した場合は、次の手順に従って、SharePoint Web アプリケーションの [アップロードの最大サイズ] を同じ値に増やしてください。  
  
     指定できる最大値は 2 GB (またはサーバーの全体管理で指定された 2047 MB) です。  
  
7.  **[OK]** をクリックします。  
  
### <a name="configure-maximum-file-size-for-a-sharepoint-web-application"></a>SharePoint Web アプリケーションに対するファイルの最大サイズの構成  
  
1.  サーバーの全体管理で、[アプリケーション構成の管理] の **[Web アプリケーションの管理]** をクリックします。  
  
    > [!NOTE]  
    >  以下の手順は、Excel Services の [ブックの最大サイズ] を大きい値に設定した場合にのみ実行してください。  
  
2.  アプリケーションを選択します ( **SharePoint -80**など)。  
  
3.  [Web アプリケーション] リボンで、[全般設定] ボタンの下矢印をクリックします。  
  
4.  **[全般設定]** をクリックします。  
  
5.  **[アップロードの最大サイズ]** までスクロールします。  
  
6.  Excel Services の [ブックの最大サイズ] 以上の値にプロパティを設定します。  
  
7.  **[OK]** をクリックします。  
  
  
