#JsonPack

## Overview

JsonPack is a high-performance and extremely easy-to-use JSON serialization
library for C++ 11, it provide a absolute abstraction layer of this Data Interchange Format. From now on,
you only should take care about managing your C++ objects and JsonPack will make the rest.

## Features

* Easy-to-use, contains a very short and intuitive API. See Example section

* Very fast, zero string copy and fast number conversions.

* Support serialization/deserialization for c++ types:
  bool, char, int, unsigned int, long, unsigned long,
  long long,unsigned long long, float, double and std::string.
  
* Support serialization/deserialization for c++ standard containers:
  array, vector, deque, list, forward_list, set, multiset, unordered_set, unordered_multiset.

* Parsing error management

* JSON keys match with C++ identifiers name convention.

## Example

```cpp
#include <jsonpack.hpp>

struct  DataObject
{
    int mInt = 0;
    float mFloat = 0.0;
    std::string mCad = "";
    bool isObject = true;
    char caracter = 0;

    // The defined members, will be the JSON attributes set
    // Pairs <"key" : value>, are: <"member-name" : member-value >
    DEFINE_JSON_ATTRIBUTES(mFloat, mInt, mCad, isObject, caracter)
};

int main()
{

    // manage my object
    DataObject src, out;

    src.mFloat = 3.1415926535897932384626433832795;
    src.mInt = 362880;
    src.mCad = "This is a test";
    src.isObject = true;
    src.caracter = '$';

    //serialize object
    char* serialized = src.json_pack();
    printf("json: \n%s\n", serialized);

    //deserialize json
    try
    {
      out.json_unpack(serialized, strlen(serialized) );
      printf("\nobject: \nout.mFloat=%0.16f\nout.mInt=%d\nout.mCad=%s\nout.isObject=%d\nout.caracter=%c\n",
              out.mFloat, out.mInt, out.mCad.data(), out.isObject, out.caracter
             );
    }
    catch (jsonpack::jsonpack_error &e)
    {
        printf("error: %s\n", e.what());
    }


    free(serialized);
    getchar();

    return 0;
}
```

## Build

### You will need:

- cmake >= 2.8.0
- gcc >= 4.7 OR msvc >= 11 OR clang >= 2.9

### Using terminal

* Without example:

  ```bash
  $ cd jsonpack
  $ mkdir build
  $ cd build
  $ cmake .. -DCMAKE_BUILD_TYPE=Release
  $ make
  $ sudo make install
  ```

* With example:

  ```bash
  $ cd jsonpack
  $ mkdir build
  $ cd build
  $ cmake ..  -DJSONPACK_BUILD_EXAMPLES=ON -DCMAKE_BUILD_TYPE=Release
  $ make
  $ sudo make install
  ```


### GUI on Windows

1. Launch cmake GUI client

2. Set 'Where is the source code:' text box and 'Where to build the binaries:' text box.

3. Click 'Configure' button.

4. Choose your Visual Studio version.

5. Click 'Generate' button.

6. Open the created jsonpack.sln on Visual Studio.

7. Build all

## Contributing

1. Fork it!
2. Create your feature branch: git checkout -b my-new-feature
3. Commit your changes: git commit -am 'Add some feature'
4. Push to the branch: git push origin my-new-feature
5. Submit a pull request :D

## License
----------

Jsonpack is licensed under the Apache License Version 2.0. See
the [`LICENSE`](./LICENSE) file for details.
