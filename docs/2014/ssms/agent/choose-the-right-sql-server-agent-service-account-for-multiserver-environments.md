---
title: マルチ サーバー環境の適切な SQL Server エージェント サービス アカウントの選択 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, service accounts
- multiserver environments [SQL Server], SQL Server Agent service account behavior
ms.assetid: a07e2f38-281c-495b-965b-13fad03ba548
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e3a981690efb0139d8878cab4e13794fdcf44ed7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199909"
---
# <a name="choose-the-right-sql-server-agent-service-account-for-multiserver-environments"></a>マルチサーバー環境に適した SQL Server エージェント サービス アカウントの選択
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスに対して選択する Windows アカウントによって、マルチサーバー環境の動作に次のような影響が生じることがあります。  
  
-   ローカルの Windows Administrators グループのメンバーではないアカウントで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを実行する場合、マスター サーバーへのターゲット サーバーの参加は、失敗する可能性があります。 その場合は、次のエラー メッセージが返されます。  
  
     "参加操作に失敗しました"  
  
     この問題を解決するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを再起動します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスがローカル システム アカウントで実行されるとき、マスター サーバーと対象サーバー間の操作は、同じコンピューターにマスター サーバーと対象サーバーの両方が存在する場合にのみサポートされます。 この構成を使用している場合に、ターゲット サーバーをマスター サーバーに参加させると、次のメッセージが返されます。  
  
     " *<target_server_computer_name>* のエージェント開始アカウントに対象サーバーとしてのログオン権限があることを確認します"  
  
     情報提供を目的としたこのメッセージは無視できます。 参加操作は、正常に完了します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスのアカウントの選択の詳細については、「 [SQL Server エージェント サービスのアカウントの選択](select-an-account-for-the-sql-server-agent-service.md)」を参照してください。  
  
  
