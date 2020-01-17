---
title: SET COLLATE コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set collate command [ODBC]
ms.assetid: 00efbcd4-fea8-4061-86a5-82de413cb753
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a7701edd4c1902399f1d040ae9027365bdf04ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997745"
---
# <a name="set-collate-command"></a>SET COLLATE コマンド
後続のインデックス作成および並べ替え操作では、文字列フィールドの照合順序を指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>引数  
 *cSequenceName*  
 照合順序を指定します。 使用可能な照合シーケンスのオプションは、次の表で説明します。  
  
|および|[言語]|  
|-------------|--------------|  
|オランダ語|オランダ語|  
|GENERAL|英語、フランス語、ドイツ語、最新のスペイン語、ポルトガル語、およびその他の西ヨーロッパ言語|  
|ドイツ語|ドイツの電話帳順序 (DIN)|  
|アイスランド|アイスランド語|  
|マシン|マシン (以前のバージョンの FoxPro の既定の照合順序)|  
|NORDAN|ノルウェー語、デンマーク語|  
|スペイン語|従来のスペイン語|  
|SWEFIN|スウェーデン語、フィンランド語|  
|UNIQWT|一意の重み|  
  
> [!NOTE]  
>  スペイン語のオプションを指定するときに*ch*を並べ替えるの間で 1 つの文字は、 *c*と*d*、および*ll*間並べ替えます*l*と*m*します。  
  
 照合順序のシーケンスのオプションをリテラル文字の文字列として指定した場合は、引用符で囲みますオプションを必ず。  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 マシンは既定の照合順序のシーケンスのオプションであり、シーケンス Xbase のユーザーが精通をします。 文字は、現在のコード ページに表示されるように並べ替えられています。  
  
 [全般] は、米国およびヨーロッパのユーザーの方が望ましい可能性があります。 文字は、現在のコード ページに表示されるように並べ替えられています。 FoxPro バージョン 2.5 より前のインデックスが作成されていてを使用して、**上限**() または**低い**() 関数の文字のフィールドを一貫性のある大文字と小文字に変換します。 FoxPro バージョン 2.5 以降は、代わりに、一般的な照合順序のシーケンス オプションを指定し、省略することができます、**上限**() 変換します。  
  
 マシンと .idx ファイルを作成するかどうか以外の照合順序オプションを指定する場合は、compact .idx が常に作成します。  
  
 SET("COLLATE") を使用して、現在の照合順序を返します。  
  
 使用してデータ ソースの照合順序を指定することができます、 [ODBC Visual FoxPro セットアップ ダイアログ ボックス](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)または Collate キーワードで、接続文字列を使用して[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)します。 これは、次のコマンドを発行するのと同じです。  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>コメント  
 部単位印刷設定は、サポートされている言語のいずれかのアクセント付き文字を含む注文テーブルにできます。 部単位印刷設定の設定を変更すると、既に開かれているインデックスの照合順序に影響しません。 Visual FoxPro には、さまざまな種類の同じフィールドの場合でも、インデックスを作成する柔軟性を提供する既存のインデックスを自動的に維持します。  
  
 たとえば、[全般] に設定を部単位印刷設定でインデックスを作成し、部単位印刷設定設定がスペイン語に変更された後で、インデックスは一般的な照合順序を保持します。  
  
## <a name="see-also"></a>関連項目  
 [ODBC Visual FoxPro セットアップ ダイアログ ボックス](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
