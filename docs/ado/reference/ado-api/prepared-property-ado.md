---
title: Prepared プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Prepared
helpviewer_keywords:
- Prepared property [ADO]
ms.assetid: 11ca8825-765e-4bb4-a6ce-3f6564ad8755
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ee7a94a06aa574c84c01cb8b9d05ebfcdf327d44
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917596"
---
# <a name="prepared-property-ado"></a>Prepared プロパティ (ADO)
コンパイル済みのバージョンを保存するかどうかを示す、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)実行前にします。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**ブール**値に設定**True**コマンドを準備することを示します。  
  
## <a name="remarks"></a>コメント  
 使用して、**準備**プロパティで指定されたクエリの準備済み (またはコンパイル済み) のバージョンを保存するプロバイダーが、 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)前に、プロパティ、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクトの最初に実行します。 これは、コマンドの最初の実行を遅い可能性がありますが、プロバイダーはパフォーマンスを向上させると、その後の実行のコンパイル済みのバージョンのコマンドを使用して、プロバイダーがコマンドをコンパイルするとします。  
  
 プロパティが場合**False**、プロバイダーが実行、**コマンド**コンパイル済みのバージョンを作成せずに直接オブジェクト。  
  
 このプロパティ設定されている場合に、エラーを返す可能性がありますが、プロバイダーがコマンドの準備をサポートしていない場合**True**します。 コマンドとセットを準備する要求を無視しますプロバイダーでエラーが返されない場合、**準備**プロパティを**False**します。  
  
## <a name="applies-to"></a>適用対象  
 [Command オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Prepared プロパティの例 (VB)](../../../ado/reference/ado-api/prepared-property-example-vb.md)   
 [Prepared プロパティの例 (VC++)](../../../ado/reference/ado-api/prepared-property-example-vc.md)   
