---
title: 複数のアクティブな結果セット (MARS)
description: 複数の SqlDataReader を1つの接続で開く方法について説明します。 SqlDataReader の各インスタンスは、個別のコマンドから起動します。
ms.date: 08/15/2019
ms.assetid: c90ef863-bac7-44cf-adc1-f05c36fcf57d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 7097dc3717966d441cd669ddccd189c2510211aa
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452148"
---
# <a name="multiple-active-result-sets-mars"></a>複数のアクティブな結果セット (MARS)

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

複数のアクティブな結果セット (MARS) は、1つの接続で複数のバッチを実行できる機能です。 以前のバージョンでは、1つの接続に対して一度に実行できるバッチは1つだけでした。 MARS を使用して複数のバッチを実行することは、操作の同時実行を意味するわけではありません。  
  
## <a name="in-this-section"></a>このセクションの内容  
[複数のアクティブな結果セットの有効化](enable-multiple-active-result-sets.md)  
MARS を SQL Server で使用する方法について説明します。  
  
[データの操作](manipulate-data.md)  
MARS アプリケーションのコーディング例を示します。  
  
## <a name="related-sections"></a>関連項目  
[非同期操作](asynchronous-operations.md)  
.NET の新しい非同期機能の使用方法について詳しく説明します。  
  
## <a name="next-steps"></a>次の手順
- [SQL Server と ADO.NET](index.md)
