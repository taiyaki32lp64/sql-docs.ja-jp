---
title: 型のマッピング (SybaseToSQL) の編集 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 513f071a-d5e6-4ed5-acca-269bf76323c5
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: cd8dfbd7aa4205424c45861f6ada1113f76d344e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029172"
---
# <a name="edit-type-mapping-sybasetosql"></a>型のマッピングの編集 (SybaseToSQL)
**型マッピングの編集** ダイアログ ボックスでは、ソースと変換先のデータベース オブジェクトの間で型をマップする方法を指定することができます。  
  
複数の場所では、このダイアログ ボックスを表示できます。  
  
-   ソース データベースまたはデータベース オブジェクトを選択すると、**型マッピングの**メタデータ エクスプ ローラーの右側にタブが表示されます。 クリックして**追加**、新しい型のマッピングを追加する**編集**既存の型マッピングを変更します。  
  
-   **ツール**メニューの **プロジェクト設定**または**プロジェクト設定の既定の**します。 結果として得られる ダイアログ ボックスで、次のように選択します。**型マッピングの**します。 クリックして**追加**、新しい型のマッピングを追加する**編集**既存の型マッピングを変更します。  
  
テーブルに固有の型のマッピングは、データベースをオーバーライドし、プロジェクトの種類のマッピング。 データベース固有のマッピングは、project のマッピングをオーバーライドします。  
  
## <a name="options"></a>および  
**ソースの種類**  
マップするソース データの種類の選択、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型。  
  
データ型が可変長の場合は、次のフィールドが下に表示されます**ソースの種類**:  
  
**From**  
このマッピングの最小の長さを指定します。 たとえば、 **nchar**データ型の場合は、このマッピングを開始位置として範囲を指定するための 10 を入力する**nchar(10)** します。  
  
**変換先**  
このマッピングの最大長を指定します。 たとえば、 **nchar**データ型、終了範囲のこのマッピングであることを指定する 20 を入力する**nchar (20) 型**します。  
  
**ターゲットの種類**  
選択、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ソースのデータ型がマップされているデータ型。 SSMA がテーブルまたはストアド プロシージャを作成するときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元のデータ型は、このデータ型に変更されます。  
  
データ型が可変長の場合は、次のフィールドが下に表示されます**ターゲットの種類**:  
  
**Replace with**  
このマッピングのターゲットの長さを指定します。 たとえば、 **nvarchar**データ型の場合は、指定したソースのデータ型にマップすることを指定する 20 を入力する**nvarchar (20)** します。  
  
