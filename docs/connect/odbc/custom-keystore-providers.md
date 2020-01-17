---
title: カスタムキーストアプロバイダー |Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a6166d7d-ef34-4f87-bd1b-838d3ca59ae7
ms.author: v-chojas
author: MightyPen
ms.openlocfilehash: 0cf2946517be732094d01ff9889faf080a36e85b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006498"
---
# <a name="custom-keystore-providers"></a>カスタム キーストア プロバイダー
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>概要

SQL Server 2016 の列暗号化機能を使用するには、暗号化された列に格納されているデータにアクセスするために、サーバーに格納されている暗号化された列暗号化キー (ECEKs) がクライアントによって取得され、列暗号化キー (CEKs) に復号化される必要があります。 ECEKs は列マスターキー (CMKs) によって暗号化され、CMKS のセキュリティは列暗号化のセキュリティにとって重要です。 そのため、CMK は安全な場所に格納する必要があります。列暗号化キーストアプロバイダーの目的は、安全に格納されている CMKs に ODBC ドライバーがアクセスできるようにするためのインターフェイスを提供することです。 独自のセキュリティで保護されたストレージを持つユーザーには、カスタムキーストアプロバイダーのインターフェイスが用意されており、CMK の安全なストレージへのアクセスを実装するためのフレームワークを提供します。 ODBC ドライバーは、CEK の暗号化と復号化を実行するために使用できます。

各キーストアプロバイダーは、1つまたは複数の CMKs を含み、管理します。これは、プロバイダーによって定義された形式のキーパス (文字列) によって識別されます。 これは、暗号化アルゴリズムと共に、プロバイダーによって定義される文字列でもあり、CEK の暗号化と ECEK の復号化を実行するために使用できます。 アルゴリズムは、ECEK およびプロバイダーの名前と共に、データベースの暗号化メタデータに格納されます。詳細については、「[列マスターキーの作成](../../t-sql/statements/create-column-master-key-transact-sql.md)」および「[列暗号化キーの作成](../../t-sql/statements/create-column-encryption-key-transact-sql.md)」を参照してください。 このため、キー管理の2つの基本的な操作は次のとおりです。

```
CEK = DecryptViaCEKeystoreProvider(CEKeystoreProvider_name, Key_path, Key_algorithm, ECEK)

-and-

ECEK = EncryptViaCEKeystoreProvider(CEKeyStoreProvider_name, Key_path, Key_algorithm, CEK)
```

は、 `CEKeystoreProvider_name`特定の列暗号化キーストアプロバイダー (CEKeystoreProvider) を識別するために使用され、その他の引数は、(E) cek の暗号化/暗号化解除のために CEKeystoreProvider によって使用されます。 名前とキーパスは CMK メタデータによって提供されますが、アルゴリズムと ECEK 値は CEK メタデータによって提供されます。 既定の組み込みプロバイダーと共に、複数のキーストアプロバイダーが存在する場合があります。 CEK を必要とする操作を実行すると、ドライバーは CMK メタデータを使用して適切なキーストアプロバイダーを名前で検索し、復号化操作を実行します。これは次のように表現できます。

```
CEK = CEKeyStoreProvider_specific_decrypt(Key_path, Key_algorithm, ECEK)
```

ドライバーでは、CEKs を暗号化する必要はありませんが、CMK の作成やローテーションなどの操作を実装するためにキー管理ツールが必要になる場合があります。これには、逆の操作を実行する必要があります。

```
ECEK = CEKeyStoreProvider_specific_encrypt(Key_path, Key_algorithm, CEK)
```

### <a name="cekeystoreprovider-interface"></a>CEKeyStoreProvider インターフェイス

このドキュメントでは、CEKeyStoreProvider インターフェイスについて詳しく説明します。 このインターフェイスを実装するキーストアプロバイダーは、Microsoft ODBC Driver for SQL Server で使用できます。 CEKeyStoreProvider の実装者は、このガイドを使用して、ドライバーが使用できるカスタムキーストアプロバイダーを開発できます。

