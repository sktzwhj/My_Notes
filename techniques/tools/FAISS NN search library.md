#Facebook FAISS install

在服务器上折腾东西总是麻烦些，记录一下安装FAISS遇到的问题。

首先MKL库的load有问题，回头看了看Makefile其实提到了

you may have to set the LD_LIBRARY_PATH=$MKLROOT/lib/intel64 at runtime.
If at runtime you get the error:
Intel MKL FATAL ERROR: Cannot load libmkl_avx2.so or libmkl_def.so.
You may add set
LD_PRELOAD=$MKLROOT/lib/intel64/libmkl_core.so:$MKLROOT/lib/intel64/libmkl_sequential.so
at runtime as well.

另外FAISS的python swig封装要求参数类型只能是float32，而numpy生成的默认是float64.