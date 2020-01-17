---
title: 複数の行セットの結果を生成するコマンド |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- SQL Server Native Client OLE DB provider, commands
- SQL Server Native Client OLE DB provider, multiple rowsets
- commands [OLE DB]
- multiple-rowset results
ms.assetid: 4567668d-35fd-4162-b61f-f7536862cdcb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04a7db670171f6f890f55a89e2da987ef2309f0e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62657682"
---
# <a name="commands-generating-multiple-rowset-results"></a>複数行セットの結果を生成するコマンド
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーから複数の行セットを返すことができます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ステートメント。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のステートメントは、次の条件が満たされた場合に複数行セットの結果を返します。  
  
-   バッチにまとめられた SQL ステートメントが 1 つのコマンドとして実行される場合。  
  
-   ストアド プロシージャが SQL ステートメントのバッチを実装している場合。  
  
## <a name="batches"></a>バッチ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、SQL ステートメントのバッチ区切り記号としてセミコロン文字を認識します。  
  
```  
WCHAR*       wSQLString = L"SELECT * FROM Categories; "  
                          L"SELECT * FROM Products";  
```  
  
 複数の SQL ステートメントを 1 つのバッチにまとめて送信する方が、各 SQL ステートメントを個別に実行するよりも効率的です。 1 つのバッチを送信することで、クライアントからサーバーへのネットワーク ラウンド トリップが減少するためです。  
  
## <a name="stored-procedures"></a>ストアド プロシージャ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、ストアド プロシージャ内のステートメントごとに結果セットを返します。このため、大半の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャは複数の結果セットを返します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [IMultipleResults を使用した複数の結果セットの処理](using-imultipleresults-to-process-multiple-result-sets.md)  
  
## <a name="see-also"></a>関連項目  
 [[コマンド]](commands.md)  
  
  
