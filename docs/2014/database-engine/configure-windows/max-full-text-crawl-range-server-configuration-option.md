---
title: max full-text crawl range サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- crawls [full-text search]
- max full-text crawl range option
ms.assetid: a49de86b-0891-4dcd-89c0-ead30aab00e0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a05811b363303e6d68e13faf62d9aca1825b767d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62781697"
---
# <a name="max-full-text-crawl-range-server-configuration-option"></a>max full-text crawl range サーバー構成オプション
  **max full-text crawl range** オプションは、CPU の使用率を最適化して、フル クロール中のクロールのパフォーマンスを向上させる場合に使用します。 このオプションを使用して、フル インデックス クロール中に [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって使用されるパーティションの数を指定できます。 たとえば、CPU が多数あり、CPU の使用率が最適でない場合は、このオプションの最大値を大きくすることができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、このオプションだけでなく、テーブルの行数や CPU 数などの他の多くの要素によって、使用する実際のパーティション数を決定します。  
  
 このオプションの既定値は 4 です。また、最小値は 1 で、最大値は 256 です。 このオプションを変更すると、変更後のクロールにのみ影響します。 このオプションの設定を変更しても、処理中のクロールは影響を受けません。  
  
 **max full-text crawl range** オプションは拡張オプションです。 **sp_configure** システム ストアド プロシージャを使用して **max full-text crawl range** の設定を変更するには、 **show advanced options** を 1 に設定する必要があります。 新しい設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
## <a name="see-also"></a>関連項目  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
