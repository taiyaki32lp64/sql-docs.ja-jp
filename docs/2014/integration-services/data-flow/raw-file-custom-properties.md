---
title: RAW ファイルのカスタム プロパティ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7e81f7e1-fac0-4b57-b145-8f1b9e4720bf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fe3f77ac629aab7534077274aa9cf62a50149b57
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900902"
---
# <a name="raw-file-custom-properties"></a>RAW ファイルのカスタム プロパティ
  **変換元のカスタム プロパティ**  
  
 RAW ファイル ソースには、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、RAW ファイル ソースのカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (列挙)|生データへのアクセスに使用するモード。 有効な値は、`File name` (0) および `File name from variable` (1) です。 既定値は `File name` (0) です。|  
|FileName|String|ソース ファイルのパスおよびファイル名。|  
  
 RAW ファイル ソースの出力および出力列には、カスタム プロパティがありません。  
  
 詳細については、「 [RAW ファイル ソース](raw-file-source.md)」を参照してください。  
  
 **変換先のカスタム プロパティ**  
  
 RAW ファイル変換先には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、RAW ファイル変換先のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (列挙)|FileName プロパティにファイル名を含めるか、またはファイル名が含まれる変数名を含めるかを指定する値。 使用できるオプションは、`File name` (0) および `File name from variable` (1) です。|  
|FileName|String|RAW ファイル変換先が書き込むファイルの名前。|  
|WriteOption|Integer (列挙)|RAW ファイル変換先が、同じ名前の既存のファイルを削除するかどうかを指定する値。 使用できるオプションは、`Create Always` (0)、`Create Once` (1)、`Truncate and Append` (3)、および `Append` (2) です。 このプロパティの既定値は `Create Always` (0) です。|  
  
> [!NOTE]  
>  追加操作では、追加するデータのメタデータが、ファイル内の既存データのメタデータと一致している必要があります。  
  
 RAW ファイル変換先の入力および入力列には、カスタム プロパティはありません。  
  
 詳細については、「 [RAW ファイル変換先](raw-file-destination.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [共通プロパティ](../common-properties.md)  
  
  
