---
title: ポリシー ベースの管理のストレージ | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, storage
ms.assetid: d0cbf214-fc2e-4917-8d31-1d71c9ffa61d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e1eab3ad745a83a8a55545570e020c1f1af732ad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62628867"
---
# <a name="policy-based-management-storage"></a>ポリシー ベースの管理のストレージ
  ポリシーは msdb データベースに格納されます。 ポリシーまたは条件を変更した後、msdb をバックアップする必要があります。 詳細については、「[システム データベースのバックアップと復元 &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)」を参照してください。  
  
## <a name="storing-policies"></a>ポリシーの保存  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの監視に使用できるポリシーが用意されています。 既定では、これらのポリシーにインストールされていない、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。 ただし、C:\Program Files (x86) \Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033 の既定のインストール場所からインポートできます。  
  
 ポリシーを直接作成するには、 **[ファイル] メニューの [新規作成]** を使用して、ポリシーをファイルに保存します。 これにより、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]インスタンスに接続していないときにポリシーを作成できます。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の現在のインスタンスで評価されたポリシーのポリシー履歴は、msdb システム テーブルに格納されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のその他のインスタンスに適用されたポリシーまたは [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] や [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] に適用されたポリシーのポリシー履歴は保持されません。  
  
  
