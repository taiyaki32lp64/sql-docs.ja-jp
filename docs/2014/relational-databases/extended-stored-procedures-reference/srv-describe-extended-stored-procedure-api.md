---
title: srv_describe (拡張ストアド プロシージャ API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_describe
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_describe
ms.assetid: 2115600e-5ce7-4be0-9cd3-a1dd1fab0729
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 64910ce8bab155639a16cb065768c43fd86ac737
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127331"
---
# <a name="srvdescribe-extended-stored-procedure-api"></a>srv_describe (拡張ストアド プロシージャ API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 行内の特定の列について、列名および送信元と送信先のデータ型を定義します。  
  
## <a name="syntax"></a>構文  
  
```  
  
int srv_describe (  
SRV_PROC *  
srvproc  
,  
int  
colnumber  
,  
DBCHAR *  
column_name  
,  
int  
namelen  
,  
DBINT  
desttype  
,  
DBINT  
destlen  
,  
DBINT  
srctype  
,  
DBINT  
srclen  
,  
void *  
srcdata  
);  
  
```  
  
## <a name="arguments"></a>引数  
 *srvproc*  
 特定のクライアント接続のためのハンドル (ここでは、行を送信するクライアント) である SRV_PROC 構造体を指すポインターです。 この構造体には、アプリケーションとクライアントの間の通信やデータを管理するために、拡張ストアド プロシージャ API ライブラリで使用するすべての情報が格納されます。  
  
 *colnumber*  
 現時点では、サポートされません。 列は順番に記述する必要があります。 **srv_sendrow** を呼び出すには、事前にすべての列を記述しておく必要があります。  
  
 *column_name*  
 データが格納される列の名前を指定します。 列に名前を付けることは必須ではないので、このパラメーターは NULL になる場合があります。  
  
 *namelen*  
 *column_name* の長さをバイト数で指定します。 *namelen* が SRV_NULLTERM である場合は、*column_name* を NULL で終端する必要があります。  
  
 *desttype*  
 送信先の行内の列のデータ型を指定します。 これはクライアントに送信するデータ型です。 データが NULL の場合でも、データ型を指定する必要があります。詳しく、「[データ型 &#40;拡張ストアド プロシージャ API&#41;](data-types-extended-stored-procedure-api.md)」をご覧ください。  
  
 *destlen*  
 クライアントに送信するデータ長をバイト数で指定します。 NULL 値を許容しない固定長データ型の場合は、*destlen* が無視されます。 可変長データ型と NULL 値を許容する固定長データ型の場合、*destlen* は送信先データで使用できる最大長を指定します。  
  
 *srctype*  
 ソース データのデータ型を指定します。  
  
 *srclen*  
 ソース データの長さをバイト数で指定します。 固定長データ型の場合、この値は無視されます。  
  
 *srcdata*  
 特定の列に対応するソース データ アドレスを指定します。 **srv_sendrow** は呼び出されると、*colnumber* のデータを *srcdata* で探します。 このため、**srv_sendrow** を呼び出す前にこの引数を解放しないでください。 ソース データ アドレスは、**srv_sendrow** の呼び出しと呼び出しの間に **srv_setcoldata** を使用して変更できます。 別に **srv_setcoldata** を呼び出して列データを置き換えるか、**srv_senddone** を呼び出すまでは、*srcdata* に割り当てたメモリを解放しないでください。  
  
 *desttype* が SRVDECIMAL または SRVNUMERIC である場合、*srcdata* パラメーターは DBNUMERIC 構造体または DBDECIMAL 構造体を指すポインターである必要があります。そのとき、構造体の有効桁数と小数点以下桁数のフィールドには、必要な値を設定しておきます。 既定の有効桁数を指定するには DEFAULTPRECISION を、既定の小数点以下桁数を指定するには DEFAULTSCALE を使用できます。  
  
## <a name="returns"></a>戻り値  
 記述された列の番号を返します。 最初の列は列 1 です。 エラーが発生すると 0 を返します。  
  
## <a name="remarks"></a>コメント  
 **srv_sendrow** を初めて呼び出す前に、行内の各列に対して 1 回ずつ **srv_describe** 関数を呼び出しておく必要があります。 行内の列は任意の順で記述できます。  
  
 完全な結果セットの送信が完了する前に行内の各列のソース データの位置および長さを変更するには、それぞれ **srv_setcoldata** と **srv_setcollen** を使用します。  
  
 データ型および拡張ストアド プロシージャ API のデータ型変換について詳しくは、「[データ型 &#40;拡張ストアド プロシージャ API&#41;](data-types-extended-stored-procedure-api.md)」をご覧ください。  
  
 アプリケーションで使用する列名が Unicode である場合は、**srv_describe** を呼び出す前に、列名をサーバーのマルチバイト コード ページに変換する必要があります。 詳しくは、「[Unicode データおよびサーバー コード ページ](../extended-stored-procedures-programming/unicode-data-and-server-code-pages.md)」をご覧ください。  
  
> [!IMPORTANT]  
>  拡張ストアド プロシージャのソース コードを十分に確認し、コンパイル済み DLL を、運用サーバーにインストールする前にテストする必要があります。 セキュリティの確認およびテストについて詳しくは、[Microsoft の Web サイト](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)をご覧ください。  
  
## <a name="see-also"></a>参照  
 [srv_sendrow &#40;拡張ストアド プロシージャ API&#41;](srv-sendrow-extended-stored-procedure-api.md)   
 [srv_setutype &#40;拡張ストアド プロシージャ API&#41;](srv-setutype-extended-stored-procedure-api.md)   
 [srv_setcoldata &#40;拡張ストアド プロシージャ API&#41;](srv-setcoldata-extended-stored-procedure-api.md)  
  
  
