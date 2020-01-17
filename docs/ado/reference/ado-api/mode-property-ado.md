---
title: Mode プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Mode
- _Stream::Mode
- _Record::Mode
helpviewer_keywords:
- Mode property [ADO]
ms.assetid: 808661eb-0d7c-4e6d-8e40-9dc3bef3d77a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc5b2e2bce410309656bad5591a3df90781cc8bc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932225"
---
# <a name="mode-property-ado"></a>Mode プロパティ (ADO)
データを変更する使用可能なアクセス許可を示します、[接続](../../../ado/reference/ado-api/connection-object-ado.md)、[レコード](../../../ado/reference/ado-api/record-object-ado.md)、または[Stream](../../../ado/reference/ado-api/stream-object-ado.md)オブジェクト。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)値。 既定値、**接続**は**adModeUnknown**します。 既定値、**レコード**オブジェクトが**adModeRead**します。 既定値、 **Stream** 、基になるソースに関連付けられている (URL または既定値として、ソースとして使用して開いた**Stream**の**レコード**) は**adModeRead**します。 既定値、 **Stream**基になると関連付けられていません (メモリ内でインスタンス化された) ソースが**adModeUnknown**します。  
  
## <a name="remarks"></a>コメント  
 使用して、**モード**プロパティを設定または使用中で、プロバイダーによって現在の接続でアクセス許可を取得します。 設定することができます、**モード**プロパティ場合にのみ、**接続**オブジェクトが閉じられます。  
  
 **Stream**オブジェクトを開くために使用するソースから継承されているアクセス モードが指定されていない場合、 **Stream**オブジェクト。 たとえば場合、 **Stream**から開かれる、**レコード**として同じモードで開くことがその既定のオブジェクト、**レコード**。  
  
 このプロパティは読み取り/書き込み、オブジェクトが開いている間、オブジェクトが閉じており、読み取り専用です。  
  
> [!NOTE]
>  **リモート データ サービスの使用状況**クライアント側で使用すると**接続**オブジェクト、**モード**プロパティのみ設定できます**adModeUnknown**します。  
  
## <a name="applies-to"></a>適用対象  
  
||||  
|-|-|-|  
|[Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>関連項目  
 [IsolationLevel および Mode プロパティの例 (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel および Mode プロパティの例 (vc++)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
