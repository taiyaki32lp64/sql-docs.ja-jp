---
title: パブリケーションでのアーティクルの追加および削除 (SSMS)
description: SQL Server Management Studio (SSMS) を使用して、パブリケーションでアーティクルを追加およびアーティクルを削除する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
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
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 682f0af6b7ac2c6dffc8d0e1988ef2973b2f7b51
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321311"
---
# <a name="add-articles-to-and-drop-articles-from-a-publication"></a>パブリケーションでのアーティクルの追加および削除
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  パブリケーションの新規作成ウィザードでパブリケーションを作成する場合は、最初にアーティクルを追加します。 このウィザードの使用の詳細については、「[パブリケーションの作成](../../../relational-databases/replication/publish/create-a-publication.md)」を参照してください。  
  
 パブリケーションの作成後、 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[アーティクル]** ページでアーティクルを追加または削除します。 このダイアログ ボックスへのアクセス方法の詳細については、「[パブリケーション プロパティの表示および変更](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」を参照してください。 アーティクルの追加と削除に関する注意点については、「[既存のパブリケーションでのアーティクルの追加および削除](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)」を参照してください。  
  
### <a name="to-add-an-article-after-a-publication-is-created"></a>パブリケーションの作成後にアーティクルを追加するには  
  
1.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[アーティクル]** ページで、 **[チェック ボックスがオンのオブジェクトのみ一覧に表示する]** チェック ボックスをオフにします。 これにより、パブリケーション データベース内のパブリッシュされていないオブジェクトも表示されるようになります。  
  
2.  追加する各アーティクルの隣にあるチェック ボックスをオンにします。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-an-article"></a>アーティクルを削除するには  
  
1.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[アーティクル]** ページで、削除するアーティクルの隣にあるチェック ボックスをオフにします。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)   
 [データとデータベース オブジェクトのパブリッシュ](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
