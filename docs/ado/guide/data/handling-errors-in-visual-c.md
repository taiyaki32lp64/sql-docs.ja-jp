---
title: Visual C でのエラー処理 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- errors [ADO], Visual C++
- Visual C++ error handling [ADO]
ms.assetid: b7576f07-020a-45f7-9e79-b5756f33f7ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb9eb29a78c3ec5f47e3ff09641ba04ca01d204a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925124"
---
# <a name="handling-errors-in-visual-c"></a>Visual C++ でエラーを処理する
COM では、ほとんどの操作は、関数が正常に完了したかどうかを示す HRESULT のリターン コードを返します。 #Import ディレクティブでは、各「生」のメソッドまたはプロパティをラッパー コードを生成し、返された HRESULT を確認します。 場合は、HRESULT が障害を示してラッパー コードは、引数として HRESULT のリターン コードで呼び出し元の _com_issue_errorex() によって COM エラーをスローします。 COM エラー オブジェクトをキャッチ、 **try catch**ブロックします。 (効率性のためは、_com_error オブジェクトへの参照をキャッチします)。  
  
 ただし、これらは、ADO エラー: ADO 操作の失敗による結果です。 基になるプロバイダーから返されるエラーの表示として**エラー**内のオブジェクト、**接続**オブジェクトの**エラー**コレクション。  
  
 #Import ディレクティブは、メソッド、および ado で宣言されたプロパティのエラー処理ルーチンを作成するだけです。 ただし、独自のエラー チェック マクロまたはインライン関数を記述することで、この同じエラー処理機構の利点を実行できます。 例についてはトピック C++® の拡張機能を参照してください。
