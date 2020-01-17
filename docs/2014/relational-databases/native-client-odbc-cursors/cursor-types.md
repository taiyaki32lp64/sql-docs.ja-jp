---
title: カーソルの種類 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC applications, cursors
- cursors [ODBC], types
- ODBC cursors, types
ms.assetid: 3a916cc7-f352-42cb-8b83-f78e06cef991
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d88b48c1fc4166b32821da9cdaaa5eb7f6c2e60
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63071003"
---
# <a name="cursor-types"></a>カーソルの種類
  ODBC は、Microsoft でサポートされている 4 つのカーソルの種類を定義します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバー。 これらのカーソルが結果セットの変更を検出する機能に異なるれ、リソースにメモリなど、使用および領域**tempdb**します。 カーソルが行への変更を検出できるのは、変更が加えられた行の再フェッチを試みたときだけです。現在フェッチしている行への変更を、データ ソースからカーソルに通知する方法はありません。 カーソルを使用して行われなかった変更を検出する機能は、トランザクション分離レベルによって異なる場合があります。  
  
 次に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされる 4 種類の ODBC カーソルを示します。  
  
-   順方向専用カーソルではスクロールがサポートされず、カーソルの最初から最後まで行を順番にフェッチする機能だけがサポートされます。  
  
-   静的カーソルが組み込まれて**tempdb**カーソルが開かれた場合。 静的カーソルは、常に、カーソルを開いた時点の結果セットを表示します。 データへの変更は反映されません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の静的カーソルは常に読み取り専用です。 静的サーバー カーソルは作業テーブルとして構築されるため**tempdb**、カーソル結果セットのサイズで許容される最大行サイズを超えることはできません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
-   キーセット ドリブン カーソルでは、カーソルを開くときに、結果セット内の行のメンバーシップと順序が固定されます。 非キー列の変更は、このカーソルを使用して表示されます。  
  
-   動的カーソルは静的カーソルと対照的です。 動的カーソルでは、結果セット内の行に対するすべての変更が反映されます。 結果セット内の行のデータ値、順序、およびメンバーシップは、フェッチを実行するたびに変化する可能性があります。  
  
## <a name="see-also"></a>関連項目  
 [カーソルを使用して&#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
