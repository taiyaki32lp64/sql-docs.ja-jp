---
title: Master、tempdb、および model データベースでフルテキスト インデックスはサポートされていません |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes
ms.assetid: f7992965-42c1-4eb8-a7fb-afb38b67c740
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 743c7153b034cf5e1267c6a0da1e585845800980
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095198"
---
# <a name="full-text-indexes-on-master-tempdb-and-model-databases-are-not-supported"></a>master、tempdb、および model データベースに対するフルテキスト インデックスはサポートされない
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、いずれのシステム データベースに対してもフルテキスト インデックスが許可されません。  
  
## <a name="description"></a>説明  
 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] では、フルテキスト インデックスが master、tempdb、および model の各データベースでサポートされていました。  
  
 Master、tempdb、および model データベースでは、すべてのフルテキスト カタログは、アップグレード中に削除されます。  
  
## <a name="see-also"></a>関連項目  
 [アップグレード アドバイザーの使用](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
