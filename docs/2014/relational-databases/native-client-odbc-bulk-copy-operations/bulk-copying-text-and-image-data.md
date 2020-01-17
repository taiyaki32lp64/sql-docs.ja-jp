---
title: テキストとイメージ データの一括コピー |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c468ec3cf52526192893458055cde857aeaa864d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067478"
---
# <a name="bulk-copying-text-and-image-data"></a>テキスト データと画像データの一括コピー
  大規模な**テキスト**、 **ntext**、および**イメージ**値は、一括コピーを使用して、 [bcp_moretext](../native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)関数。 コードを記述[bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)の**テキスト**、 **ntext**、または**イメージ**列で、 *pData*ポインターに設定NULL を示すデータが提供されます**bcp_moretext**します。 それぞれの指定したデータの正確な長さを指定することが重要**テキスト**、 **ntext**、または**イメージ**一括コピーの各行の列。 列のデータの長さがで指定された列の長さと異なる場合[bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)を使用して、 [bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)長さを適切な値に設定します。 A [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)送信すべて以外**テキスト**、非-**ntext**、および非-**イメージ**データは呼び出して**bcp_moretext**を送信する、**テキスト**、 **ntext**、または**イメージ**個別の単位でのデータ。 一括コピー関数は、現在のすべてのデータが送信されたことを確認**テキスト**、 **ntext**、または**イメージ**を通じて送信されるデータの長さの合計列**bcp_moretext**最新版の指定された長さと等しい**bcp_collen**または**bcp_bind**します。  
  
 **bcp_moretext**列を識別するためにパラメーターがありません。 複数の場合**テキスト**、 **ntext**、または**イメージ**、行内の列**bcp_moretext**で動作、**テキスト**、 **ntext**、または**イメージ**列序数が最も低い、最高の序数の列に進みますから始まる列。 **bcp_moretext**送信されるデータの長さの合計が最新で指定された長さと等しい場合は、次 1 つの列からが**bcp_collen**または**bcp_bind**現在の列。  
  
## <a name="see-also"></a>関連項目  
 [一括コピー操作を実行する&#40;ODBC&#41;](performing-bulk-copy-operations-odbc.md)  
  
  
