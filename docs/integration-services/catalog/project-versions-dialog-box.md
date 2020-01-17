---
title: '[プロジェクトのバージョン] ダイアログ ボックス | Microsoft Docs'
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.isprojectprop.versions.f1
ms.assetid: a48a387c-2e70-45bc-be2e-26e57a9bb2c4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9b1715b517f6933a9f904b17ff268fdf7162464d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294896"
---
# <a name="project-versions-dialog-box"></a>[プロジェクトのバージョン] ダイアログ ボックス

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **[プロジェクトのバージョン]** ダイアログ ボックスを使用して、プロジェクトのバージョンの表示および以前のバージョンへの復元を行うことができます。  
  
 また、[catalog.object_versions &#40;SSISDB Database&#41;](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md) ビューで以前のバージョンを表示し、[catalog.restore_project &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md) ストアド プロシージャを使用して以前のバージョンを復元することもできます。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [[プロジェクトのバージョン] ダイアログ ボックスを開く](#open_dialog)  
  
-   [プロジェクトのバージョンの復元](#restore)  
  
##  <a name="open_dialog"></a> [プロジェクトのバージョン] ダイアログ ボックスを開く  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]から [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに接続します。  
  
     つまり、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] データベースをホストする [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のインスタンスに接続します。  
  
2.  オブジェクト エクスプローラーで、ツリーを展開して、 **[Integration Services カタログ]** ノードを表示します。  
  
3.  **[Integration Services カタログ]** ノードを展開して、 **[SSISDB]** ノードを表示します。  
  
4.  **[SSISDB]** ノードには 1 つ以上のフォルダーが含まれており、各フォルダーには 1 つ以上のプロジェクトが含まれています。 対象とするプロジェクトを含むフォルダーを展開します。  
  
5.  このプロジェクトを右クリックし、 **[バージョン]** をクリックします。  
  
 **[プロジェクトのバージョン]** ダイアログ ボックスの **[バージョン]** テーブルには、サーバー上に配置されたプロジェクトのバージョン、バージョンが配置された日時、バージョンが復元された日時 (復元された場合)、バージョンの説明、およびバージョンの識別子の一覧が表示されます。 このテーブルでは、現在アクティブなバージョンの **[現在]** 列にチェック マークが付きます。  
  
##  <a name="restore"></a> プロジェクトのバージョンの復元  
 以前のバージョンのプロジェクトを復元するには、 **[バージョン]** テーブルでバージョンを選択し、 **[選択したバージョンに復元]** をクリックします。 プロジェクトが選択したバージョンに復元され、 **[バージョン]** テーブルでは、そのバージョンの **[現在]** 列にチェック マークが付きます。  
  
  
