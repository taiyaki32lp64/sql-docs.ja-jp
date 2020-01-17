---
title: トランザクションの注釈を設定する (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- annotations [Master Data Services], for transactions
ms.assetid: f5a6b2ca-56de-4e42-9da8-fba0ac3e8d92
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 87e33ff166f07c10ee8b0b32eac5590f486e70c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483916"
---
# <a name="annotate-a-transaction-master-data-services"></a>トランザクションの注釈を設定する (Master Data Services)
  履歴を参照する目的でトランザクションの詳細をサポートする場合、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]でトランザクションの注釈を設定します。  
  
> [!NOTE]  
>  注釈は削除できません。  
  
## <a name="prerequisites"></a>前提条件  
  
-   作成したトランザクションの注釈を設定するためには、 **[エクスプローラー]** 機能領域へのアクセス権限と、注釈を設定するモデル オブジェクトに対する **更新** 権限が最低限必要です。  
  
-   すべてのユーザーのトランザクションの注釈を設定するためには、 **[バージョン管理]** 機能領域へのアクセス権限を持っているモデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
### <a name="to-annotate-a-transaction-in-explorer"></a>[エクスプローラー] でトランザクションの注釈を設定するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、 **[モデル]** ボックスの一覧からモデルを選択します。  
  
2.  **[バージョン]** ボックスの一覧からバージョンを選択します。  
  
3.  **[エクスプローラー]** をクリックします。  
  
4.  メニュー バーの **[エンティティ]** をポイントして、注釈を設定するトランザクションを持つメンバーを含むエンティティの名前をクリックします。  
  
5.  グリッドで、メンバーの行をクリックします。  
  
6.  **[トランザクションの表示]** をクリックします。  
  
7.  **[トランザクションの表示]** ダイアログ ボックスで、注釈を設定するトランザクションをクリックします。  
  
8.  ダイアログ ボックスの下部にあるボックスに、注釈を入力します。  
  
9. **[注釈の追加]** をクリックします。 **[注釈]** ペインに注釈が表示されます。  
  
### <a name="to-annotate-a-transaction-in-version-management-administrators-only"></a>[バージョン管理] でトランザクションに注釈を設定する (管理者のみ)  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ホーム ページで、 **[バージョン管理]** をクリックします。  
  
2.  メニュー バーの **[トランザクション]** をクリックします。  
  
3.  **[トランザクション]** ペインで、注釈を設定するトランザクションのグリッド内の行をクリックします。  
  
4.  **[トランザクションの注釈]** ペインの **[注釈]** ボックスに注釈を入力します。  
  
5.  **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [注釈 (マスター データ サービス)](../../2014/master-data-services/annotations-master-data-services.md)   
 [トランザクション (マスター データ サービス)](../../2014/master-data-services/transactions-master-data-services.md)  
  
  
