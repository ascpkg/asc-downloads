https://github.com/llvm/llvm-project/releases/tag/llvmorg-13.0.0

https://github.com/sighingnow/libclang/releases/tag/llvm-13.0.0

https://pypi.org/project/libclang/13.0.0/#files

```git
commit d7b669b3a30345cfcdb2fde2af6f48aa4b94845d (HEAD -> main, tag: llvmorg-13.0.0-rc4, tag: llvmorg-13.0.0)
Author: Matheus Izvekov <mizvekov@gmail.com>
Date:   Wed Sep 15 01:46:30 2021 +0200

    [clang] don't mark as Elidable CXXConstruct expressions used in NRVO

    See PR51862.

    The consumers of the Elidable flag in CXXConstructExpr assume that
    an elidable construction just goes through a single copy/move construction,
    so that the source object is immediately passed as an argument and is the same
    type as the parameter itself.

    With the implementation of P2266 and after some adjustments to the
    implementation of P1825, we started (correctly, as per standard)
    allowing more cases where the copy initialization goes through
    user defined conversions.

    With this patch we stop using this flag in NRVO contexts, to preserve code
    that relies on that assumption.
    This causes no known functional changes, we just stop firing some asserts
    in a cople of included test cases.

    Reviewed By: rsmith

    Differential Revision: https://reviews.llvm.org/D109800

    (cherry picked from commit d9308aa39b236064a680ca57178af3c731e13e49)

 clang/include/clang/Sema/Initialization.h | 16 ++++++-------
 clang/lib/AST/ExprConstant.cpp            | 15 ++++++++++---
 clang/lib/CodeGen/CGExprCXX.cpp           | 19 +++++++++-------
 clang/lib/Sema/Sema.cpp                   |  2 +-
 clang/lib/Sema/SemaCoroutine.cpp          |  2 +-
 clang/lib/Sema/SemaDeclCXX.cpp            |  9 ++++++++
 clang/lib/Sema/SemaExpr.cpp               |  2 +-
 clang/lib/Sema/SemaExprCXX.cpp            |  5 ++---
 clang/lib/Sema/SemaLambda.cpp             |  3 +--
 clang/lib/Sema/SemaObjCProperty.cpp       |  3 +--
 clang/lib/Sema/SemaStmt.cpp               |  8 +++----
 clang/test/CodeGen/nrvo-tracking.cpp      | 37 +++++++++++++++++++++++++++++++
 clang/test/CodeGenCXX/copy-elision.cpp    | 34 ++++++++++++++++++++++++++++
 13 files changed, 122 insertions(+), 33 deletions(-)
```
