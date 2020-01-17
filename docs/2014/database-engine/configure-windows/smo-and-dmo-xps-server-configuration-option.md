---
title: SMO and DMO XPs サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d55bd667909721a68d51bcd1db7128b809118843
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62755279"
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>SMO and DMO XPs サーバー構成オプション
  このサーバーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) の拡張ストアド プロシージャを使用するには、SMO and DMO XPs オプションを使用します。  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]の DMO は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で削除されました。  
  
 次の表に、このオプションで使用可能な値を示します。  
  
|値|説明|  
|-----------|-------------|  
|0|SMO 拡張ストアド プロシージャ (XP) を使用できません。|  
|1|SMO 拡張ストアド プロシージャ (XP) を使用できます。 既定値です。|  
  
 この設定はすぐに有効になります。  
  
## <a name="examples"></a>使用例  
 次の例では、SMO の拡張ストアド プロシージャを有効にします。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'SMO and DMO XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>参照  
 [SQL Server 管理オブジェクト &#40;SMO&#41; プログラミング ガイド](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