キーストアプロバイダーライブラリ ("プロバイダーライブラリ") はダイナミックリンクライブラリであり、ODBC ドライバーによって読み込むことができ、1つ以上のキーストアプロバイダーが含まれています。 シンボル`CEKeystoreProvider`は、プロバイダーライブラリによってエクスポートされる必要があります。また、ライブラリ内の各キー `CEKeystoreProvider`ストアプロバイダーに1つずつ、構造体へのポインターの null で終わる配列のアドレスにする必要があります。

構造`CEKeystoreProvider`体は、1つのキーストアプロバイダーのエントリポイントを定義します。

```
typedef struct CEKeystoreProvider {
    wchar_t *Name;
    int (*Init)(CEKEYSTORECONTEXT *ctx, errFunc *onError);
    int (*Read)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int *len);
    int (*Write)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len);
    int (*DecryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *ecek,
                        unsigned short ecekLen,
                        unsigned char **cekOut,
                        unsigned short *cekLen);
    int (*EncryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *cek,
                        unsigned short cekLen,
                        unsigned char **ecekOut,
                        unsigned short *ecekLen);
    void (*Free)();
} CEKEYSTOREPROVIDER;
```

|フィールド名|[説明]|
|:--|:--|
|`Name`|キーストアプロバイダーの名前。 これは、ドライバーによって以前に読み込まれた、またはこのライブラリにある他のキーストアプロバイダーと同じにすることはできません。 null 値で終わる、ワイド文字列 (*) です。|
|`Init`|初期化関数。 初期化関数が不要な場合、このフィールドは null になることがあります。|
|`Read`|プロバイダーの読み取り関数です。 必要でない場合は null を指定できます。|
|`Write`|プロバイダー書き込み関数です。 Read が null でない場合は必須です。 必要でない場合は null を指定できます。|
|`DecryptCEK`|ECEK 復号化関数。 この関数は、キーストアプロバイダーが存在する理由です。 null にすることはできません。|
|`EncryptCEK`|CEK 暗号化関数。 ドライバーはこの関数を呼び出しませんが、キー管理ツールによって ECEK の作成にプログラムでアクセスできるようにするために用意されています。 必要でない場合は null を指定できます。|
|`Free`|終了関数。 必要でない場合は null を指定できます。|

