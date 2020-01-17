---
title: SSIS パッケージの形式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cfe0e5dc-5be3-4222-b721-fe83665edd94
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f59ed0eee86f17fdda568caa5c1a1dc7252c6d9c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055349"
---
# <a name="ssis-package-format"></a>SSIS パッケージの形式
  最新のリリースの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]では、形式の読み取りとパッケージの比較を容易にするために、パッケージの形式 (.dtsx file) に大幅な変更が加えられました。 変更の競合またはバイナリ形式で格納されている変更が含まれていないパッケージをより確実にマージできます。  
  
 最新の DTSX パッケージ ファイル形式を表示するを参照してください[ \[MS-DTSX\]:。データ変換サービス パッケージの XML ファイル形式の仕様](https://go.microsoft.com/fwlink/?LinkId=233251)します。  
  
 ファイル形式の変更の概要を次に示します。 これらの変更のコード例については、「 [SQL Server 2012 のパッケージ形式の変更](https://go.microsoft.com/fwlink/?LinkId=233255)」を参照してください。  
  
-   .dtsx ファイルの読みやすさとわかりやすさを向上させるために、形式規則が適用されています。  
  
-   形式はより簡潔になっています。 プロパティごとの個別の要素は属性として残っています。ただし、PackageFormatVersion は除きます。 属性はアルファベット順に一覧表示され、既定値を持つプロパティはもう残っていません。 最後に、複数回出現する要素は親要素内に含まれています。  
  
-   他のオブジェクトで参照できるパッケージ内のほとんどのオブジェクトに、パッケージ XML で定義された `refId` 属性が割り当てられています。 系列 ID の代わりに `refID`が残っています。 系列 ID は今でもランタイム内で使用され、パッケージを読み込むと再生成されます。  
  
     `refId` 値は、GUID または整数値よりも読みやすくわかりやすい一意の文字列です。 この文字列は、以前のリリースの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]でパッケージ構成に使用されたパス値に似ています。  
  
     2 つのバージョンのパッケージ間の変更をマージする場合は、検索/置換操作で `refId` を使用して、そのオブジェクトへのすべての参照が正しく更新されたことを確認できます。  
  
-   レイアウト情報は CData セクションにあります。  
  
-   注釈はクリア テキストで残ります。 これにより、ドキュメントの自動生成に関する情報を簡単に抽出できます。  
  
  
