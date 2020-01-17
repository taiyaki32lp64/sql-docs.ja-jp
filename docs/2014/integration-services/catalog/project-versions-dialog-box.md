---
title: '[プロジェクトのバージョン] ダイアログ ボックス | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isprojectprop.versions.f1
ms.assetid: a48a387c-2e70-45bc-be2e-26e57a9bb2c4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8aefce0d5afe7bec37c5fe49ba63c3fec61f3747
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771545"
---
# <a name="project-versions-dialog-box"></a>[プロジェクトのバージョン] ダイアログ ボックス
  **[プロジェクトのバージョン]** ダイアログ ボックスを使用して、プロジェクトのバージョンの表示および以前のバージョンへの復元を行うことができます。  
  
 また、[catalog.object_versions &#40;SSISDB Database&#41;](/sql/integration-services/system-views/catalog-object-versions-ssisdb-database) ビューで以前のバージョンを表示し、[catalog.restore_project &#40;SSISDB Database&#41;](/sql/integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database) ストアド プロシージャを使用して以前のバージョンを復元することもできます。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [[プロジェクトのバージョン] ダイアログ ボックスを開く](#open_dialog)  
  
-   [プロジェクトのバージョンの復元](#restore)  
  
##  <a name="open_dialog"></a> [プロジェクトのバージョン] ダイアログ ボックスを開く  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]から [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] サーバーに接続します。  
  
     つまり、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] データベースをホストする [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のインスタンスに接続します。  
  
2.  オブジェクト エクスプローラーで、ツリーを展開して、 **[Integration Services カタログ]** ノードを表示します。  
  
3.  **[Integration Services カタログ]** ノードを展開して、 **[SSISDB]** ノードを表示します。  
  
4.  **[SSISDB]** ノードには 1 つ以上のフォルダーが含まれており、各フォルダーには 1 つ以上のプロジェクトが含まれています。 対象とするプロジェクトを含むフォルダーを展開します。  
  
5.  このプロジェクトを右クリックし、 **[バージョン]** をクリックします。  
  
 **[プロジェクトのバージョン]** ダイアログ ボックスの **[バージョン]** テーブルには、サーバー上に配置されたプロジェクトのバージョン、バージョンが配置された日時、バージョンが復元された日時 (復元された場合)、バージョンの説明、およびバージョンの識別子の一覧が表示されます。 このテーブルでは、現在アクティブなバージョンの **[現在]** 列にチェック マークが付きます。  
  
##  <a name="restore"></a> プロジェクトのバージョンの復元  
 以前のバージョンのプロジェクトを復元するには、 **[バージョン]** テーブルでバージョンを選択し、 **[選択したバージョンに復元]** をクリックします。 プロジェクトが選択したバージョンに復元され、 **[バージョン]** テーブルでは、そのバージョンの **[現在]** 列にチェック マークが付きます。  
  
  
