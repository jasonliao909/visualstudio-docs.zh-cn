---
description: 根据要使用的最大字节数检索文档校验和和算法标识符。
title: IDebugDocumentChecksum2：：GetChecksumAndAlgorithmId |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentChecksum2::GetChecksumAndAlgorithmI
- GetChecksumAndAlgorithmI
ms.assetid: 25efef99-0ef3-4332-a752-607605fc6e67
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e2aec1d8303f4b3ab553cf70caf1aac84c3be1d6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122079254"
---
# <a name="idebugdocumentchecksum2getchecksumandalgorithmid"></a>IDebugDocumentChecksum2::GetChecksumAndAlgorithmId
根据要使用的最大字节数检索文档校验和和算法标识符。

## <a name="syntax"></a>语法

```cpp
HRESULT GetChecksumAndAlgorithmId(
    GUID  *pRetVal,
    ULONG cMaxBytes,
    BYTE  *pChecksum,
    ULONG *pcNumBytes
);
```

```csharp
public int GetChecksumAndAlgorithmId(
    out Guid pRetVal,
    uint     cMaxBytes,
    out byte pChecksum,
    out uint pcNumBytes
);
```

## <a name="parameters"></a>参数
`pRetVal`\
[out]校验和算法的唯一标识符。

`cMaxBytes`\
[in]要用于校验和的最大字节数。

`pChecksum`\
[out]校验和的值。

`pcNumBytes`\
[out]校验和使用的实际字节数。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="example"></a>示例
下面的示例使用此方法获取文档的校验和和算法。

```cpp
HRESULT CDebugCodeContext::GetDocumentChecksumAndAlgorithmId(GUID *pguidAlgorithm, BYTE **ppChecksum, ULONG *pcNumBytes)
{
    HRESULT hRes = E_FAIL;

    *ppChecksum = NULL;
    *pcNumBytes = 0;

    CComPtr<IDebugDocumentContext2> pDocContext;

    hRes = this->GetDocumentContext(&pDocContext);

    if ( HREVAL(S_OK, hRes) )
    {
        CComQIPtr<IDebugDocumentChecksum2> pDocChecksum(pDocContext);

        if ( pDocChecksum != NULL )
        {
            // Figure out the size of the checksum buffer required
            ULONG cNumBytes = 0;

            hRes = pDocChecksum->GetChecksumAndAlgorithmId(pguidAlgorithm, 0, NULL, &cNumBytes);

            if ( S_OK == hRes )
            {
                // check to see if we got back valid values
                if ( cNumBytes && GUID_NULL != (*pguidAlgorithm) )
                {
                    // Alloc space for the checksum data
                    BYTE *pChecksum = (BYTE*) CoTaskMemAlloc(cNumBytes);

                    if ( pChecksum )
                    {
                        // Get the buffer containing the checksum info
                        hRes = pDocChecksum->GetChecksumAndAlgorithmId(pguidAlgorithm, cNumBytes, pChecksum, &cNumBytes);

                        if ( HREVAL(S_OK, hRes) )
                        {
                            *ppChecksum = pChecksum;
                            *pcNumBytes = cNumBytes;
                        }
                        else
                        {
                            CoTaskMemFree(pChecksum);
                        }
                    }
                    else
                        hRes = E_OUTOFMEMORY;
                }
                else
                    hRes = S_FALSE; // lang doesn't support checksums
            }
            else
                hRes = S_FALSE; // failed to work out checksum info
        }
        else
            hRes = S_FALSE; // SH doesn't support checksums
    }

    return ( hRes );
}
```

## <a name="see-also"></a>请参阅
- [IDebugDocumentChecksum2](../../../extensibility/debugger/reference/idebugdocumentchecksum2.md)
