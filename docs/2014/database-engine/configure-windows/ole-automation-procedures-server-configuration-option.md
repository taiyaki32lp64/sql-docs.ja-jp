---
title: Ole Automation Procedures サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Ole Automation Procedures option
ms.assetid: e8982e05-4984-4406-9760-285e8c028ddf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f00c238dfb32089261c51936b3937b0657c58b08
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62782030"
---
# <a name="ole-automation-procedures-server-configuration-option"></a>Ole Automation Procedures サーバー構成オプション
  `Ole Automation Procedures` オプションは、[!INCLUDE[tsql](../../includes/tsql-md.md)] バッチ内で OLE オートメーション オブジェクトをインスタンス化するかどうかを指定するために使用します。 このオプションは、ポリシー ベースの管理または **sp_configure** ストアド プロシージャを使用して構成することもできます。 詳細については、「 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)」を参照してください。  
  
 `Ole Automation Procedures` オプションに設定できる値を次に示します。  
  
 0  
 OLE オートメーション プロシージャを無効にします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の新しいインスタンスの既定値です。  
  
 1  
 OLE オートメーション プロシージャを有効にします。  
  
 OLE オートメーション プロシージャが有効である場合、 **sp_OACreate** を呼び出すと OLE 共有実行環境が開始します。  
  
 現在の値、`Ole Automation Procedures`オプションを表示およびを使用して変更できる、 **sp_configure**システム ストアド プロシージャ。  
  
## <a name="examples"></a>使用例  
 OLE オートメーション プロシージャの現在の設定を確認する方法を次の例に示します。  
  
```  
EXEC sp_configure 'Ole Automation Procedures';  
GO  
```  
  
 OLE オートメーション プロシージャを有効にする方法を次の例に示します。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Ole Automation Procedures', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
