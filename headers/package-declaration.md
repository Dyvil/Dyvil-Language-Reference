# Package Declaration

The Package Declaration ensures that the location of a source file in the file tree is correct. For example, the below Dyvil file has to be located in the directory tree as shown.

`Test.dyv`:
```java
package com.mycompany.test

class Test
```

**Directory Tree**:

```
- src
  - com
    - mycompany
      - test
        - Test.dyv
        - ...
- bin
  - com
    - ...
- ...
```

If the package declaration is missing or does not match the directory structure, an error is raised by the compiler.

If every class in a project shows such an error, you should check your `source` directory in the Compiler Configuration. Note that the value of this option is the `src` directory in the above example.