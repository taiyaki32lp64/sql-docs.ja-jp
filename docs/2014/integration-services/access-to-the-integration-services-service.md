---
title: サービスのサービスの統合へのアクセス |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- viewing packages while running
- displaying packacges while running
- security [Integration Services], running packages
- packages [Integration Services], security
- current packages running
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 1088aafc-14c5-4e7d-9930-606a24c3049b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e3654be0afe51be6566a09897a2656dd53c77696
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062234"
---
# <a name="access-to-the-integration-services-service"></a>Integration Services サービスへのアクセス
  パッケージの保護レベルによって、パッケージを編集および実行できるユーザーを制限できます。 サーバーで現在実行中のパッケージの一覧を表示できるユーザー、および [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]で現在実行中のパッケージを停止できるユーザーを制限するには、追加の保護が必要です。  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] では、実行中のパッケージを一覧表示する際に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] サービスが使用されます。 Windows の Administrators グループのメンバーは、実行中のすべてのパッケージを表示および停止できます。 Administrators グループのメンバーではないユーザーは、本人が起動したパッケージのみを表示および停止できます。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] サービス (特に、リモート フォルダーの列挙を行う可能性のある [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] サービス) を実行するコンピューターへのアクセスを制限することは重要です。 認証を受けたユーザーであれば、パッケージの列挙を要求できます。 でも、サービスが検出されない場合、サービス、サービスにフォルダーを列挙します。 これらのフォルダー名が、悪意あるユーザーに悪用される場合があります。 管理者がリモート コンピューターのフォルダーを列挙できるようにサービスを設定した場合、ユーザーも通常は参照できないフォルダー名を参照することができます。  
  
  
