---
title: レコードの追加 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- editing data [ADO], AddNew method
- editing data [ADO], adding data
ms.assetid: dd34669e-6f06-403b-9241-1c85c82aecc2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f4ec0934fbf75de18f460abae84b8117e99f452
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926265"
---
# <a name="adding-records-to-a-recordset"></a>レコードをレコード セットに追加します。
使用して、 **AddNew**メソッドを作成し、既存の新しいレコードの初期化を**Recordset**します。 使用することができます、**サポート**メソッドを**CursorOptionEnum**の値**adAddNew**を現在のレコードを追加できるかどうかを確認する**レコードセット**オブジェクト。

 呼び出した後、 **AddNew**メソッドでは、新しいレコードが現在のレコードになり、を呼び出した後は、最新の状態、 **Update**メソッド。 場合、 **Recordset**オブジェクトは、ブックマークをサポートしていない、別のレコードに移動すると、新しいレコードにアクセスすることができません。 そのため、カーソルの種類に応じてする必要がありますを呼び出す、 **Requery**メソッドを新しいレコードにアクセスできるようにします。

 呼び出す場合**AddNew** ADO を呼び出し、現在のレコードを編集している間、または新しいレコードを追加するときに、 **Update**を保存する方法の変更し、新しいレコードを作成します。

 このセクションでは、次のトピックを扱います。

-   [AddNew を使用してレコードを追加する](../../../ado/guide/data/adding-records-using-addnew.md)

-   [複数のフィールドの追加](../../../ado/guide/data/adding-multiple-fields.md)

-   [編集モードの決定](../../../ado/guide/data/determining-edit-mode.md)

-   [イミディエイト モードとバッチ モードで AddNew を使用する](../../../ado/guide/data/using-addnew-in-immediate-and-batch-modes.md)
