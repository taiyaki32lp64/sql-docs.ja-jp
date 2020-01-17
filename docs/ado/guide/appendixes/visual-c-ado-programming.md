---
title: Visual C での ADO プログラミング |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO]
ms.assetid: 11233b96-e05c-4221-9aed-5f20944b0f1c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1890d554367b2a21bcd46a6d2ebddf00013957e6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926423"
---
# <a name="visual-c-ado-programming"></a>Visual C++ での ADO プログラミング
ADO の API リファレンスには、ADO アプリケーション プログラミング インターフェイス (API)、Microsoft Visual Basic に似た構文を使用しての機能について説明します。 ADO のプログラマが Visual Basic、Visual C などのさまざまな言語を使用する対象とするユーザーには、すべてのユーザーが、(としない場合、 **#import**ディレクティブ)、および Visual j (ADO と WFC クラス パッケージ) にします。  

> [!NOTE]
> Microsoft では、2004 年 Visual j のサポートが終了しました。

 このような多様性に対応するために、 [Visual C++ 構文のインデックス用の ADO](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)機能、パラメーター、例外的な動作、およびでは、API での一般的な説明へのリンクに Visual C の言語固有の構文を提供参照。  
  
 ADO は COM (コンポーネント オブジェクト モデル) インターフェイスで実装されます。 ただし、他よりも、特定のプログラミング言語で COM を使用するプログラマにとって容易になります。 たとえば、自体、詳細な情報を Visual C プログラマに参加する必要がありますが、Visual Basic プログラマにとっての COM の使用のほぼすべての詳細は暗黙的に処理されます。  
  
 次のセクションでは、ADO を使用して、C および C++ のプログラマのための詳細を集計して、 **#import**ディレクティブ。 COM に固有のデータ型に焦点を当てます (**バリアント**、 **BSTR**、および**SafeArray**)、およびエラー処理 (_com_error)。  
  
## <a name="using-the-import-compiler-directive"></a>#Import コンパイラ ディレクティブを使用します。  
 **#Import** Visual C コンパイラ ディレクティブが ADO メソッドとプロパティの使用を簡略化します。 ディレクティブは、ado (Msado15.dll) などのタイプ ライブラリを含むファイルの名前を受け取り、typedef 宣言、インターフェイス、および列挙定数のスマート ポインターを含むヘッダー ファイルを生成します。 各インターフェイスがカプセル化され、またはクラスでラップします。  
  
 クラス (メソッドまたはプロパティの呼び出し) 内の各操作については、宣言操作を直接 (つまり、「生」の形式、操作)、呼び出すと、生の操作を呼び出すし、succ を実行する操作が失敗した場合は、COM エラーをスローする宣言essfully します。 操作がプロパティの場合、Visual Basic のような構文のある操作の代替構文を作成できるコンパイラ ディレクティブは通常があります。  
  
 プロパティの値を取得する操作は、フォームの名前を持つ**取得**_プロパティ_します。 プロパティの値を設定する操作は、フォームの名前を持つ**配置**_プロパティ_します。 ADO オブジェクトへのポインターのプロパティの値を設定する操作は、フォームの名前を持つ**PutRef**_プロパティ_します。  
  
 これらの形式の呼び出しでプロパティを設定または取得できます。  
  
```cpp
variable = objectPtr->GetProperty(); // get property value   
objectPtr->PutProperty(value);       // set property value  
objectPtr->PutRefProperty(&value);   // set property with object pointer  
```
  
## <a name="using-property-directives"></a>プロパティのディレクティブを使用します。  
 **__Declspec(property...)** コンパイラ ディレクティブは、Microsoft 固有の C 言語拡張機能に代替構文は、プロパティとして使用される関数を宣言します。 その結果、設定したり、Visual Basic に似た方法でプロパティの値を取得できます。 たとえば、設定でき、この方法でプロパティを取得します。  
  
```cpp
objectPtr->property = value;        // set property value  
variable = objectPtr->property;     // get property value  
```
  
 通知コードする必要はありません。  
  
```cpp
objectPtr->PutProperty(value);      // set property value  
variable = objectPtr->GetProperty;  // get property value  
```
  
 コンパイラは、適切な生成**取得** _-_ 、**配置**-、または**PutRef**_プロパティ_代替構文は宣言されており、プロパティがされているかどうかに基づいて、呼び出しの読み取りまたは書き込み。  
  
 **__Declspec(property...)** コンパイラ ディレクティブでのみ宣言できます**取得**、**配置**、または**取得**と**配置**関数の代替構文。 読み取り専用操作のみがある、**取得**宣言です書き込み専用の操作のみが、**配置**宣言です。 操作はどちらも読み取りおよび書き込みの両方がある**取得**と。**配置**宣言します。  
  
 2 つだけ宣言はこのディレクティブを指定します。ただし、各プロパティには、次の 3 つのプロパティ関数があります。**取得**_プロパティ_、**配置**_プロパティ_、および**PutRef**_プロパティ_します。 その場合は、プロパティの 2 つの形式では、代替構文があります。  
  
 たとえば、**コマンド**オブジェクト**ActiveConnection**プロパティが、別の構文で宣言された**取得**_ActiveConnection_と**PutRef**_ActiveConnection_します。 **PutRef**-たいので、実際が通常開いている状態に、構文は、適切な選択**接続**オブジェクト (つまり、**接続**オブジェクト ポインター) このプロパティ。 一方で、**レコード セット**オブジェクトが**取得**-、**配置**-、および**PutRef**_ActiveConnection_、操作が別の構文ではありません。  
  
## <a name="collections-the-getitem-method-and-the-item-property"></a>コレクション、GetItem メソッドをおよび項目のプロパティ  

 ADO など、いくつかのコレクションを定義する**フィールド**、**パラメーター**、**プロパティ**、および**エラー**します。 Visual C で、 **GetItem (_インデックス_)** メソッドは、コレクションのメンバーを返します。 *インデックス*は、**バリアント**、この値は、コレクション内のメンバーの数値インデックスまたは、メンバーの名前を含む文字列。  
  
 **__Declspec(property...)** コンパイラ ディレクティブを宣言、**項目**プロパティとして各コレクションに別の構文の基本的な**37-1getitem ()** メソッド。 代替構文は、角かっこを使用して、配列参照するようになります。 一般に、2 つの形式は、次のようになります。  
  
```cpp
  
      collectionPtr->GetItem(index);  
collectionPtr->Item[index];  
```
  
 などのフィールドに値を割り当てる、 **Recordset**という名前のオブジェクト **_rs_** から派生した、**作成者**のテーブル**pubs**データベース。 使用して、 **Item()** 、3 番目にアクセスするプロパティ**フィールド**の**Recordset**オブジェクト**フィールド**コレクション (コレクションのインデックスはから0;3 番目のフィールドがという名前の想定 **_au\_fname_** )。 呼び出して、 **Value()** メソッドを**フィールド**文字列値を代入するオブジェクト。  
  
 これで表現できる Visual Basic では、次の 4 つの方法 (Visual Basic に最後の 2 つのフォームが固有; 他の言語には、相当するはありません)。  
  
```cpp
rs.Fields.Item(2).Value = "value"  
rs.Fields.Item("au_fname").Value = "value"  
rs(2) = "value"  
rs!au_fname = "value"  
```
  
 Visual C で上記の最初の 2 つのフォームには。  
  
```cpp
rs->Fields->GetItem(long(2))->PutValue("value");   
rs->Fields->GetItem("au_fname")->PutValue("value");  
```
  
 \- または - (の代替構文を**値**もプロパティが表示されます)  
  
```cpp
rs->Fields->Item[long(2)]->Value = "value";  
rs->Fields->Item["au_fname"]->Value = "value";  
```
  
 コレクションを反復処理する例については、「ADO 参照」の「ADO コレクション」セクションを参照してください。  
  
## <a name="com-specific-data-types"></a>COM に固有のデータ型  
 一般に、任意の Visual Basic データ型が ADO の API リファレンスを検索するには、同等の Visual C があります。 などの標準的なデータ型が含まれます**unsigned char** Visual basic**バイト**、**短い**の**整数**、および**長い**の**長い**します。 構文 Indexesto ファイルの場所では、オペランドの特定のメソッドまたはプロパティの必要なものだけを参照してください。  
  
 このルールの例外は、COM に固有のデータ型は。**Variant**、 **BSTR**、および**SafeArray**します。  
  
### <a name="variant"></a>Variant  
 A**バリアント**value メンバーとデータ型のメンバーを含む構造化されたデータ型です。 A**バリアント**幅広い別バリアント、BSTR、ブール値、IDispatch または IUnknown ポインター、通貨、日付、およびなどを含むその他のデータ型を含めることができます。 COM では、メソッドを簡単に 1 つのデータ型の変換も提供します。  
  
 **_Variant_t**クラスがカプセル化し、管理、**バリアント**データ型。  
  
 ADO の API リファレンスは、メソッドまたはプロパティのオペランドは値を受け取り、通常は、値が渡された、 **_variant_t**します。  
  
 このルールは、明示的に true のときに、**パラメーター** ADO の API リファレンスのトピックの「よると、オペランドは、**バリアント**します。 1 つの例外は、ドキュメントに明示的に記載されている場合、オペランドをなど、標準的なデータ型が**長い**または**バイト**、または列挙体。 別の例外は、オペランドの実行時、**文字列**します。  
  
### <a name="bstr"></a>BSTR  
 A **BSTR** (**B**asic **STR**ing) 文字の文字列と文字列の長さを含む構造化されたデータ型です。 COM は、割り当て、操作、および解放するメソッドを提供する**BSTR**します。  
  
 **_Bstr_t**クラスがカプセル化し、管理、 **BSTR**データ型。  
  
 ADO の API リファレンスがメソッドまたはプロパティを表示する場合は、**文字列**値、つまり、値の形式で、 **_bstr_t**します。  
  
### <a name="casting-variantt-and-bstrt-classes"></a>キャスト _variant_t と _bstr_t クラス  
 多くの場合、コードでは明示的にする必要はありません、 **_variant_t**または **_bstr_t**に、操作の引数にします。 場合、 **_variant_t**または **_bstr_t**クラスの引数のデータ型と一致するコンス トラクターには、コンパイラは、適切な生成 **_variant_t**または **_bstr_t**します。  
  
 ただし、引数があいまいな場合は、引数のデータ型は、複数のコンス トラクターを一致する、適切なコンス トラクターを呼び出すための適切なデータ型の引数をキャストする必要があります。  
  
 宣言など、 **Recordset::Open**メソッドは。  
  
```cpp
    HRESULT Open (  
        const _variant_t & Source,  
        const _variant_t & ActiveConnection,  
        enum CursorTypeEnum CursorType,  
        enum LockTypeEnum LockType,  
        long Options );  
```
  
 `ActiveConnection`引数への参照には、 **_variant_t**、接続文字列または開いているへのポインターとしてコーディングすることがありますが**接続**オブジェクト。  
  
 正しい **_variant_t**など、文字列を渡す場合は、暗黙的に構築されます"`DSN=pubs;uid=MyUserName;pwd=MyPassword;`"、またはなどのポインター"`(IDispatch *) pConn`"。  
  
> [!NOTE]
>  Windows 認証をサポートするデータ ソース プロバイダーに接続するかどうかは、する必要がありますを指定する**Trusted_Connection = yes**または**Integrated Security = SSPI**ユーザー ID とパスワードの代わりに接続文字列の情報です。  
  
 または、明示的にコーディングすることがあります、 **_variant_t**などのポインターを格納している"`_variant_t((IDispatch *) pConn, true)`"。 キャスト`(IDispatch *)`、IUnknown インターフェイスへのポインターを受け取るもう 1 つのコンス トラクターを持つあいまいさを解決します。  
  
 めったにありません 実際には、ADO は IDispatch インターフェイスを記載されているが、重要です。 たびとして ADO オブジェクトへのポインターを渡す必要があります、**バリアント**、IDispatch インターフェイスへのポインターとしてそのポインターをキャストする必要があります。  
  
 最後の場合は、コンス トラクターの 2 つ目のブール型の引数は省略可能、既定値を明示的にコード`true`します。 この引数により、**バリアント**コンス トラクターを呼び出すその**AddRef**() メソッドは、ADO が自動的に呼び出すことを補正、 **_variant_t::Release**() メソッドADO メソッドまたはプロパティの呼び出しが完了したとき。  
  
### <a name="safearray"></a>SafeArray  
 A **SafeArray**は他のデータ型の配列を含む構造化されたデータ型です。 A **SafeArray**と呼びます*セーフ*のため、各配列の次元の境界に関する情報を格納し、それらの範囲内の配列要素へのアクセスを制限します。  
  
 ADO の API リファレンスは、メソッドまたはプロパティは、または配列を返しますメソッドになります。 または、またはプロパティはを返します、 **SafeArray**、ネイティブ c/c++ 配列ではありません。  
  
 2 番目のパラメーターなど、**接続**オブジェクト**OpenSchema**メソッドには、配列が必要です。**バリアント**値。 これら**バリアント**の要素としての値を渡す必要があります、 **SafeArray**、および**SafeArray**別の値として設定する必要があります**バリアント**. 他の**バリアント**の 2 番目の引数として渡される**OpenSchema**します。  
  
 例として、さらに、最初の引数、**検索**メソッドは、**バリアント**値が 1 次元**SafeArray**; 各オプションの最初と 2 番目の引数の**AddNew**は、1 次元**SafeArray**; と戻り値、 **GetRows**メソッドは、**バリアント**が値は、2 次元**SafeArray**します。  
  
## <a name="missing-and-default-parameters"></a>不足していると、既定のパラメーター  
 Visual Basic ではメソッドのパラメーターがありません。 たとえば、**レコード セット**オブジェクト**オープン**メソッドには 5 つのパラメーターが、中間のパラメーターをスキップして、後続のパラメーターをオフのままにすることができます。 既定の**BSTR**または**バリアント**は不足しているオペランドのデータ型によって置き換えられます。  
  
 C と C++ では、すべてのオペランドを指定する必要があります。 データ型は文字列で不足しているパラメーターを指定する場合、指定、 **_bstr_t** null 文字列を格納します。 データ型が不足しているパラメーターを指定するかどうか、**バリアント**、指定、 **_variant_t** DISP_E_PARAMNOTFOUND と VT_ERROR の型の値。 代わりに、相当するものを指定 **_variant_t**定数、 **vtMissing**、によって提供されますが、 **#import**ディレクティブ。  
  
 3 つのメソッドは例外の一般的な用途を**vtMissing**します。 これらは、 **Execute**のメソッド、**接続**と**コマンド**オブジェクト、および**NextRecordset**メソッド、の**Recordset**オブジェクト。 そのシグネチャを次に示します。  
  
```cpp
_RecordsetPtr <A HREF="mdmthcnnexecute.htm">Execute</A>( _bstr_t CommandText, VARIANT * RecordsAffected,   
        long Options );  // Connection  
_RecordsetPtr <A HREF="mdmthcmdexecute.htm">Execute</A>( VARIANT * RecordsAffected, VARIANT * Parameters,   
        long Options );  // Command  
_RecordsetPtr <A HREF="mdmthnextrec.htm">NextRecordset</A>( VARIANT * RecordsAffected );  // Recordset  
```
  
 パラメーター、 *RecordsAffected*と*パラメーター*へのポインターを**バリアント**します。 *パラメーター*のアドレスを指定する入力パラメーターには、**バリアント**1 つを格納しているパラメーター、または実行中のコマンドを変更するには、パラメーターの配列。 *RecordsAffected*のアドレスを指定する出力パラメーター、**バリアント**、メソッドによって影響を受ける行の数が返されます。  
  
 **コマンド**オブジェクト**Execute**メソッドを設定して、パラメーターが指定されていないことを示す*パラメーター*いずれかに`&vtMissing`(これを推奨) またはnull ポインター (つまり、 **NULL**またはゼロ (0))。 場合*パラメーター*設定を null ポインターでは、メソッドは内部的に相当**vtMissing**、操作が完了するとします。  
  
 すべてのメソッドに影響を受けたレコードの数を設定して返されないことを示す*RecordsAffected* null ポインター。 この場合、null ポインター パラメーターではありませんほど不足していることを表すメソッドが影響を受けたレコードの数を破棄する必要があります。  
  
 したがって、これら 3 つの方法など、コードを記述するは無効があります。  
  
```cpp
pConnection->Execute("commandText", NULL, adCmdText);   
pCommand->Execute(NULL, NULL, adCmdText);  
pRecordset->NextRecordset(NULL);  
```
  
## <a name="error-handling"></a>エラー処理  
 COM では、ほとんどの操作は、関数が正常に完了したかどうかを示す HRESULT のリターン コードを返します。 **#Import**ディレクティブは、各「生」のメソッドまたはプロパティをラッパー コードを生成し、返された HRESULT を確認します。 場合は、HRESULT が障害を示してラッパー コードは、引数として HRESULT のリターン コードで呼び出し元の _com_issue_errorex() によって COM エラーをスローします。 COM エラー オブジェクトをキャッチ、**お試しください**-**キャッチ**ブロック。 (効率性のために、キャッチへの参照を **_com_error**オブジェクトです)。  
  
 ただし、これらは、ADO エラー: ADO 操作の失敗による結果です。 基になるプロバイダーから返されるエラーの表示として**エラー**内のオブジェクト、**接続**オブジェクト**エラー**コレクション。  
  
 **#Import**ディレクティブはエラーのみのメソッドおよび ado で宣言されたプロパティの処理ルーチンを作成します。 ただし、このエラー処理機構を独自のエラー チェック マクロまたはインライン関数を記述することで活用を実行できます。 このトピックを参照して[Visual C 拡張](../../../ado/guide/appendixes/visual-c-extensions-for-ado.md)、またはコード例については、次のセクションでは。  
  
## <a name="visual-c-equivalents-of-visual-basic-conventions"></a>Visual Basic の規則の対応する visual C  
 ADO のドキュメントでは、Visual Basic の場合と同等の Visual C でコード化されたいくつかの規則の概要を次に示します。  
  
### <a name="declaring-an-ado-object"></a>ADO オブジェクトの宣言  
 Visual basic で ADO オブジェクト変数 (この場合は、**レコード セット**オブジェクト) が次のように宣言されています。  
  
```vb
Dim rst As ADODB.Recordset  
```
  
 句、"`ADODB.Recordset`"の ProgID は、**レコード セット**レジストリで定義されているオブジェクトします。 新しいインスタンスを**レコード**オブジェクトが次のように宣言されています。  
  
```vb
Dim rst As New ADODB.Recordset  
```
  
 \- または -  
  
```vb
Dim rst As ADODB.Recordset  
Set rst = New ADODB.Recordset  
```
  
 Visual C で、 **#import**ディレクティブには、すべての ADO オブジェクトのスマート ポインター型宣言が生成されます。 指す変数など、 **_Recordset**型のオブジェクトは、 **_RecordsetPtr**が次のように宣言されているとします。  
  
```cpp
_RecordsetPtr  rs;  
```
  
 新しいインスタンスを指す変数を **_Recordset**オブジェクトが次のように宣言されています。  
  
```cpp
_RecordsetPtr  rs("ADODB.Recordset");  
```
  
 \- または -  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance("ADODB.Recordset");  
```
  
 \- または -  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance(__uuidof(_Recordset));  
```
  
 後に、 **CreateInstance**メソッドが呼び出されると、変数を次のように使用できます。  
  
```cpp
rs->Open(...);  
```
  
 1 つのケースで、"`.`"の場合、変数がクラスのインスタンスを同じように、演算子を使用 (`rs.CreateInstance`) と別の場合、"`->`"変数がインターフェイスへのポインターであるかのように、演算子を使用 (`rs->Open`)。  
  
 2 つの方法で 1 つの変数を使用できる、"`->`"インターフェイスへのポインターと同様に動作するためのクラスのインスタンスを許可する演算子をオーバー ロードします。 インスタンス変数のプライベート クラス メンバーにはへのポインターが含まれています、 **_Recordset**インターフェイスは、"`->`"演算子を返しますそのポインターと返されるポインターのメンバーにアクセスする、 **_Recordset。** オブジェクト。  
  
### <a name="coding-a-missing-parameter---string"></a>不足しているパラメーターの文字列のコーディング  
 存在しないをコーディングする必要がある場合**文字列**オペランド、オペランドの省略だけで Visual basic でします。 Visual C では、オペランドを指定する必要があります。 コードを **_bstr_t**を持つ値として空の文字列。  
  
```cpp
_bstr_t strMissing(L"");  
```
  
### <a name="coding-a-missing-parameter---variant"></a>不足しているパラメーターの場合は、バリアントのコーディング  
 存在しないをコーディングする必要がある場合**バリアント**オペランド、オペランドの省略だけで Visual basic でします。 Visual C では、すべてのオペランドを指定する必要があります。 コードが存在しない**バリアント**パラメーター、 **_variant_t**特殊な値や DISP_E_PARAMNOTFOUND、型、VT_ERROR に設定します。 代わりに、指定**vtMissing**、これと同じ定義済みの定数によって提供される、 **#import**ディレクティブ。  
  
```cpp
_variant_t  vtMissingYours(DISP_E_PARAMNOTFOUND, VT_ERROR);   
```
  
 またはを使用して、  
  
```cpp
...vtMissing...;  
```
  
### <a name="declaring-a-variant"></a>バリアント型を宣言します。  
 Visual basic で、**バリアント**で宣言されて、 **Dim**ステートメントは、次のとおりです。  
  
```vb
Dim VariableName As Variant  
```
  
 ビジュアルでC++、型として変数を宣言 **_variant_t**します。 いくつかの概略図 **_variant_t**宣言を以下に示します。  
  
> [!NOTE]
>  これらの宣言は、独自のプログラムでコーディングする内容の大まかなアイデアだけを提供します。 詳細については、以下の例と Visual c ドキュメントを参照してください。  
  
```cpp
_variant_t  VariableName(value);  
_variant_t  VariableName((data type cast) value);  
_variant_t  VariableName(value, VT_DATATYPE);  
_variant_t  VariableName(interface * value, bool fAddRef = true);  
```
  
### <a name="using-arrays-of-variants"></a>Variant の配列を使用します。  
 Visual basic での配列**バリアント**でコーディングすることができます、 **Dim**ステートメント、またはを使用して、**配列**関数は、次のコード例で示した。  
  
```vb
Public Sub ArrayOfVariants  
Dim cn As ADODB.Connection  
Dim rs As ADODB.Recordset  
Dim fld As ADODB.Field  
  
    cn.Open "DSN=pubs"  
    rs = cn.OpenSchema(adSchemaColumns, _  
        Array(Empty, Empty, "authors", Empty))  
    For Each fld in rs.Fields  
        Debug.Print "Name = "; fld.Name  
    Next fld  
    rs.Close  
    cn.Close  
End Sub  
```
  
 次のビジュアルC++使用例を示します、 **SafeArray**と併用、 **_variant_t**します。  
  
#### <a name="notes"></a>メモ  
 次のノートは、コード例ではコメント部分に対応します。  
  
1.  もう一度、TESTHR() のインライン関数は、既存のエラー処理メカニズムを活用するために定義されます。  
  
2.  必要なだけ 1 次元配列で使用できるように**SafeArrayCreateVector**、一般的な用途ではなく**SAFEARRAYBOUND**宣言と**SafeArrayCreate**関数。 次にそのコードがどのようにを使用して**SafeArrayCreate**:  
  
    ```cpp
       SAFEARRAYBOUND   sabound[1];  
       sabound[0].lLbound = 0;  
       sabound[0].cElements = 4;  
       pSa = SafeArrayCreate(VT_VARIANT, 1, sabound);  
    ```
  
3.  列挙型の定数で識別されるスキーマ**adSchemaColumns**、4 つの制約の列に関連付けられました。TABLE_CATALOG、table_schema、TABLE_NAME、COLUMN_NAME します。 そのため、配列の**バリアント**4 つの要素を持つ値を作成します。 TABLE_NAME、3 番目の列に対応する制約値を指定します。  
  
     **Recordset**返されるサブセットを実行するは、制約列の複数の列で構成されます。 返された各行の制約列の値は、対応する制約の値と同じである必要があります。  
  
4.  慣れ親しんでいる**Safearray**可能性があるスタジオに驚き**SafeArrayDestroy**() は、終了する前に呼び出されません。 実際には、呼び出す**SafeArrayDestroy**() ここで、実行時と例外が発生します。 その理由は、デストラクターの`vtCriteria`が呼び出す**VariantClear**() ときに、 **_variant_t**が解放は、スコープ外になる、 **SafeArray**します。 呼び出す**SafeArrayDestroy**、手動でオフにせず、 **_variant_t**、無効なをオフにしようとするデストラクターを引き起こす**SafeArray**ポインター。  
  
     場合**SafeArrayDestroy**いたよう呼び出されると、コードになります。  
  
    ```cpp
          TESTHR(SafeArrayDestroy(pSa));  
       vtCriteria.vt = VT_EMPTY;  
          vtCriteria.parray = NULL;  
    ```
  
     ただし、使用できるようにするほうが、 **_variant_t**管理、 **SafeArray**します。  
  
```cpp
// Visual_CPP_ADO_Prog_1.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Note 1  
inline void TESTHR( HRESULT _hr ) {   
   if FAILED(_hr)   
      _com_issue_error(_hr);   
}  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _RecordsetPtr pRs("ADODB.Recordset");  
      _ConnectionPtr pCn("ADODB.Connection");  
      _variant_t vtTableName("authors"), vtCriteria;  
      long ix[1];  
      SAFEARRAY *pSa = NULL;  
  
      pCn->Provider = "sqloledb";  
      pCn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
      // Note 2, Note 3  
      pSa = SafeArrayCreateVector(VT_VARIANT, 1, 4);  
      if (!pSa)   
         _com_issue_error(E_OUTOFMEMORY);  
  
      // Specify TABLE_NAME in the third array element (index of 2).   
      ix[0] = 2;        
      TESTHR(SafeArrayPutElement(pSa, ix, &vtTableName));  
  
      // There is no Variant constructor for a SafeArray, so manually set the   
      // type (SafeArray of Variant) and value (pointer to a SafeArray).  
  
      vtCriteria.vt = VT_ARRAY | VT_VARIANT;  
      vtCriteria.parray = pSa;  
  
      pRs = pCn->OpenSchema(adSchemaColumns, vtCriteria, vtMissing);  
  
      long limit = pRs->GetFields()->Count;  
      for ( long x = 0 ; x < limit ; x++ )  
         printf( "%d: %s\n", x + 1, ((char*) pRs->GetFields()->Item[x]->Name) );  
      // Note 4  
      pRs->Close();  
      pCn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Error:\n");  
      printf("Code = %08lx\n", e.Error());  
      printf("Code meaning = %s\n", (char*) e.ErrorMessage());  
      printf("Source = %s\n", (char*) e.Source());  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   CoUninitialize();  
}  
```
  
### <a name="using-property-getputputref"></a>プロパティの Get と Put/PutRef を使用します。  
 Visual basic ではか取得、割り当てられている、または参照の割り当てによって、プロパティの名前は修飾されません。  
  
```vb
Public Sub GetPutPutRef  
Dim rs As New ADODB.Recordset  
Dim cn As New ADODB.Connection  
Dim sz as Integer  
cn.Open "Provider=sqloledb;Data Source=yourserver;" & _  
         "Initial Catalog=pubs;Integrated Security=SSPI;"  
rs.PageSize = 10  
sz = rs.PageSize  
rs.ActiveConnection = cn  
rs.Open "authors",,adOpenStatic  
' ...  
rs.Close  
cn.Close  
End Sub  
```
  
 この Visual C の例では、**取得**/**配置**/**PutRef**_プロパティ_します。  
  
#### <a name="notes"></a>メモ  
 次のノートは、コード例ではコメント部分に対応します。  
  
1.  この例は、不足している文字列引数の 2 つの形式を使用して: 明示的な定数、 **strMissing**、およびコンパイラが、一時パスワードが作成に使用する文字列 **_bstr_t** のスコープに存在します。**開いている**メソッド。  
  
2.  オペランドをキャストする必要はありません`rs->PutRefActiveConnection(cn)`に`(IDispatch *)`オペランドの型が既に`(IDispatch *)`します。  
  
```cpp
// Visual_CPP_ado_prog_2.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _bstr_t strMissing(L"");  
      long oldPgSz = 0, newPgSz = 5;  
  
      // Note 1  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", strMissing, "", adConnectUnspecified);  
  
      oldPgSz = rs->GetPageSize();  
      // -or-  
      // oldPgSz = rs->PageSize;  
  
      rs->PutPageSize(newPgSz);  
      // -or-  
      // rs->PageSize = newPgSz;  
  
      // Note 2  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockReadOnly, adCmdTable);  
      printf("Original pagesize = %d, new pagesize = %d\n", oldPgSz, rs->GetPageSize());  
      rs->Close();  
      cn->Close();  
  
   }  
   catch (_com_error &e) {  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="using-getitemx-and-itemx"></a>GetItem(x) および項目の [x] を使用します。  
 この Visual Basic の例は、の標準と代替構文を示します**項目**()。  
  
```vb
Public Sub GetItemItem  
Dim rs As New ADODB.Recordset  
Dim name as String  
rs = rs.Open "authors", "DSN=pubs;", adOpenDynamic, _  
         adLockBatchOptimistic, adTable  
name = rs(0)  
' -or-  
name = rs.Fields.Item(0)  
rs(0) = "Test"  
rs.UpdateBatch  
' Restore name  
rs(0) = name  
rs.UpdateBatch  
rs.Close  
End Sub  
```
  
 この Visual C の例では**項目**します。  
  
> [!NOTE]
>  次のメモは、コード例のセクションをコメントに対応します。コレクションにアクセスするときに**項目**、インデックス、 **2**にキャストする必要があります**長い**適切なコンス トラクターが呼び出されるようにします。  
  
```cpp
// Visual_CPP_ado_prog_3.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
void main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _variant_t vtFirstName;  
  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", "", "", adConnectUnspecified);  
  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockOptimistic, adCmdTable);  
      rs->MoveFirst();  
  
      // Note 1. Get a field.  
      vtFirstName = rs->Fields->GetItem((long)2)->GetValue();  
      // -or-  
      vtFirstName = rs->Fields->Item[(long)2]->Value;  
  
      printf( "First name = '%s'\n", (char*)( (_bstr_t)vtFirstName) );  
  
      rs->Fields->GetItem((long)2)->Value = L"TEST";  
      rs->Update(vtMissing, vtMissing);  
  
      // Restore name  
      rs->Fields->GetItem((long)2)->PutValue(vtFirstName);  
      // -or-  
      rs->Fields->GetItem((long)2)->Value = vtFirstName;  
      rs->Update(vtMissing, vtMissing);  
      rs->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="casting-ado-object-pointers-with-idispatch-"></a>ADO オブジェクトのポインターにキャスト (IDispatch *)  
 Visual C の例を次に示しますを使用して (IDispatch *) ADO オブジェクト ポインターのキャストにします。  
  
