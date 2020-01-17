---
title: レコード セット関連のエラー情報 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d3f8e8d9802b5d0c73af73aff20d929c188b9292
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924370"
---
# <a name="recordset-related-error-information"></a>レコードセット関連のエラー情報
バッチの処理中に、**状態**のプロパティ、**レコード セット**オブジェクト内の個別のレコードに関する情報は、**レコード セット**します。 バッチ更新が実行する前に、**状態**のプロパティ、 **Recordset**追加、変更および削除するレコードについての情報が反映されます。 後**UpdateBatch**が呼び出されて、**状態**プロパティは、操作の成否を示します。 レコード間を移動すると、**レコード セット**の値、**状態**プロパティに対する変更を現在のレコードの状態を説明します。
