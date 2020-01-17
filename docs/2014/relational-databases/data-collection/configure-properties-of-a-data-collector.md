---
title: データ コレクターのプロパティの構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.dc.datacollectionprop.advanced.f1
- sql12.swb.dc.datacollectionprop.general.f1
ms.assetid: cf98f57d-5a6d-4bc3-bf10-783e460fc63d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 37df9ccdd0bc2b44384bb9fd3d130c8d3bf8ca36
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62873428"
---
# <a name="configure-properties-of-a-data-collector"></a>データ コレクターのプロパティの構成
  ここでは、データ コレクターのプロパティを構成する方法について説明します。  
  
## <a name="data-collection-properties-general-tab"></a>[データ コレクションのプロパティ] ([全般] タブ)  
 このページを使用すると、管理データ ウェアハウスの設定を構成し、収集したデータをデータ ウェアハウスにアップロードするまで格納しておく場所を指定できます。  
  
 **[データ コレクションの有効化]**  
 データ コレクションを有効にする場合にオンにします。 これは、sp_syscollector_enable_collector ストアド プロシージャを実行するのと同じ効果があります。 このチェック ボックスをオフにすると、データ コレクションが無効になり、sp_syscollector_disable_collector ストアド プロシージャを実行した場合と同じ結果になります。  
  
 **[サーバー]**  
 管理データ ウェアハウスをホストするサーバーの名前が表示されます。  
  
 **データベース名**  
 管理データ ウェアハウスに使用されるリレーショナル データベースの名前が表示されます。  
  
 **[接続テスト]**  
 データ コレクションの構成時に指定した情報を使用して、 **[サーバー]** で指定したサーバーへの接続をテストします。  
  
 **[キャッシュ ディレクトリ]**  
 収集したデータを管理データ ウェアハウスにアップロードするまで格納しておく、データを収集したシステム上のディレクトリを指定します。 **キャッシュ ディレクトリ** が指定されていない場合、データ コレクターは %TEMP% 環境変数と %TMP% 環境変数を探し、これらの場所を一時ストレージの既定の場所として使用しようとします。 これらの環境変数が構成されていない場合はエラーが発生し、キャッシュ ディレクトリを作成するよう求めるメッセージが表示されます。  
  
## <a name="data-collection-properties-advanced-tab"></a>[データ コレクションのプロパティ] ([詳細設定] タブ)  
 このページを使用すると、管理データ ウェアハウスへの接続の再試行の設定を構成できます。  
  
 **[アップロード失敗時の再試行回数]**  
 アップロードが失敗した場合に、管理データ ウェアハウスへのアップロードを再試行する回数を指定します。 既定値は 1 です。  
  
## <a name="see-also"></a>参照  
 [データ コレクションの管理](data-collection.md)   
 [管理データ ウェアハウスの構成 &#40;SQL Server Management Studio&#41;](configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
  
