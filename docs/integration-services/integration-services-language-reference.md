---
title: Integration Services 言語リファレンス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: c67b72f1-0a1e-42f0-878a-84e85efc915b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f32f03c7059cdb2410bc40312ce7d32555003e4e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284524"
---
# <a name="integration-services-language-reference"></a>Integration Services 言語リファレンス

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  このセクションでは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスに配置されている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを管理するための [!INCLUDE[tsql](../includes/tsql-md.md)] API について説明します。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] は、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] カタログと呼ばれるデータベースにオブジェクト、設定、および業務データを格納します。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] カタログの既定の名前は、SSISDB です。 カタログに格納されているオブジェクトには、プロジェクト、パッケージ、パラメーター、環境、操作履歴があります。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] カタログは、ユーザーに表示されない内部テーブルにデータを格納します。 ただし、必要な情報は、パブリック ビューに対してクエリを実行することで公開されます。 カタログの一般的なタスクを実行するために使用できる一連のストアド プロシージャも用意されています。  
  
 通常、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] を開くことによって、カタログの [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] オブジェクトを管理します。 ただし、データベース ビューとストアド プロシージャを直接使用することも、マネージド API を呼び出すカスタム コードを記述することもできます。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] およびマネージド API では、ビューに対してクエリを実行し、多くのタスクを実行するストアド プロシージャ (このセクションで説明) を呼び出します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [ビュー &#40;Integration Services カタログ&#41;](../integration-services/system-views/views-integration-services-catalog.md)  
 ビューに対してクエリを実行し、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] オブジェクト、設定、および業務データを調べます。  
  
 [ストアド プロシージャ &#40;Integration Services カタログ&#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
 ストアド プロシージャを呼び出して、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] オブジェクトおよび設定を追加、削除、または変更します。  
  
 [関数 &#40;Integration Services カタログ&#41;](https://msdn.microsoft.com/library/9f2aec85-3d4c-415f-b1f8-8328a60b1c7f)  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを管理する関数を呼び出します。  
  
  
