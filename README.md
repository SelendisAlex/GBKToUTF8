# GBKToUTF8
[GitHub](https://github.com/SelendisAlex/GBKToUTF8)

## Description

GBK encode/decode to UTF8 functions for SA-MP Pawn scripting.
* <b>It's especially suitable for use with [requests](https://github.com/Southclaws/pawn-requests) to send data to websites.</b>

## Installation

Simply install to your project:

```bash
sampctl package install SelendisAlex/GBKToUTF8
```

Include in your code and begin using the library:

```pawn
#include <GBKToUTF8>
```

## Functions

* `GbkToUtf8` - Encode a GBK/GB2312 string to UTF-8.

* `Utf8ToGbk` - Decode a UTF-8 string to GBK/GB2312.

## Examples

### `GbkToUtf8`

```cpp
#include <requests>

public OnGameModeInit()
{
    new utf8Text[128];
    GbkToUtf8(utf8Text, "GB2312 String: 这是一些字符");

    new RequestsClient:client = RequestsClient("https://www.foo.com");
    new Request:id = RequestJSON(
        client,
        "",            
        HTTP_METHOD_POST, 
        "OnPostJson",
        JsonObject(
            "content", JsonString(utf8Text)
        ),
        RequestHeaders("Content-Type", "application/json")
    );
    return 1;
}

// Can send UTF-8 strings to any website.
```

### `Utf8ToGbk`

```cpp
public OnPostJson(Request:id, E_HTTP_STATUS:status, Node:node) 
{
    new content[128];
    new ret = JsonGetString(node, "content", content);
    
    if(ret) {
        printf("[Json] failed to get content error: %d", ret);
    }

    new gbkText[128];
    Utf8ToGbk(gbkText, content);

    printf(gbkText);
    return 1;
}

// Decode the return string to GBK/GB2312.
```

## Dependencies
- [strlib](https://github.com/oscar-broman/strlib)

## Notes
> For Chinese users / 给中文用户:
+ This library is encoded in UTF-8. If you want to see the Chinese comments in the library, please convert the library to GBK encoding.
+ 此文件的编码为UTF-8，如果你想看到文件中的中文注释的话，请将文件转换为GBK编码

## Thanks
> [oscar-broman](https://github.com/oscar-broman)
+ The base code of this library is from oscar-broman's [strlib](https://github.com/oscar-broman/strlib).
> [Southclaws](https://github.com/Southclaws)
+ If it weren't for Southclaws' [requests](https://github.com/Southclaws/pawn-requests), I probably wouldn't have developed this library.
> [siwode](https://github.com/siwode1)
+ Provided inspiration for the library and thoroughly tested it.