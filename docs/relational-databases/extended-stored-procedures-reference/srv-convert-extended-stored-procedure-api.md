---
title: srv_convert (拡張ストアド プロシージャ API) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_convert
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_convert
ms.assetid: 216b4a31-786e-4361-8a33-e5f6e9790f90
author: rothja
ms.author: jroth
ms.openlocfilehash: b6ba4c356411800dc7c5e52907b0baccd5682f09
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064142"
---
# <a name="srv_convert-extended-stored-procedure-api"></a>srv_convert (拡張ストアド プロシージャ API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 データを別のデータ型に変換します。  
  
## <a name="syntax"></a>構文  
  
```  
  
int srv_convert (  
SRV_PROC *  
srvproc  
,  
int  
srctype  
,  
void *  
src  
,  
DBINT  
srclen  
,  
int  
desttype  
,  
void *  
  dest  
,  
DBINT  
destlen  
);  
```  
  
## <a name="arguments"></a>引数  
 *srvproc*  
 特定のクライアント接続のためのハンドルである SRV_PROC 構造体を指すポインターです。 この構造体には、アプリケーションとクライアントの間の通信やデータを管理するために、拡張ストアド プロシージャ API で使用するすべての制御情報が格納されます。 *srvproc* ハンドルが指定されている場合、エラーが発生すると、拡張ストアド プロシージャ API エラー ハンドラー関数に渡されます。  
  
 *srctype*  
 変換元データのデータ型を指定します。 このパラメーターには、拡張ストアド プロシージャ API の任意のデータ型を使用できます。  
  
 *src*  
 変換元データへのポインターです。 このパラメーターには、拡張ストアド プロシージャ API の任意のデータ型を使用できます。  
  
 *srclen*  
 変換元データの長さをバイト数で指定します。 *srclen* が 0 である場合、**srv_convert** は出力先変数に NULL を格納します。 0 以外の場合、固定長のデータ型ではこのパラメーターが無視され、変換元データが NULL であると見なされます。 SRVCHAR データ型のデータの場合、長さが -1 であれば、文字列が NULL 終端であることを示します。  
  
 *desttype*  
 変換先のデータ型を指定します。 このパラメーターには、拡張ストアド プロシージャ API の任意のデータ型を使用できます。  
  
 *dest*  
 変換したデータを受け取る出力先変数を指すポインターです。 このポインターが NULL である場合、ユーザーが指定したエラー ハンドラーがあれば **srv_convert** はそのエラー ハンドラーを呼び出し、-1 を返します。  
  
 *desttype* が SRVDECIMAL または SRVNUMERIC である場合、*dest* パラメーターは DBNUMERIC 構造体または DBDECIMAL 構造体を指すポインターである必要があります。その際、構造体の有効桁数と小数点以下桁数のフィールドには、必要な値を設定しておきます。 既定の有効桁数を指定するには DEFAULTPRECISION を、既定の小数点以下桁数を指定するには DEFAULTSCALE を使用できます。  
  
 *destlen*  
 出力先変数の長さをバイト数で指定します。 固定長データ型の場合、このパラメーターは無視されます。 出力先変数が SRVCHAR 型である場合、*destlen* の値を出力先バッファー領域全体の長さにする必要があります。 SRVCHAR 型または SRVBINARY 型の出力先変数の長さが -1 であれば、十分な領域があることを示します。 出力先変数が *srvchar* 型である場合、長さを -1 にすると文字列が NULL 終端になります。  
  
## <a name="returns"></a>戻り値  
 データ型の変換が成功した場合は、変換後のデータの長さをバイト数で返します。 **srv_convert** がサポートしていないデータ型への変換要求を受けた場合は、開発者の定義したエラー ハンドラーがあればそれを呼び出し、グローバル エラー番号を設定して -1 を返します。  
  
## <a name="remarks"></a>Remarks  
 **srv_willconvert** 関数は、特定の変換が可能かどうかを判断する関数です。  
  
 概数データ型 SRVFLT4 または SRVFLT8 への変換では、有効桁数の一部が失われることがあります。 概数データ型 SRVFLT4 または SRVFLT8 から SRVCHAR または SRVTEXT への変換でも有効桁数の一部が失われることがあります。  
  
 SRVFLT*x*、SRVINT*x*、SRVMONEY、SRVMONEY4、SRVDECIMAL、SRVNUMERIC のいずれかに変換した結果、数値が出力先の最大値より大きい場合はオーバーフロー、最小値より小さい場合はアンダーフローになることがあります。 SRVCHAR または SRVTEXT への変換時にオーバーフローが発生した場合、変換後の値の最初の文字はエラーを示すアスタリスク (*) なります。  
  
 SRVCHAR を SRVBINARY に変換する場合、文字列に先頭ビット 0 が含まれているかどうかに関係なく、**srv_convert** は SRVCHAR を 16 進数として解釈します。 SRVBINARY から SRVCHAR に変換する場合、**srv_convert** は先頭ビット 0 のない 16 進数文字列を作成します。 それ以外の、SRVBINARY データ型からの変換または SRVBINARY データ型への変換ではビット コピーを忠実に行います。  
  
 場合によっては、同じデータ型への変換が役立つことがあります。 たとえば、*destlen* を -1 にして SRVCHAR から SRVCHAR に変換すると、文字列に NULL 終端が追加されます。  
  
 データ型および拡張ストアド プロシージャ API のデータ型変換について詳しくは、「[データ型 &#40;拡張ストアド プロシージャ API&#41;](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md)」をご覧ください。  
  
 **srv_convert** 関数は、次の理由で変換に失敗することがあります。  
  
-   要求された変換がサポートされていない。  
  
-   変換の結果、出力先変数で切り捨て、オーバーフロー、または有効桁数の損失が発生した。  
  
-   文字列を数値データ型に変換するときに構文エラーが発生した。  
  
> [!IMPORTANT]  
>  拡張ストアド プロシージャのソース コードを十分に確認し、コンパイル済み DLL を、運用サーバーにインストールする前にテストする必要があります。 セキュリティの確認およびテストについて詳しくは、[Microsoft の Web サイト](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)をご覧ください。  
  
## <a name="see-also"></a>参照  
 [srv_setutype &#40;拡張ストアド プロシージャ API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-setutype-extended-stored-procedure-api.md)   
 [srv_willconvert &#40;拡張ストアド プロシージャ API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-willconvert-extended-stored-procedure-api.md)  
  
  
