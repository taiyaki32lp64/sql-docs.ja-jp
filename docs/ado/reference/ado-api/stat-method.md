---
title: Stat メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Stat
helpviewer_keywords:
- Stat method [ADO]
ms.assetid: 99a2b2d4-e6b1-4205-b011-72d024ea7240
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0538a3afae1e4c0bf4159d8ef6a42872f21ff6ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916868"
---
# <a name="stat-method"></a>Stat メソッド
に関する情報を取得、 [Stream](../../../ado/reference/ado-api/stream-object-ado.md)オブジェクト。  
  
## <a name="syntax"></a>構文  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>戻り値  
 A**長い**操作の状態を示す値。  
  
#### <a name="parameters"></a>パラメーター  
 *StatStg*  
 ストリームに関する情報が格納される、STATSTG 構造。 実装、 **Stat** ADO Stream オブジェクトによって使用されるメソッドがすべての構造体のフィールドでいっぱいになりません。  
  
 *StatFlag*  
 このメソッドが返さないこと、メンバーの一部、メモリ割り当て操作を節約できるよう、STATSTG 構造を指定します。 値は、STATFLAG 列挙から取得されます。 STATFLAG 列挙体が 2 つの値  
  
|定数|[値]|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>コメント  
 Stat ADO Stream オブジェクトに対して実装されるメソッドのバージョンは、STATSTG 構造体の次のフィールドに入力します。  
  
 *pwcsName*  
 STATFLAG_NONAME StatFlag 値とがある場合、ストリームの名前を含む文字列が指定されませんでした。  
  
 *cbSize*  
 バイト ストリームまたはバイト配列のサイズを指定します。  
  
 *mtime*  
 このストレージ、ストリーム、またはバイト配列の最終変更時刻を示します。  
  
 *ctime*  
 このストレージ、ストリーム、またはバイト配列の作成時間を示します。  
  
 *atime*  
 このストレージ、ストリームまたはバイト配列の最終アクセス時刻を示します。  
  
 STATFLAG_NONAME が StatFlag パラメーターで指定されている場合、ストリームの名前は返されません。  
  
 STATFLAG_NONAME が StatFlag パラメーターで指定されていないと、現在のストリームの名前はありません、この値は E_NOTIMPL になります。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
