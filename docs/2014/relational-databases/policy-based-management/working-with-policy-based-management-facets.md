---
title: ポリシー ベースの管理ファセットの操作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- viewing Policy-Based Management facets
- facets [Policy-Based Management], copying
- facets [Policy-Based Management], viewing
- copying Policy-Based Management facets
ms.assetid: 88d025c4-07c2-4e4d-8634-204249a8c82c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 037eb57f53bf583195efdf1f91fcd55f94ebaddc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62676905"
---
# <a name="working-with-policy-based-management-facets"></a>ポリシー ベースの管理ファセットの操作
  ポリシー ベースの管理ファセットは、管理対象の領域に関連する一連の論理プロパティです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、いくつかの定義済みファセットが用意されています。 たとえば、セキュリティ構成ファセットは既定で無効になる機能をプロパティとして定義します。  
  
 同様の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境を多数管理する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の 1 つのインスタンスでファセットを構成し、ファセットの状態をファイルにコピーして、そのファイルを別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにポリシーとしてインポートできます。 状態がポリシーに変換されたら、そのポリシーを別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス、インスタンス オブジェクト、データベース、またはデータベース オブジェクトに適用できます。  
  
 このトピックでは、ファセットの状態を XML ファイルにコピーする方法について説明します。  
  
##  <a name="BeforeYouBegin"></a> 権限  
 このトピックの手順では、msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
## <a name="viewing-and-copying-facet-states"></a>ファセットの状態の表示とコピー  
 [SQL Server オブジェクトのポリシー ベースの管理ファセットの表示](view-the-policy-based-management-facets-on-a-sql-server-object.md)  
  
 [XML ファイルへのポリシー ベースの管理ファセットの状態のコピー](copy-a-policy-based-management-facet-state-to-an-xml-file.md)  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したサーバーの管理](administer-servers-by-using-policy-based-management.md)  
  
  
