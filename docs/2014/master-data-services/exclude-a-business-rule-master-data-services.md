---
title: ビジネス ルールを除外する (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], excluding
ms.assetid: bdbc9df0-23f7-40b9-8aba-4445c1482580
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8f18e047b11bee4093ce7a6e494c1ae1bf3d0ada
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483385"
---
# <a name="exclude-a-business-rule-master-data-services"></a>ビジネス ルールを除外する (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で、ビジネス ルールを完全に削除せずにそのルールに対するデータの検証が行われないようにする場合は、ビジネス ルールを除外します。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[システム管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
### <a name="to-exclude-a-business-rule"></a>ビジネス ルールを除外するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  メニュー バーから **[管理]** をポイントして **[ビジネス ルール]** をクリックします。  
  
3.  **[ビジネス ルールのメンテナンス]** ページの **[モデル]** の一覧からモデルを選択します。  
  
4.  **[エンティティ]** の一覧からエンティティを選択します。  
  
5.  **メンバーの種類**一覧で、メンバーの種類を選択します。  
  
6.  **[属性]** の一覧で、属性を選択するか、 **[すべて]** の既定値のままにします。  
  
7.  グリッドで、ビジネス ルールの行のチェック ボックスをオン、**除外**列。 値、**状態**列が**除外の保留中**します。  
  
8.  **[ビジネス ルールのパブリッシュ]** をクリックします。  
  
9. 確認のダイアログ ボックスで **[OK]** をクリックします。 値、**状態**列が**除外**します。  
  
## <a name="see-also"></a>参照  
 [ビジネス ルールを削除する (マスター データ サービス)](../../2014/master-data-services/delete-a-business-rule-master-data-services.md)   
 [ビジネス ルールを作成しパブリッシュする (マスター データ サービス)](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [ビジネス ルール (マスター データ サービス)](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
