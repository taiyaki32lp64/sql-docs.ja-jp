---
title: 次のフェッチ位置 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c47f1a8692cf7d2e3fb4f00c64770b3b0c69e5a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63183643"
---
# <a name="next-fetch-position"></a>次のフェッチ位置
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは常に追跡の次のフェッチ位置のためをへの呼び出しのシーケンス、 **GetNextRows**メソッド (の方向、または介在する変更の呼び出しをスキップ、なし、 **FindNextRow**、**シーク**、または**RestartPosition**メソッド) をスキップまたは任意の行を繰り返しせずに行セット全体を読み取ります。 **IRowset::GetNextRows**、**IRowset::RestartPosition**、または **IRowsetIndex::Seek** を呼び出すか、*pBookmark* 値に NULL を指定して **FindNextRow** を呼び出すことにより、次のフェッチ位置が変更されます。 *pBookmark* 値に NULL 以外の値を指定して **FindNextRow** を呼び出しても、次のフェッチ位置には影響しません。  
  
## <a name="see-also"></a>参照  
 [行のフェッチ](fetching-rows.md)  
  
  
