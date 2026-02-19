<div align="center">

# Local Build for CUDA 12.8+

</div>

This tutorial provides a step-by-step guide on how to compile and install `cumm` and `spconv` from source specifically for CUDA 12.8.

This tutorial has benn tested on CUDA 12.8, Python 3.12, and CUDA arch 10.0.

Steps:

`cumm` install
```bash
# if cumm is intalled, uninstall it
pip list | grep cumm # pip uninstall cumm
export CUDA_PATH="path/to/you/cuda/dir/"
git clone https://github.com/RayYoh/cumm.git

cd cumm
export CUMM_CUDA_VERSION="12.8" # cuda version
export CUMM_DISABLE_JIT="1" # build whl then install
# GPU arch, https://developer.nvidia.com/cuda/gpus
export CUMM_CUDA_ARCH_LIST="10.0"
python3 setup.py bdist_wheel
pip install dist/cumm_cu128-0.8.2-cp312-cp312-linux_x86_64.whl
```

`spconv` install
```bash
pip list | grep spconv # pip uninstall spconv*
git clone https://github.com/kenomo/spconv.git

cd spconv
export SPCONV_DISABLE_JIT="1"
cd spconv
python3 setup.py bdist_wheel
pip install dist/spconv_cu128-2.3.8-cp312-cp312-linux_x86_64.whl

# test
python test/benchmark.py && \
python test/fake_train.py
```

Note: Compiling these libraries is resource-intensive. Ensure your system has sufficient RAM and that your MAX_JOBS environment variable is set appropriately to avoid out-of-memory errors during the build process.

## :clap: Acknowledgement

[[Blog]](https://zhuanlan.zhihu.com/p/672153815), [[kenomo]](https://github.com/traveller59/spconv/issues/746#issuecomment-3155991737)