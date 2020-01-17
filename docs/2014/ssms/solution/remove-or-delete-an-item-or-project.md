---
title: アイテムやプロジェクトのクリアまたは削除 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting project items
- projects [SQL Server Management Studio], item removal
- removing project items
ms.assetid: 3fd92434-70f5-466e-bef0-7e0fd73ddb1c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dd6d04b186c68b128ad35ec5e5bd8b92ad1541c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63035695"
---
# <a name="remove-or-delete-an-item-or-project"></a>アイテムやプロジェクトのクリアまたは削除
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] プロジェクトに含まれるプロジェクト アイテムには、クエリ、接続、およびその他のファイルがあります。 プロジェクトのクエリとその他のファイルは、記憶域に残したままソリューションからクリアできます。 現在のソリューションでは使用せずに、別のソリューションで使用する場合は、プロジェクトやアイテムをクリアします。  
  
### <a name="to-remove-a-project-item"></a>プロジェクト アイテムをクリアするには  
  
1.  ソリューション エクスプローラーで、クリアするプロジェクト アイテムを選択します。  
  
2.  **[編集]** メニューの **[削除]** をクリックします。  
  
3.  確認ダイアログで **[削除]** をクリックすると、プロジェクトからアイテムが削除されます。  
  
 クリアしたアイテムは、ファイル システムにまだ存在しています。 したがって、クリアしたアイテムは、元のソリューションまたは別のソリューションに追加することができます。  
  
#### <a name="to-remove-a-project"></a>プロジェクトをクリアするには  
  
1.  ソリューション エクスプローラーで、クリアするプロジェクトを選択します。  
  
2.  **[編集]** メニューの **[削除]** をクリックします。  
  
3.  確認ダイアログで **[OK]** をクリックします。ソリューションからプロジェクトがクリアされます。  
  
 プロジェクトは完全に削除できますが、最初に [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ソリューションからプロジェクトへの参照をすべてクリアし、次に [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows エクスプローラーを使用して、関連付けられているファイルを記憶域から完全に削除する必要があります。  
  
#### <a name="to-delete-a-project"></a>プロジェクトを削除するには  
  
1.  ソリューション エクスプローラーで、ソリューションから削除するプロジェクトをクリアします。  
  
2.  Windows エクスプローラーで、削除するプロジェクトまたはアイテムに関連付けられているファイルを検索して選択します。  
  
3.  **[ファイル]** メニューの **[削除]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [ソリューション エクスプ ローラー](solution-explorer.md)   
 [新しい項目をプロジェクトに追加します。](add-new-items-to-a-project.md)   
 [既存の項目をプロジェクトに追加する](add-existing-items-to-a-project.md)  
  
  
