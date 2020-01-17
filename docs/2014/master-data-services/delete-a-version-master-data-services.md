---
title: バージョンを削除する (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- versions [Master Data Services], deleting
- deleting versions [Master Data Services]
ms.assetid: 2a4eeffe-8379-4744-ad44-c27d8c8ac9a8
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 1e9f8d65e1a835af954952a64322f21a484a16f3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483340"
---
# <a name="delete-a-version-master-data-services"></a>バージョンを削除する (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で、バージョンに関連付けられたマスター データが確実に不要になった場合には、そのバージョンを削除します。 バージョンを削除した後、関連するマスター データを取得することはできません。  
  
> [!WARNING]  
>  モデルにバージョンが 1 つしかない場合にそのバージョンを削除すると、モデルは使用できなくなります。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースで mdm.viw_SYSTEM_SCHEMA_VERSION ビューを表示して mds.udpVersionDelete ストアド プロシージャを実行するための権限が必要です。 詳細については、「[データベース オブジェクト セキュリティ (マスター データ サービス)](database-object-security-master-data-services.md)」を参照してください。  
  
### <a name="to-delete-a-version"></a>バージョンを削除するには  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を開き、 [!INCLUDE[ssDE](../includes/ssde-md.md)] データベースの [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] インスタンスに接続します。  
  
2.  mdm.viw_SYSTEM_SCHEMA_VERSION ビューを開きます。  
  
3.  削除するモデルのバージョンを見つけ、 **ID** フィールドの値をコピーします。  
  
4.  新しいクエリを作成します。  
  
5.  次のテキストを入力します。その場合、 *version_ID* を手順 2 でコピーした値で置き換えます。  
  
    ```  
    EXEC [mdm].[udpVersionDelete] @Version_ID='version_ID'  
    ```  
  
6.  クエリを実行します。  
  
    > [!NOTE]  
    >  Web アプリケーションに変更が反映されるまで数分かかる場合があります。  
  
## <a name="see-also"></a>関連項目  
 [バージョン (マスター データ サービス)](../../2014/master-data-services/versions-master-data-services.md)   
 [バージョンをコピーする (マスター データ サービス)](../../2014/master-data-services/copy-a-version-master-data-services.md)  
  
  
