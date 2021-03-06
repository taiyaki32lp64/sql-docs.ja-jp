---
title: エクスポート (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bb777a0de00596c99e22e514986cf3ec930ba0fd
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2018
ms.locfileid: "37991063"
---
# <a name="export-dmx"></a>EXPORT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  マイニング モデルまたはマイニング構造オブジェクトをサーバーから Analysis Services Backup File (.abf) へ展開します。  
  
## <a name="syntax"></a>構文  
  
```  
  
EXPORT <object type> <object name>[, <object name>] [<object type> <object name>[, <object name] ] TO <filename> [WITH DEPENDENCIES]  
```  
  
## <a name="arguments"></a>引数  
 *オブジェクトの種類*  
 (マイニング モデルまたはマイニング構造) をエクスポートするオブジェクトの型を省略します。  
  
 *オブジェクト名*  
 任意。 エクスポートするオブジェクトの名前です。  
  
 *filename*  
 文字列としてエクスポートするファイルの名前と場所です。  
  
## <a name="remarks"></a>コメント  
 ステートメントがマイニング モデルを指定する場合、結果ファイルは関連するマイニング構造も含みます。 ステートメントが指定されている場合**WITH DEPENDENCIES**、(データ ソースとデータ ソース ビューなど) のオブジェクトを処理するために必要なすべてのオブジェクトが、.abf ファイルに含まれます。  
  
 データベースであるか、エクスポートまたはインポートするサーバーの管理者がオブジェクトから、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]データベース。  
  
## <a name="export-mining-structure-example"></a>マイニング構造のエクスポート例  
 次の例は、Targeted Mailing と Forecasting マイニング構造、および Association マイニング モデルを、指定したファイルの場所にエクスポートします。 Association モデルは Market Basket マイニング構造の一部であるため、例では Market Basket 構造もエクスポートします。 使用してアソシエーション モデルがエクスポートされるため、Market Basket マイニング構造の一部はエクスポートされず可能性のあるその他のすべてのマイニング モデル**マイニング モデル**ではなく、**マイニング構造**します。  
  
```  
EXPORT MINING STRUCTURE [Targeted Mailing], [Forecasting] MINING MODEL Association TO 'C:\TM_NEW.abf'  
```  
  
## <a name="export-mining-model-example"></a>マイニング モデルのエクスポート例  
 次の例は、Association マイニング モデルを、指定したファイルの場所にエクスポートします。 ステートメントが指定されているので**WITH DEPENDENCIES**、データ ソースおよびデータ ソース ビュー オブジェクトも .abf ファイルに含まれます。  
  
```  
EXPORT MINING MODEL [Association] TO 'C:\Association_NEW.abf' WITH DEPENDENCIES  
```  
  
## <a name="see-also"></a>参照  
 [データ マイニング拡張機能&#40;DMX&#41;データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能&#40;DMX&#41;ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)   
 [インポート&AMP;#40;DMX&AMP;#41;](../dmx/import-dmx.md)   
 [データ マイニング オブジェクトのエクスポートおよびインポート](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  
