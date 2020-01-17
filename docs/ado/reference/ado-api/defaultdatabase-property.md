---
title: DefaultDatabase プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::DefaultDatabase
helpviewer_keywords:
- DefaultDatabase property
ms.assetid: 41e8a8dd-e69c-4a09-8736-93502e01961c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c78dfdc476dc9dcf599fcfe7cb87bd5e1a39d281
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919160"
---
# <a name="defaultdatabase-property"></a>DefaultDatabase プロパティ
既定のデータベースを示す、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**文字列**プロバイダーから使用可能なデータベースの名前に評価される値。  
  
## <a name="remarks"></a>コメント  
 使用して、 **DefaultDatabase**プロパティを設定または特定の既定のデータベースの名前を返す**接続**オブジェクト。  
  
 既定のデータベースがある場合、SQL 文字列は、そのデータベース内のオブジェクトにアクセスする構文が不適切なを使用する場合があります。 指定されている以外のデータベースでオブジェクトにアクセスする、 **DefaultDatabase**プロパティ、目的のデータベース名でオブジェクト名を修飾する必要があります。 接続時に、プロバイダーが既定のデータベース情報を書き込み、 **DefaultDatabase**プロパティ。 一部のプロバイダーは接続ごとに 1 つだけデータベースを許可する、その場合で変更することはできません、 **DefaultDatabase**プロパティ。  
  
 いくつかのデータ ソースおよびプロバイダーは、この機能に対応していないと、エラーまたは空の文字列を返す可能性があります。  
  
> [!NOTE]
>  **リモート データ サービスの使用状況**このプロパティはクライアント側で使用可能な**接続**オブジェクト。  
  
## <a name="applies-to"></a>適用対象  
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Provider および DefaultDatabase プロパティの例 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Provider および DefaultDatabase プロパティの例 (VC++)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vc.md)   
