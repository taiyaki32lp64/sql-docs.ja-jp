---
title: XTP ストレージ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 50e62a9232690deb368096723f428118e9de7aa2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151152"
---
# <a name="xtp-storage"></a>XTP ストレージ
  XTP ストレージのパフォーマンス オブジェクトには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の XTP ストレージに関連するカウンターが含まれています。  
  
 この表は、 **XTP ストレージ**カウンター。  
  
|カウンター|説明|  
|-------------|-----------------|  
|**終了したチェックポイント**|オンライン エージェントによって終了されたチェックポイントの数。|  
|**完了したチェックポイント**|オフライン チェックポイント スレッドによって処理されたチェックポイントの数。|  
|**完了したコア マージ**|マージ ワーカー スレッドによって実行されたコア マージの数。 これらのマージは、引き続きインストールされている必要があります。|  
|**マージ ポリシーの評価**|サーバーが開始してから行われたマージ ポリシーの評価の数。|  
|**未処理のマージ要求**|サーバーが開始してから未処理になっているのマージ要求の数。|  
|**放棄されたマージ**|エラーにより放棄されたマージの数。|  
|**インストールされているマージ**|適切にインストールされたマージの数。|  
|**マージされているファイルの総数**|マージされているソース ファイルの総数。 この数を使用すると、マージ内のソース ファイル数の平均がわかります。|  
  
## <a name="see-also"></a>参照  
 [XTP &#40;、インメモリ OLTP&#41;パフォーマンス カウンター](../../integration-services/performance/performance-counters.md)  
  
  
