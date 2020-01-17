---
title: テキストとイメージデータを一括コピーする |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ab694a8ba3a1976207ad1d0c6505cc953f39ff94
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73785146"
---
# <a name="bulk-copying-text-and-image-data"></a>テキスト データと画像データの一括コピー
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Large **text**、 **ntext**、 **image**の値は、 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)関数を使用して一括コピーされます。 **Text**型、 **ntext**型、または**image**型の列に対して[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)コードを作成し、データが**bcp_moretext**で提供されることを示す*pData*ポインターを NULL に設定します。 各一括コピーされた行の**text**、 **ntext**、または**image**列ごとに指定されるデータの正確な長さを指定することが重要です。 列のデータの長さが[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)で指定された列の長さと異なる場合は、 [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)を使用して長さを適切な値に設定します。 [Bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)は、すべての非**テキスト**、非**ntext**、および非**イメージ**データを送信します。次に、 **bcp_moretext**を呼び出して、 **text**、 **ntext**、または**image**型のデータを別々の単位で送信します。 一括コピー関数は、現在の**text**、 **ntext**、または**image**列に対して、 **bcp_moretext**で送信されたデータの長さの合計が、最新の bcp_collen で指定された長さと等しい場合に、すべてのデータが送信されたことを確認します。または**bcp_bind**。  
  
 **bcp_moretext**には、列を識別するパラメーターがありません。 行内に複数の**text**、 **ntext**、または**image**型の列がある場合、 **bcp_moretext**は、最小の序数を持つ列で始まる**text**、 **ntext**、または**image**型の列を操作します。序数が最も大きい列に進みます。 送信されるデータの長さの合計が、最新の**bcp_collen**または現在の列の**bcp_bind**に指定された長さと等しい場合、 **bcp_moretext**は1つの列から次の列に移動します。  
  
## <a name="see-also"></a>参照  
 [一括コピー操作&#40;の実行 (ODBC)&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
