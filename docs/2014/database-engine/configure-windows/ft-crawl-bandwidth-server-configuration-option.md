---
title: ft crawl bandwidth サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- large memory buffers
- memory [SQL Server], buffers
- ft crawl bandwidth option
ms.assetid: e5864ad9-92f5-43b5-95de-46d68ded8694
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f603987608a4c6456e01efc171bc93301069f046
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62782178"
---
# <a name="ft-crawl-bandwidth-server-configuration-option"></a>ft crawl bandwidth サーバー構成オプション
  **ft crawl bandwidth** オプションを使用すると、大規模メモリ バッファーのプールを拡張するサイズを指定できます。 大規模メモリ バッファーのサイズは 4 MB です。 **max** パラメーターの値によって、大規模バッファー プールでフルテキスト メモリ マネージャーが保持する必要があるバッファーの最大数が指定されます。 **max** の値がゼロ (0) の場合、大規模バッファー プールで保持できるバッファー数に上限はありません。  
  
 **min** パラメーターによって、大規模メモリ バッファーのプールで保持する必要があるメモリ バッファーの最少数が指定されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メモリ マネージャーからの要求時に、余分なバッファー プールがすべて解放されますが、このバッファーの最少数は保持されます。 ただし、 **min** の値にゼロ (0) が指定されている場合は、すべてのメモリ バッファーが解放されます。  
  
 特定の状況では、その時点で割り当てられるバッファーの数が **min** パラメーターによって指定された値よりも少なくなることがあります。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>参照  
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [ft notify bandwidth サーバー構成オプション](ft-notify-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
