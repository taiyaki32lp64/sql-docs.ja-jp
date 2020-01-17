---
title: データ処理拡張機能の削除 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- deleting data processing extensions
- data processing extensions [Reporting Services], removing
- removing data processing extensions
ms.assetid: 1d89e32b-0631-44f6-8178-a57fb791d26d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9f5dfd3a6a7615fa3fd91c917bba6dbf0808f0f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63163972"
---
# <a name="removing-a-data-processing-extension"></a>データ処理拡張機能の削除
  データ処理拡張機能を削除する場合は、データ処理拡張機能の **Extension** 要素を構成ファイルから削除するだけです。 レポート サーバーに加えてレポート デザイナーにもエントリを作成した場合は、RSReportServer.config ファイルと RSReportDesigner.config ファイルの両方から **Extension** 要素を削除します。 構成情報を削除すると、そのコンポーネントではデータ処理拡張機能を使用できなくなります。  
  
## <a name="see-also"></a>関連項目  
 [Reporting Services の拡張機能](../reporting-services-extensions.md)   
 [データ処理拡張機能の実装](implementing-a-data-processing-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../reporting-services-extension-library.md)  
  
  
