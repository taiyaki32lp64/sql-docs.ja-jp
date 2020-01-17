---
title: インポート (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2141a4f8ccc6e34ec3010ad3ce8e8e3789d09132
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892754"
---
# <a name="import-dmx"></a>IMPORT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Analysis Services バックアップファイル (abf) ファイルからサーバーにマイニングモデルまたはマイニング構造を読み込みます。  
  
## <a name="syntax"></a>構文  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>引数  
 *filename*  
 インポートするファイルの名前と場所を表す文字列。  
  
## <a name="remarks"></a>コメント  
 オブジェクトが指定されていない場合は、.dmb ファイルの内容全体が読み込まれます。 .dmb ファイルに、サーバー上に存在しないデータベースが含まれている場合、そのデータベースが作成されます。  
  
 オブジェクトをエクスポートまたはインポートするには、データベースまたはサーバーの管理者である必要があります。  
  
## <a name="import-from-file-example"></a>ファイルからインポートする例  
 次の例では、アソシエーションモデルと構造を含むファイルの内容全体を現在のサーバーにインポートします。  
  
```  
IMPORT FROM 'C:\TEMP\Association_NEW.dmb'  
```  
  
## <a name="see-also"></a>関連項目  
 [データマイニング拡張&#40;機能&#41; DMX データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データマイニング拡張&#40;機能&#41; DMX データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データマイニング拡張&#40;機能&#41; DMX ステートメントリファレンス](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX &#40;のエクスポート&#41;](../dmx/export-dmx.md)   
 [データ マイニング オブジェクトのエクスポートおよびインポート](https://docs.microsoft.com/analysis-services/data-mining/export-and-import-data-mining-objects)  
  
  
