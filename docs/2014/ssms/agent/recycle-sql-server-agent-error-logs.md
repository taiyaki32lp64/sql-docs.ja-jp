---
title: '[SQL Server エージェント エラー ログの再利用] | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c0654dcc83e757751ac055192775c0ee958f26e9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62753069"
---
# <a name="recycle-sql-server-agent-error-logs"></a>[SQL Server エージェント エラー ログの再利用]
  このページを使用すると、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント エラー ログを再利用できます。 ログを再利用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを再起動しなくても、現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント エラー ログが閉じ、新しいエラー ログが開始します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで保持されるエラー ログは直前の 9 個までであることに注意してください。 既にエラー ログが 9 個に達している場合は、エラー ログを再利用すると [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは最も古いエラーログを削除します。  
  
## <a name="see-also"></a>参照  
 [SQL Server エージェント エラー ログ](sql-server-agent-error-log.md)  
  
  
