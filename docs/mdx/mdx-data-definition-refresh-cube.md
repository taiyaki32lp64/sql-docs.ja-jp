---
title: REFRESH CUBE ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 957609573c206b7c3492789c369d0fb2be2398a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038163"
---
# <a name="mdx-data-definition---refresh-cube"></a>MDX データ操作 - REFRESH CUBE


  キューブのクライアント キャッシュを更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 キューブ名を提供する有効な文字列式。  
  
## <a name="remarks"></a>コメント  
 インスタンスに接続されているクライアント アプリケーションの[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、このステートメントは、サーバーと同期するクライアント アプリケーションのキャッシュ メモリをによりします。 この検出および更新は日常的かつ自動的に行われますが、同期が行われるまでの時間はクライアント接続文字列の設定によって異なります。 REFRESH CUBE ステートメントは、データをすぐに更新します。  
  
 ローカル キューブに接続されている、クライアント アプリケーションは、REFRESH CUBE ステートメントは、再構築するローカル キューブ ファイルをさせます。  
  
> [!IMPORTANT]  
>  サーバーに保存されている名前付きセットは更新されません。  
  
## <a name="see-also"></a>関連項目  
 [MDX データ定義ステートメント&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
