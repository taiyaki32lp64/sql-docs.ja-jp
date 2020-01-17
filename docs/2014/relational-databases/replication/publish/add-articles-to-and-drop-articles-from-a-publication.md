---
title: アーティクルを追加したり削除パブリケーション (SQL Server Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- dropping articles
- adding articles
- articles [SQL Server replication], adding
ms.assetid: d5a3e536-62d2-4473-a178-877ba52f7d7f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3301be2f0af9960a48602a1b540fa2cac2f39914
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63021363"
---
# <a name="add-articles-to-and-drop-articles-from-a-publication-sql-server-management-studio"></a>パブリケーションでのアーティクルの追加または削除 (SQL Server Management Studio)
  パブリケーションの新規作成ウィザードでパブリケーションを作成する場合は、最初にアーティクルを追加します。 このウィザードの使用の詳細については、「[パブリケーションの作成](create-a-publication.md)」を参照してください。  
  
 パブリケーションの作成後、 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[アーティクル]** ページでアーティクルを追加または削除します。 このダイアログ ボックスへのアクセス方法の詳細については、「[パブリケーション プロパティの表示および変更](view-and-modify-publication-properties.md)」を参照してください。 アーティクルの追加と削除に関する注意点については、「[既存のパブリケーションでのアーティクルの追加および削除](add-articles-to-and-drop-articles-from-existing-publications.md)」を参照してください。  
  
### <a name="to-add-an-article-after-a-publication-is-created"></a>パブリケーションの作成後にアーティクルを追加するには  
  
1.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[アーティクル]** ページで、 **[チェック ボックスがオンのオブジェクトのみ一覧に表示する]** チェック ボックスをオフにします。 これにより、パブリケーション データベース内のパブリッシュされていないオブジェクトも表示されるようになります。  
  
2.  追加する各アーティクルの隣にあるチェック ボックスをオンにします。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-an-article"></a>アーティクルを削除するには  
  
1.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[アーティクル]** ページで、削除するアーティクルの隣にあるチェック ボックスをオフにします。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [アーティクルの定義](define-an-article.md)   
 [データとデータベース オブジェクトのパブリッシュ](publish-data-and-database-objects.md)  
  
  