#### <a name="notes"></a>メモ  
 次のノートは、コード例ではコメント部分に対応します。  
  
1.  開いているを指定**接続**で明示的にコード化されたオブジェクト**バリアント**します。 キャスト (IDispatch \*) 適切なコンス トラクターが呼び出されるようにします。 また、2 つ目を明示的に設定 **_variant_t**パラメーターの既定値を**true**、オブジェクトの参照カウントされるため、適切なときに、 **Recordset::Open**操作を終了します。  
  
2.  式では、 `(_bstr_t)`、キャストではありませんが、 **_variant_t**抽出演算子を **_bstr_t**から文字列、**バリアント**によって返される**値**.  
  
 式では、 `(char*)`、キャストではありませんが、 **_bstr_t**でカプセル化された文字列へのポインターを抽出する演算子、 **_bstr_t**オブジェクト。  
  
 このセクションのコードでは、に使用できる動作の一部を示します **_variant_t**と **_bstr_t**演算子。  
  
```cpp
// Visual_CPP_ado_prog_4.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr pConn("ADODB.Connection");  
      _RecordsetPtr pRst("ADODB.Recordset");  
  
      pConn->Provider = "sqloledb";  
      pConn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
  
      // Note 1.  
      pRst->Open("authors", _variant_t((IDispatch *) pConn, true), adOpenStatic, adLockReadOnly, adCmdTable);  
      pRst->MoveLast();  
  
      // Note 2.  
      printf("Last name is '%s %s'\n",   
         (char*) ((_bstr_t) pRst->GetFields()->GetItem("au_fname")->GetValue()),  
         (char*) ((_bstr_t) pRst->Fields->Item["au_lname"]->Value));  
  
      pRst->Close();  
      pConn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }     
   ::CoUninitialize();  
}  
```
