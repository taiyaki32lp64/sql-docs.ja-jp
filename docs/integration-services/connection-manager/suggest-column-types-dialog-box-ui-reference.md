---
title: '[列の型の推測] ダイアログ ボックスの UI リファレンス | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.suggestdatatypes.f1
ms.assetid: 8d5652e0-cf57-483f-828b-10f00c08418b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 86e63eb6ab4c8d851d442e50b68cc56d2456580c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298448"
---
# <a name="suggest-column-types-dialog-box-ui-reference"></a>[列の型の推測] ダイアログ ボックスの UI リファレンス

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **[列の型の推測]** ダイアログ ボックスを使用すると、フラット ファイル接続マネージャー内の列のデータ型および長さを、ファイルの内容のサンプリングに基づいて識別できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]で使用されるデータ型の詳細については、「 [Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="options"></a>オプション  
 **[行数]**  
 アルゴリズムで使用するサンプル内の行数を入力または選択します。  
  
 **[最小の整数データ型を推測する]**  
 評価をスキップする場合は、このチェック ボックスをオフにします。 オンにすると、整数の数値データを含む列で使用できる最小の整数データ型が決定されます。  
  
 **[最小の実数データ型を推測する]**  
 評価をスキップする場合は、このチェック ボックスをオフにします。 オンにすると、実数データを含む列で、より小さい実数データ型 DT_R4 を使用できるかどうかが決定されます。  
  
 **[以下の値を使用してブール型の列を特定する]**  
 ブール値 True および False として使用する 2 つの値を入力します。 値はコンマで区切る必要があり、最初の値が True を表すようにします。  
  
 **[文字列型の列を埋め込む]**  
 このチェック ボックスをオンにすると、文字列の埋め込みが有効になります。  
  
 **[埋め込み率]**  
 文字データ型の列の長さを増やすために使用する、列の長さに対する割合を入力または選択します。 割合は整数にする必要があります。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../integration-services/integration-services-error-and-message-reference.md)   
 [フラット ファイル接続マネージャー](../../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  
