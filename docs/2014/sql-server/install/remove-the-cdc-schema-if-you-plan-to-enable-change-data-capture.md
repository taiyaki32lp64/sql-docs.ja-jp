---
title: 変更データ キャプチャを有効にする場合は、cdc スキーマを削除する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- cdc schema
- change data capture
ms.assetid: 6a84aa25-0f31-4be3-b2dd-4f249b8254ae
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cc580a6032a19eb8248759669278f8730fc617cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092949"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>変更データ キャプチャを有効にする場合に cdc スキーマを削除する
  データベースには、既に cdc スキーマが含まれています。 アップグレード後に変更データ キャプチャを有効にする場合は、まずこの cdc スキーマを削除する必要があります。 データベースで変更データ キャプチャを有効にすると、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]によって、cdc という名前の新しいスキーマが作成されます。  
  
  
