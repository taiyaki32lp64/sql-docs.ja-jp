---
title: 編集モードの決定 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22e63bad49586bbbc1a5616114055779cd3ea041
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925548"
---
# <a name="determining-edit-mode"></a>編集モードの決定
ADO では、現在のレコードに関連付けられている編集のバッファーを保持します。 **EditMode**プロパティをこのバッファーに変更が加えられましたかどうか、または新しいレコードが作成されているかどうかを示します。 使用**EditMode**現在のレコードの編集状態を確認します。 編集プロセスが中断された場合は、保留中の変更をテストして使用する必要があるかどうかを判断、 **Update**または**CancelUpdate**メソッド。  
  
 **EditMode**のいずれかを返します、 **EditModeEnum**定数は、次の表に記載されています。  
  
|定数|説明|  
|--------------|-----------------|  
|**adEditNone**|進行中の編集操作がないことを示します。|  
|**adEditInProgress**|現在のレコード内のデータが変更されたが、保存されないことを示します。|  
|**adEditAdd**|示します、 **AddNew**メソッドが呼び出された、コピー バッファーの現在のレコードは新しいレコードをデータベースに保存されていません。|  
|**adEditDelete**|現在のレコードが削除されたことを示します。|  
  
 **EditMode**現在のレコードがある場合にのみ、有効な値を返すことができます。 **EditMode**場合はエラーを返します**BOF**または**EOF**は**True**または現在のレコードが削除されている場合。
