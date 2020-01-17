---
title: パラメーター ヒント (IntelliSense)
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Parameter Info option [IntelliSense]
- stored function parameter completion [Intellisense]
- language references [SQL Server]
- IntelliSense [SQL Server], Parameter Info option
ms.assetid: 56c2aac9-c65c-4679-b62c-d9f689876dde
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b842f35c2852ce6ed607e943199bb322823651b9
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75242007"
---
# <a name="parameter-info-intellisense"></a>パラメーター ヒント (IntelliSense)
  IntelliSense [!INCLUDE[msCoName](../../includes/msconame-md.md)]の [**パラメーターヒント**] オプションを使用すると、パラメーターの一覧が表示され、関数またはストアドプロシージャで必要とされるパラメーターの数、名前、および型に関する情報を参照できます。 太字で表示されるパラメーターは、入力中の関数やストアド プロシージャで次に必要なパラメーターを示しています。  
  
 パラメーター リストは入れ子にされた関数についても表示されます。 他の関数のパラメーターとして関数を入力する場合、パラメーター リストには内部関数のパラメーターが表示されます。 内部関数のパラメーター リストが完了すると、パラメーター リストには再び外部関数のパラメーターが表示されます。  
  
#### <a name="to-view-parameter-info-for-functions-or-stored-procedures"></a>関数またはストアド プロシージャのパラメーター ヒントを表示するには  
  
1.  関数の場合、名前の後に、通常と同じように左かっこを入力すると、パラメーター リストが表示されます。 ストアド プロシージャの場合、名前を入力した後に、通常と同じようにスペースを入力すると、プロシージャのパラメーターに関する情報が表示されます。  
  
     IntelliSense は、関数の宣言全体またはストアド プロシージャのパラメーターをポップアップ ウィンドウとして挿入ポイントのすぐ下に表示します。 リスト内の最初のパラメーターは太字で表示されます。  
  
2.  パラメーターを入力していくと、次に入力する必要のあるパラメーターに応じて太字が変わります。  
  
3.  Esc キーを押してリストを閉じるか、関数が完了するまで入力を続けます。  
  
     関数の場合、右かっこを入力するとパラメーター リストも閉じます。  
  
#### <a name="to-manually-start-parameter-info"></a>パラメーター ヒントを手動で起動するには  
  
1.  
  **[編集]** メニューの **[IntelliSense]** をポイントし、 **[パラメーター ヒント]** をクリックします。  
  
2.  Ctrl&lt;/localizedText&gt; キーと &lt;localizedText&gt;Shift&lt;/localizedText&gt; キーを押しながら &lt;localizedText&gt;Space&lt;/localizedText&gt; キーを押します。  
  
 詳細については、「[IntelliSense の構成 &#40;SQL Server Management Studio&#41;](configure-intellisense-sql-server-management-studio.md)」を参照してください。  
  
> [!NOTE]  
>  
  **[パラメーター ヒント]** オプションは、[!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターと XML クエリ エディターでのみ使用できます。  
  
  
