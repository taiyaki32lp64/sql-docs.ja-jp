---
title: リターン コード |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- SQL Server Native Client OLE DB provider, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
ms.assetid: 7f7457e9-fce4-400c-82e5-ee02e9e811c6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 625d56a38d88b3cccbea1c75ad88917af1a6f6dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63228941"
---
# <a name="return-codes"></a>リターン コード
  最も基本的なレベルでは、メンバー関数は成功するか失敗するかのどちらかです。 それよりもやや詳細なレベルでは、関数は成功しても、その成功はアプリケーション開発者が意図した状態ではない場合があります。  
  
 OLE DB のリターン コードの詳細については、「[リターン コード (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631)」を参照してください。  
  
 ときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのメンバー関数が S_OK では、その関数は成功を返します。  
  
 ときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのメンバー関数が S_OK を返さない、全体的な成功または失敗を関数の OLE/COM HRESULT をアンパックする FAILED マクロと IS_ERROR マクロを確認できます。  
  
 FAILED または IS_ERROR が TRUE を返す場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのコンシューマーがメンバー関数の実行が失敗したことを保証します。 FAILED または IS_ERROR が FALSE と、HRESULT、それを返す場合は、S_OK を等しくなく、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのコンシューマーがいくつかの意味では、関数が成功したことを保証します。 コンシューマーからこの「成功した場合に情報を含む」を返す詳細の情報を取得できます、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのエラー インターフェイス。 また、関数 (、FAILED マクロに TRUE を返します) が失敗した明確にする場合、拡張エラー情報があるから、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのエラー インターフェイス。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのコンシューマーは、情報を含む DB_S_ERRORSOCCURRED"success"HRESULT 戻り値をよく遭遇します。 通常、DB_S_ERRORSOCCURRED を返すメンバー関数では、コンシューマーに状態値を提供するパラメーターが 1 つ以上定義されています。 コンシューマーは状態値パラメーターに返される情報以外のエラー情報を取得できない場合があるので、状態値が提供された場合にこの値を取得できるアプリケーション ロジックを実装することをお勧めします。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのメンバー関数は、成功コード S_FALSE を返しません。 すべて[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダーのメンバー関数は、常に成功した場合は S_OK を返します。  
  
## <a name="see-also"></a>参照  
 [エラー](errors.md)  
  
  