Free を除き、このインターフェイスの関数はすべて、 **ctx**と**onError**のパラメーターのペアを持ちます。 前者は、関数が呼び出されるコンテキストを識別しますが、後者はエラーの報告に使用されます。 詳細については、以下の「[コンテキスト](#context-association)と[エラー処理](#error-handling)」を参照してください。

```
int Init(CEKEYSTORECONTEXT *ctx, errFunc onError);
```
プロバイダー定義の初期化関数のプレースホルダー名。 ドライバーは、プロバイダーが読み込まれた後、初めて ECEK の暗号化解除または読み取り ()/書き込み () 要求を実行する必要があるときに、この関数を1回呼び出します。 この関数は、必要な初期化を実行するために使用します。 

|引数|[説明]|
|:--|:--|
|`ctx`|代入操作コンテキスト。|
|`onError`|代入エラー-レポート機能。|
|`Return Value`|成功を示す場合は0以外の値を返し、エラーを示す場合は0を返します。|

```
int Read(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int *len);
```

プロバイダーが定義した通信関数のプレースホルダー名。 ドライバーは、アプリケーションが SQL_COPT_SS_CEKEYSTOREDATA 接続属性を使用して (以前に書き込まれた) プロバイダーからデータを読み取るように要求するときに、この関数を呼び出します。これにより、アプリケーションはプロバイダーから任意のデータを読み取ることができます。 詳細については、「[キーストアプロバイダーとの通信](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers)」を参照してください。

|引数|[説明]|
|:--|:--|
|`ctx`|代入操作コンテキスト。|
|`onError`|代入エラー-レポート機能。|
|`data`|Outputアプリケーションによって読み込まれるデータがプロバイダーによって書き込まれるバッファーへのポインター。 これは、CEKEYSTOREDATA 構造体のデータフィールドに対応します。|
|`len`|InOut長さの値へのポインター。入力時には、これはデータバッファーの最大長であり、プロバイダーは書き込みを * len バイト以上にする必要があります。 プロバイダーは、返されるときに、実際に書き込まれたバイト数を使用して * len を更新する必要があります。|
|`Return Value`|成功を示す場合は0以外の値を返し、エラーを示す場合は0を返します。|

```
int Write(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int len);
```
プロバイダーが定義した通信関数のプレースホルダー名。 アプリケーションが SQL_COPT_SS_CEKEYSTOREDATA 接続属性を使用してプロバイダーにデータを書き込むように要求すると、ドライバーはこの関数を呼び出します。これにより、アプリケーションは任意のデータをプロバイダーに書き込むことができます。 詳細については、「[キーストアプロバイダーとの通信](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers)」を参照してください。

|引数|[説明]|
|:--|:--|
|`ctx`|代入操作コンテキスト。|
|`onError`|代入エラー-レポート機能。|
|`data`|代入読み取るプロバイダーのデータを格納しているバッファーへのポインター。 これは、CEKEYSTOREDATA 構造体のデータフィールドに対応します。 プロバイダーは、このバッファーから len バイトを超える値を読み取ることはできません。|
|`len`|代入データで使用可能なバイト数。 これは、CEKEYSTOREDATA 構造体の dataSize フィールドに相当します。|
|`Return Value`|成功を示す場合は0以外の値を返し、エラーを示す場合は0を返します。|

```
int (*DecryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen);
```
プロバイダー定義の ECEK 復号化関数のプレースホルダー名。 ドライバーは、このプロバイダーに関連付けられている CMK によって暗号化された ECEK を CEK に復号化するために、この関数を呼び出します。

|引数|[説明]|
|:--|:--|
|`ctx`|代入操作コンテキスト。|
|`onError`|代入エラー-レポート機能。|
|`keyPath`|代入指定した ECEK によって参照される CMK の[KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) metadata 属性の値。 null 値で終わるワイド文字列 (*) です。 これは、このプロバイダーによって処理される CMK を識別するためのものです。|
|`alg`|代入指定した ECEK の[アルゴリズム](../../t-sql/statements/create-column-encryption-key-transact-sql.md)メタデータ属性の値。 null 値で終わるワイド文字列 (*) です。 これは、指定された ECEK の暗号化に使用される暗号化アルゴリズムを識別するためのものです。|
|`ecek`|代入暗号化を解除する ECEK へのポインター。|
|`ecekLen`|代入ECEK の長さ。|
|`cekOut`|Outputプロバイダーは、復号化された ECEK にメモリを割り当て、cekOut が指すポインターにそのアドレスを書き込む必要があります。 [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) または Free (Linux/Mac) 関数を使用して、このメモリブロックを解放できる必要があります。 エラーが原因でメモリが割り当てられなかった場合、プロバイダーは * cekOut を null ポインターに設定します。|
|`cekLen`|Outputプロバイダーは、cekLen が指すアドレスに、* * Ceklen に書き込まれた復号化された ECEK の長さを書き込む必要があります。|
|`Return Value`|成功を示す場合は0以外の値を返し、エラーを示す場合は0を返します。|

```
int (*EncryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *cek,unsigned short cekLen, unsigned char **ecekOut, unsigned short *ecekLen);
```
プロバイダー定義の CEK 暗号化関数のプレースホルダー名。 ドライバーは、この関数を呼び出したり、ODBC インターフェイスを介して機能を公開したりすることはありませんが、キー管理ツールによって ECEK の作成にプログラムでアクセスできるようにするために用意されています。

|引数|[説明]|
|:--|:--|
|`ctx`|代入操作コンテキスト。|
|`onError`|代入エラー-レポート機能。|
|`keyPath`|代入指定した ECEK によって参照される CMK の[KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) metadata 属性の値。 null 値で終わるワイド文字列 (*) です。 これは、このプロバイダーによって処理される CMK を識別するためのものです。|
|`alg`|代入指定した ECEK の[アルゴリズム](../../t-sql/statements/create-column-encryption-key-transact-sql.md)メタデータ属性の値。 null 値で終わるワイド文字列 (*) です。 これは、指定された ECEK の暗号化に使用される暗号化アルゴリズムを識別するためのものです。|
|`cek`|代入暗号化する CEK へのポインター。|
|`cekLen`|代入CEK の長さ。|
|`ecekOut`|Outputプロバイダーは、暗号化された CEK にメモリを割り当て、ecekOut が指すポインターにそのアドレスを書き込む必要があります。 [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) または Free (Linux/Mac) 関数を使用して、このメモリブロックを解放できる必要があります。 エラーが原因でメモリが割り当てられなかった場合、プロバイダーは * ecekOut を null ポインターに設定する必要があります。|
|`ecekLen`|Outputプロバイダーは、* * ecekOut に書き込まれた暗号化された CEK の長さを ecekLen が指すアドレスに書き込む必要があります。|
|`Return Value`|成功を示す場合は0以外の値を返し、エラーを示す場合は0を返します。|

```
void (*Free)();
```
プロバイダー定義の終了関数のプレースホルダー名。 ドライバーは、プロセスの通常の終了時にこの関数を呼び出すことができます。

> [!NOTE]
> *ワイド文字列は、SQL Server に格納されるため、2バイト文字 (UTF-16) です。*


### <a name="error-handling"></a>エラー処理

プロバイダーの処理中にエラーが発生する可能性があるため、ブール値の成功または失敗よりも具体的な詳細情報でドライバーにエラーを報告できるようにするためのメカニズムが用意されています。 関数の多くには、 **ctx**と**onError**という2つのパラメーターがあります。これは、成功/失敗の戻り値に加えて、この目的で一緒に使用されます。

**Ctx**パラメーターは、プロバイダー操作が発生するコンテキストを識別します。

**OnError**パラメーターは、次のプロトタイプを使用して、エラー報告関数を指します。

`typedef void errFunc(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...);`

|引数|[説明]|
|:--|:--|
|`ctx`|代入エラーを報告するコンテキスト。|
|`msg`|代入報告するエラーメッセージ。 null 値で終わるワイド文字列です。 パラメーター化された情報を使用できるようにするために、この文字列には、 [FormatMessage](/windows/desktop/api/winbase/nf-winbase-formatmessage)関数によって受け入れられるフォームの挿入書式指定シーケンスが含まれる場合があります。 拡張機能は、次に示すように、このパラメーターで指定できます。|
|[...]|代入必要に応じて、メッセージの書式指定子に合わせて追加の可変個引数パラメーターを指定します。|

エラーが発生したことを報告するために、プロバイダーは onError を呼び出します。これは、ドライバーによってプロバイダー関数に渡されたコンテキストパラメーターと、書式設定するオプションの追加パラメーターを含むエラーメッセージを提供します。 プロバイダーは、この関数を複数回呼び出して、1つのプロバイダー関数呼び出し内で複数のエラーメッセージを連続してポストする場合があります。 例:

```
    if (!doSomething(...))
    {
        onError(ctx, L"An error occurred in doSomething.");
        onError(ctx, L"Additional error message with more details.");
        return 0;
    }
```


`msg`パラメーターは通常、ワイド文字列ですが、追加の拡張機能を使用できます。

IDS_MSG マクロで特別な定義済みの値の1つを使用すると、既に存在していて、かつドライバーのローカル形式の一般的なエラーメッセージが使用される場合があります。 たとえば、プロバイダーがメモリの割り当てに失敗した場合`IDS_S1_001` 、"メモリ割り当てエラー" というメッセージが表示されます。

`onError(ctx, IDS_MSG(IDS_S1_001));`

ドライバーによってエラーが認識されされるようにするには、プロバイダー関数がエラーを返す必要があります。 これが odbc 操作のコンテキストで実行されると、標準の odbc 診断機構 (`SQLError`、 `SQLGetDiagRec`、および`SQLGetDiagField`) を使用して、接続またはステートメントハンドルでポストされたエラーにアクセスできるようになります。


### <a name="context-association"></a>コンテキストの関連付け

構造`CEKEYSTORECONTEXT`体は、エラーコールバックのコンテキストを提供するだけでなく、プロバイダー操作が実行される ODBC コンテキストを特定するためにも使用できます。 これにより、プロバイダーは、各コンテキストにデータを関連付けることができます。たとえば、接続ごとの構成を実装できます。 このため、構造体には、環境、接続、およびステートメントのコンテキストに対応する3つの不透明なポインターが含まれています。

```
typedef struct CEKeystoreContext
{
void *envCtx;
void *dbcCtx;
void *stmtCtx;
} CEKEYSTORECONTEXT;
```

|フィールド|[説明]|
|:--|:--|
|`envCtx`|環境コンテキスト。|
|`dbcCtx`|接続コンテキスト。|
|`stmtCtx`|ステートメントコンテキスト。|

これらの各コンテキストは不透明な値であり、対応する ODBC ハンドルと同じではなく、ハンドルの一意の識別子として使用できます。ハンドル*X*がコンテキスト値*Y*に関連付けられている場合、他の環境、接続、または*X*と同時に存在するステートメントハンドルは、コンテキスト値が*Y*になり、その他のコンテキスト値はハンドル*X*に関連付けられません。実行されているプロバイダーの操作に特定のハンドルコンテキストが存在しない場合 (例: SQLSetConnectAttr を呼び出してプロバイダーを読み込んで構成し、ステートメントハンドルがない場合) は、構造体の対応するコンテキスト値が null になります。


## <a name="example"></a>例

### <a name="keystore-provider"></a>キーストアプロバイダー

次のコードは、最小キーストアプロバイダーの実装の例です。

```
/* Custom Keystore Provider Example

Windows:   compile with cl MyKSP.c /LD /MD /link /out:MyKSP.dll
Linux/Mac: compile with gcc -fshort-wchar -fPIC -o MyKSP.so -shared MyKSP.c

 */

#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#endif

#include <stdlib.h>
#include <sqltypes.h>
#include "msodbcsql.h"
#include <sql.h>
#include <sqlext.h>

int __stdcall KeystoreInit(CEKEYSTORECONTEXT *ctx, errFunc *onError) {
    printf("KSP Init() function called\n");
    return 1;
}

static unsigned char *g_encryptKey;
static unsigned int g_encryptKeyLen;

int __stdcall KeystoreWrite(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len) {
    printf("KSP Write() function called (%d bytes)\n", len);
    if (len) {
        if (g_encryptKey)
            free(g_encryptKey);
        g_encryptKey = malloc(len);
        if (!g_encryptKey) {
            onError(ctx, L"Memory Allocation Error");
            return 0;
        }
        memcpy(g_encryptKey, data, len);
        g_encryptKeyLen = len;
    }
    return 1;
}

// Very simple "encryption" scheme - rotating XOR with the key
int __stdcall KeystoreDecrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg,
    unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen) {
    unsigned int i;
    printf("KSP Decrypt() function called (keypath=%S alg=%S ecekLen=%u)\n", keyPath, alg, ecekLen);
    if (wcscmp(keyPath, L"TheOneAndOnlyKey")) {
        onError(ctx, L"Invalid key path");
        return 0;
    }
    if (wcscmp(alg, L"none")) {
        onError(ctx, L"Invalid algorithm");
        return 0;
    }
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
#ifndef _WIN32
    *cekOut = malloc(ecekLen);
#else
    *cekOut = LocalAlloc(LMEM_FIXED, ecekLen);
#endif
    if (!*cekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *cekLen = ecekLen;
    for (i = 0; i < ecekLen; i++)
        (*cekOut)[i] = ecek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

// Note that in the provider interface, this function would be referenced via the CEKEYSTOREPROVIDER
// structure. However, that does not preclude keystore providers from exporting their own functions,
// as illustrated by this example where the encryption is performed via a separate function (with a
// different prototype than the one in the KSP interface.)
#ifdef _WIN32
__declspec(dllexport)
#endif
int KeystoreEncrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError,
    unsigned char *cek, unsigned short cekLen,
    unsigned char **ecekOut, unsigned short *ecekLen) {
    unsigned int i;
    printf("KSP Encrypt() function called (cekLen=%u)\n", cekLen);
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
    *ecekOut = malloc(cekLen);
    if (!*ecekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *ecekLen = cekLen;
    for (i = 0; i < cekLen; i++)
        (*ecekOut)[i] = cek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

CEKEYSTOREPROVIDER MyCustomKSPName_desc = {
    L"MyCustomKSPName",
    KeystoreInit,
    0,
    KeystoreWrite,
    KeystoreDecrypt,
    0
};

#ifdef _WIN32
__declspec(dllexport)
#endif
CEKEYSTOREPROVIDER *CEKeystoreProvider[] = {
    &MyCustomKSPName_desc,
    0
};
```

### <a name="odbc-application"></a>ODBC アプリケーション

次のコードは、上記のキーストアプロバイダーを使用するデモアプリケーションです。 このファイルを実行するときは、プロバイダーライブラリがアプリケーションバイナリと同じディレクトリにあり、接続文字列で`ColumnEncryption=Enabled`設定が指定されていることを確認します (または、を含む DSN を指定します)。

```
/*
 Example application for demonstration of custom keystore provider usage

Windows:   compile with cl /MD kspapp.c /link odbc32.lib
Linux/Mac: compile with gcc -o kspapp -fshort-wchar kspapp.c -lodbc -ldl
 
 usage: kspapp connstr

 */

#define KSPNAME L"MyCustomKSPName"
#define PROV_ENCRYPT_KEY "JHKCWYT06N3RG98J0MBLG4E3"

#include <stdio.h>
#include <stdlib.h>
#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#include <dlfcn.h>
#endif
#include <sql.h>
#include <sqlext.h>
#include "msodbcsql.h"

/* Convenience functions */

int checkRC(SQLRETURN rc, char *msg, int ret, SQLHANDLE h, SQLSMALLINT ht) {
    if (rc == SQL_ERROR) {
        fprintf(stderr, "Error occurred upon %s\n", msg);
        if (h) {
            SQLSMALLINT i = 0;
            SQLSMALLINT outlen = 0;
            char errmsg[1024];
            while ((rc = SQLGetDiagField(
                ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
                || rc == SQL_SUCCESS_WITH_INFO) {
                fprintf(stderr, "Err#%d: %s\n", i, errmsg);
            }
        }
        if (ret)
            exit(ret);
        return 0;
    }
    else if (rc == SQL_SUCCESS_WITH_INFO && h) {
        SQLSMALLINT i = 0;
        SQLSMALLINT outlen = 0;
        char errmsg[1024];
        printf("Success with info for %s:\n", msg);
        while ((rc = SQLGetDiagField(
            ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
            || rc == SQL_SUCCESS_WITH_INFO) {
            fprintf(stderr, "Msg#%d: %s\n", i, errmsg);
        }
    }
    return 1;
}

void postKspError(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...) {
    if (msg > (wchar_t*)65535)
        wprintf(L"Provider emitted message: %s\n", msg);
    else
        wprintf(L"Provider emitted message ID %d\n", msg);
}

int main(int argc, char **argv) {
    char sqlbuf[1024];
    SQLHENV env;
    SQLHDBC dbc;
    SQLHSTMT stmt;
    SQLRETURN rc;
    unsigned char CEK[32];
    unsigned char *ECEK;
    unsigned short ECEKlen;
#ifdef _WIN32
    HMODULE hProvLib;
#else
    void *hProvLib;
#endif
    CEKEYSTORECONTEXT ctx = {0};
    CEKEYSTOREPROVIDER **ppKsp, *pKsp;
    int(__stdcall *pEncryptCEK)(CEKEYSTORECONTEXT *, errFunc *, unsigned char *, unsigned short, unsigned char **, unsigned short *);
    int i;
    if (argc < 2) {
        fprintf(stderr, "usage: kspapp connstr\n");
        return 1;
    }

    /* Load the provider library */
#ifdef _WIN32
    if (!(hProvLib = LoadLibrary("MyKSP.dll"))) {
#else
    if (!(hProvLib = dlopen("./MyKSP.so", RTLD_NOW))) {
#endif
        fprintf(stderr, "Error loading KSP library\n");
        return 2;
    }
#ifdef _WIN32
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)GetProcAddress(hProvLib, "CEKeystoreProvider"))) {
#else
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)dlsym(hProvLib, "CEKeystoreProvider"))) {
#endif
        fprintf(stderr, "The export CEKeystoreProvider was not found in the KSP library\n");
        return 3;
    }
    while (pKsp = *ppKsp++) {
        if (!memcmp(KSPNAME, pKsp->Name, sizeof(KSPNAME)))
            goto FoundProv;
    }
    fprintf(stderr, "Could not find provider in the library\n");
    return 4;
FoundProv:
    if (pKsp->Init && !pKsp->Init(&ctx, postKspError)) {
        fprintf(stderr, "Could not initialize provider\n");
        return 5;
    }
#ifdef _WIN32
    if (!(pEncryptCEK = (LPVOID)GetProcAddress(hProvLib, "KeystoreEncrypt"))) {
#else
    if (!(pEncryptCEK = dlsym(hProvLib, "KeystoreEncrypt"))) {
#endif
        fprintf(stderr, "The export KeystoreEncrypt was not found in the KSP library\n");
        return 6;
    }
    if (!pKsp->Write) {
        fprintf(stderr, "Provider does not support configuration\n");
        return 7;
    }

    /* Configure the provider with the key */
    if (!pKsp->Write(&ctx, postKspError, PROV_ENCRYPT_KEY, strlen(PROV_ENCRYPT_KEY))) {
        fprintf(stderr, "Error writing to KSP\n");
        return 8;
    }

    /* Generate a CEK and encrypt it with the provider */
    srand(time(0) ^ getpid());
    for (i = 0; i < sizeof(CEK); i++)
        CEK[i] = rand();

    if (!pEncryptCEK(&ctx, postKspError, CEK, sizeof(CEK), &ECEK, &ECEKlen)) {
        fprintf(stderr, "Error encrypting CEK\n");
        return 9;
    }

    /* Connect to Server */
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &env);
    checkRC(rc, "allocating environment handle", 2, 0, 0);
    rc = SQLSetEnvAttr(env, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0);
    checkRC(rc, "setting ODBC version to 3.0", 3, env, SQL_HANDLE_ENV);
    rc = SQLAllocHandle(SQL_HANDLE_DBC, env, &dbc);
    checkRC(rc, "allocating connection handle", 4, env, SQL_HANDLE_ENV);
    rc = SQLDriverConnect(dbc, 0, argv[1], strlen(argv[1]), NULL, 0, NULL, SQL_DRIVER_NOPROMPT);
    checkRC(rc, "connecting to data source", 5, dbc, SQL_HANDLE_DBC);
    rc = SQLAllocHandle(SQL_HANDLE_STMT, dbc, &stmt);
    checkRC(rc, "allocating statement handle", 6, dbc, SQL_HANDLE_DBC);

    /* Create a CMK definition on the server */
    {
        static char cmkSql[] = "CREATE COLUMN MASTER KEY CustomCMK WITH ("
            "KEY_STORE_PROVIDER_NAME = 'MyCustomKSPName',"
            "KEY_PATH = 'TheOneAndOnlyKey')";
        printf("Create CMK: %s\n", cmkSql);
        SQLExecDirect(stmt, cmkSql, SQL_NTS);
    }

    /* Create a CEK definition on the server */
    {
        const char cekSqlBefore[] = "CREATE COLUMN ENCRYPTION KEY CustomCEK WITH VALUES ("
            "COLUMN_MASTER_KEY = CustomCMK,"
            "ALGORITHM = 'none',"
            "ENCRYPTED_VALUE = 0x";
        char *cekSql = malloc(sizeof(cekSqlBefore) + 2 * ECEKlen + 2); /* 1 for ')', 1 for null terminator */
        strcpy(cekSql, cekSqlBefore);
        for (i = 0; i < ECEKlen; i++)
            sprintf(cekSql + sizeof(cekSqlBefore) - 1 + 2 * i, "%02x", ECEK[i]);
        strcat(cekSql, ")");
        printf("Create CEK: %s\n", cekSql);
        SQLExecDirect(stmt, cekSql, SQL_NTS);
        free(cekSql);
#ifdef _WIN32
        LocalFree(ECEK);
#else
        free(ECEK);
#endif
    }

#ifdef _WIN32
    FreeLibrary(hProvLib);
#else
    dlclose(hProvLib);
#endif

    /* Create a table with encrypted columns */
    {
        static char *tableSql = "CREATE TABLE CustomKSPTestTable ("
            "c1 int,"
            "c2 varchar(255) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = CustomCEK, ENCRYPTION_TYPE = DETERMINISTIC, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'))";
        printf("Create table: %s\n", tableSql);
        SQLExecDirect(stmt, tableSql, SQL_NTS);
    }

    /* Load provider into the ODBC Driver and configure it */
    {
        unsigned char ksd[sizeof(CEKEYSTOREDATA) + sizeof(PROV_ENCRYPT_KEY) - 1];
        CEKEYSTOREDATA *pKsd = (CEKEYSTOREDATA*)ksd;
        pKsd->name = L"MyCustomKSPName";
        pKsd->dataSize = sizeof(PROV_ENCRYPT_KEY) - 1;
        memcpy(pKsd->data, PROV_ENCRYPT_KEY, sizeof(PROV_ENCRYPT_KEY) - 1);
#ifdef _WIN32
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "MyKSP.dll", SQL_NTS);
#else
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "./MyKSP.so", SQL_NTS);
#endif
        checkRC(rc, "Loading KSP into ODBC Driver", 7, dbc, SQL_HANDLE_DBC);
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREDATA, (SQLPOINTER)pKsd, SQL_IS_POINTER);
        checkRC(rc, "Configuring the KSP", 7, dbc, SQL_HANDLE_DBC);
    }

    /* Insert some data */
    {
        int c1;
        char c2[256];
        rc = SQLBindParameter(stmt, 1, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 0, 0, &c1, 0, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        rc = SQLBindParameter(stmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_VARCHAR, 255, 0, c2, 255, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        for (i = 0; i < 10; i++) {
            c1 = i * 10 + i + 1;
            sprintf(c2, "Sample data %d for column 2", i);
            rc = SQLExecDirect(stmt, "INSERT INTO CustomKSPTestTable (c1, c2) values (?, ?)", SQL_NTS);
            checkRC(rc, "Inserting rows query", 10, stmt, SQL_HANDLE_STMT);
        }
        printf("(Encrypted) data has been inserted into the [CustomKSPTestTable]. You may inspect the data now.\n"
            "Press Enter to continue...\n");
        getchar();
    }

    /* Retrieve the data */
    {
        int c1;
        char c2[256];
        rc = SQLBindCol(stmt, 1, SQL_C_LONG, &c1, 0, 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLBindCol(stmt, 2, SQL_C_CHAR, c2, sizeof(c2), 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLExecDirect(stmt, "SELECT c1, c2 FROM CustomKSPTestTable", SQL_NTS);
        checkRC(rc, "Retrieving rows query", 12, stmt, SQL_HANDLE_STMT);
        while (SQL_SUCCESS == (rc = SQLFetch(stmt)))
            printf("Retrieved data: c1=%d c2=%s\n", c1, c2);
        SQLFreeStmt(stmt, SQL_CLOSE);
        printf("Press Enter to clean up and exit...\n");
        getchar();
    }

    /* Clean up */
    {
        SQLExecDirect(stmt, "DROP TABLE CustomKSPTestTable", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN ENCRYPTION KEY CustomCEK", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN MASTER KEY CustomCMK", SQL_NTS);
        printf("Removed table, CEK, and CMK\n");
    }
    SQLDisconnect(dbc);
    SQLFreeHandle(SQL_HANDLE_DBC, dbc);
    SQLFreeHandle(SQL_HANDLE_ENV, env);
    return 0;
}

```

## <a name="see-also"></a>参照

[ODBC ドライバーで Always Encrypted を使用する](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
