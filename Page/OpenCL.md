**OpenCL**（**Open** **C**omputing **L**anguage，开放计算语言）是一个为异构平台编写程序的框架，此异构平台可由[CPU](https://zh.wikipedia.org/wiki/CPU "wikilink")、[GPU](https://zh.wikipedia.org/wiki/GPU "wikilink")、[DSP](https://zh.wikipedia.org/wiki/DSP "wikilink")、[FPGA或其他类型的处理器與硬體加速器所组成](https://zh.wikipedia.org/wiki/FPGA "wikilink")。OpenCL由一门用于编写kernels（在OpenCL设备上运行的函数）的语言（基于[C99](https://zh.wikipedia.org/wiki/C99 "wikilink")）和一组用于定义并控制平台的API组成。OpenCL提供了基于任务分割和数据分割的[并行计算](../Page/并行计算.md "wikilink")机制。

OpenCL类似于另外两个开放的工业标准[OpenGL](../Page/OpenGL.md "wikilink")和[OpenAL](../Page/OpenAL.md "wikilink")，这两个标准分别用于三维图形和计算机音频方面。OpenCL擴充了GPU圖形生成之外的能力。OpenCL由非盈利性技术组织[Khronos Group掌管](https://zh.wikipedia.org/wiki/Khronos_Group "wikilink")。

## 历史

OpenCL最初由[苹果公司开发](https://zh.wikipedia.org/wiki/苹果公司 "wikilink")，拥有其商标权，并在与[AMD](https://zh.wikipedia.org/wiki/AMD "wikilink")，[IBM](../Page/IBM.md "wikilink")，[Intel和](https://zh.wikipedia.org/wiki/Intel "wikilink")[NVIDIA技术团队的合作之下初步完善](https://zh.wikipedia.org/wiki/NVIDIA "wikilink")。随后，苹果将这一草案提交至[Khronos Group](https://zh.wikipedia.org/wiki/Khronos_Group "wikilink")。

2008年6月16日，Khronos的通用计算工作小组成立\[1\]。5个月后的2008年11月18日，该工作组完成了OpenCL 1.0规范的技术细节\[2\]。该技术规范在由Khronos成员进行审查之后，于2008年12月8日公开发表\[3\]。2010年6月14日，OpenCL 1.1发布\[4\]。

## 範例

### 快速傅立葉變換

一個[快速傅立葉變換的式子](https://zh.wikipedia.org/wiki/快速傅立葉變換 "wikilink")： \[5\]

``` c
  // create a compute context with GPU device
  context = clCreateContextFromType(NULL, CL_DEVICE_TYPE_GPU, NULL, NULL, NULL);

  // create a command queue
  queue = clCreateCommandQueue(context, NULL, 0, NULL);

  // allocate the buffer memory objects
  memobjs[0] = clCreateBuffer(context, CL_MEM_READ_ONLY | CL_MEM_COPY_HOST_PTR, sizeof(float)*2*num_entries, srcA, NULL);
  memobjs[1] = clCreateBuffer(context, CL_MEM_READ_WRITE, sizeof(float)*2*num_entries, NULL, NULL);

  // create the compute program
  program = clCreateProgramWithSource(context, 1, &fft1D_1024_kernel_src, NULL, NULL);

  // build the compute program executable
  clBuildProgram(program, 0, NULL, NULL, NULL, NULL);

  // create the compute kernel
  kernel = clCreateKernel(program, "fft1D_1024", NULL);

  // set the args values
  clSetKernelArg(kernel, 0, sizeof(cl_mem),(void *)&memobjs[0]);
  clSetKernelArg(kernel, 1, sizeof(cl_mem),(void *)&memobjs[1]);
  clSetKernelArg(kernel, 2, sizeof(float)*(local_work_size[0]+1)*16, NULL);
  clSetKernelArg(kernel, 3, sizeof(float)*(local_work_size[0]+1)*16, NULL);

  // create N-D range object with work-item dimensions and execute kernel
  global_work_size[0] = num_entries;
  local_work_size[0] = 64;
  clEnqueueNDRangeKernel(queue, kernel, 1, NULL, global_work_size, local_work_size, 0, NULL, NULL);
```

真正的運算：（基於[Fitting FFT onto the G80 Architecture](http://www.cs.berkeley.edu/~kubitron/courses/cs258-S08/projects/reports/project6_report.pdf)）\[6\]

``` c
  // This kernel computes FFT of length 1024. The 1024 length FFT is decomposed into
  // calls to a radix 16 function, another radix 16 function and then a radix 4 function

  __kernel void fft1D_1024(__global float2 *in, __global float2 *out,
                          __local float *sMemx, __local float *sMemy){
    int tid = get_local_id(0);
    int blockIdx = get_group_id(0) * 1024 + tid;
    float2 data[16];

    // starting index of data to/from global memory
    in = in + blockIdx;  out = out + blockIdx;

    globalLoads(data, in, 64); // coalesced global reads
    fftRadix16Pass(data);      // in-place radix-16 pass
    twiddleFactorMul(data, tid, 1024, 0);

    // local shuffle using local memory
    localShuffle(data, sMemx, sMemy, tid, (((tid & 15)* 65) +(tid >> 4)));
    fftRadix16Pass(data);               // in-place radix-16 pass
    twiddleFactorMul(data, tid, 64, 4); // twiddle factor multiplication

    localShuffle(data, sMemx, sMemy, tid, (((tid >> 4)* 64) +(tid & 15)));

    // four radix-4 function calls
    fftRadix4Pass(data);      // radix-4 function number 1
    fftRadix4Pass(data + 4);  // radix-4 function number 2
    fftRadix4Pass(data + 8);  // radix-4 function number 3
    fftRadix4Pass(data + 12); // radix-4 function number 4

    // coalesced global writes
    globalStores(data, out, 64);
  }
```

Apple的網站上可以發現傅立葉變換的例子\[7\]

### 平行合併排序法

使用 Python 3.x 搭配 PyOpenCL 與 NumPy

<div style="height:400px; overflow-y: scroll;">

``` python3
import io
import random
import numpy as np
import pyopencl as cl

def dump_step(data, chunk_size):
    """顯示排序過程"""
    msg = io.StringIO('')
    div = io.StringIO('')
    for idx, item in enumerate(data):
        if idx % chunk_size == 0:
            if idx > 0:
                msg.write(' ||')
                div.write('   ')
            div.write(' --')
        else:
            msg.write('   ')
            div.write('------')
        msg.write(' {:2d}'.format(item))

    out = msg.getvalue()
    if chunk_size == 1: print(' ' + '-' * (len(out) - 1))
    print(out)
    print(div.getvalue())
    msg.close()
    div.close()

def cl_merge_sort_sbs(data_in):
    """平行合併排序"""
    # OpenCL kernel 函數程式碼
    CL_CODE = '''
    kernel void merge(int chunk_size, int size, global long* data, global long* buff) {
        // 取得分組編號
        const int gid = get_global_id(0);

        // 根據分組編號計算責任範圍
        const int offset = gid * chunk_size;
        const int real_size = min(offset + chunk_size, size) - offset;
        global long* data_part = data + offset;
        global long* buff_part = buff + offset;

        // 設定合併前的初始狀態
        int r_beg = chunk_size >> 1;
        int b_ptr = 0;
        int l_ptr = 0;
        int r_ptr = r_beg;

        // 進行合併
        while (b_ptr < real_size) {
            if (r_ptr >= real_size) {
                // 若右側沒有資料，取左側資料堆入緩衝區
                buff_part[b_ptr] = data_part[l_ptr++];
            } else if (l_ptr == r_beg) {
                // 若左側沒有資料，取右側資料堆入緩衝區
                buff_part[b_ptr] = data_part[r_ptr++];
            } else {
                // 若兩側都有資料，取較小資料堆入緩衝區
                if (data_part[l_ptr] < data_part[r_ptr]) {
                    buff_part[b_ptr] = data_part[l_ptr++];
                } else {
                    buff_part[b_ptr] = data_part[r_ptr++];
                }
            }
            b_ptr++;
        }
    }
    '''

    # 配置計算資源，編譯 OpenCL 程式
    ctx = cl.Context(dev_type=cl.device_type.GPU)
    prg = cl.Program(ctx, CL_CODE).build()
    queue = cl.CommandQueue(ctx)
    mf = cl.mem_flags

    # 資料轉換成 numpy 形式以利轉換為 OpenCL Buffer
    data_np = np.int64(data_in)
    buff_np = np.empty_like(data_np)

    # 建立緩衝區，並且複製數值到緩衝區
    data = cl.Buffer(ctx, mf.READ_WRITE | mf.COPY_HOST_PTR, hostbuf=data_np)
    buff = cl.Buffer(ctx, mf.READ_WRITE | mf.COPY_HOST_PTR, hostbuf=buff_np)

    # 設定合併前初始狀態
    data_len = np.int32(len(data_np))
    chunk_size = np.int32(1)

    dump_step(data_np, chunk_size)
    while chunk_size < data_len:
        # 更新分組大小，每一回合變兩倍
        chunk_size <<= 1
        # 換算平行作業組數
        group_size = ((data_len - 1) // chunk_size) + 1
        # 進行分組合併作業
        prg.merge(queue, (group_size,), (1,), chunk_size, data_len, data, buff)
        # 將合併結果作為下一回合的原始資料
        temp = data
        data = buff
        buff = temp
        # 顯示此回合狀態
        cl.enqueue_copy(queue, data_np, data)
        dump_step(data_np, chunk_size)

    queue.finish()
    data.release()
    buff.release()

def main():
    n = random.randint(5, 16)
    data = []
    for i in range(n):
        data.append(random.randint(1, 99))
    cl_merge_sort_sbs(data)

if __name__ == '__main__':
    main()
```

</div>

執行結果：

``` text
 --------------------------------------------------------------------------------------
 85 || 41 || 64 || 40 || 90 || 29 || 38 || 41 || 64 || 17 || 20 || 41 || 16 || 65 || 83
 --    --    --    --    --    --    --    --    --    --    --    --    --    --    --
 41    85 || 40    64 || 29    90 || 38    41 || 17    64 || 20    41 || 16    65 || 83
 --------    --------    --------    --------    --------    --------    --------    --
 40    41    64    85 || 29    38    41    90 || 17    20    41    64 || 16    65    83
 --------------------    --------------------    --------------------    --------------
 29    38    40    41    41    64    85    90 || 16    17    20    41    64    65    83
 --------------------------------------------    --------------------------------------
 16    17    20    29    38    40    41    41    41    64    64    65    83    85    90
 --------------------------------------------------------------------------------------
```

## 參考文獻

## 外部連結

  - [支援OpenCL的產品](https://www.khronos.org/conformance/adopters/conformant-products/opencl)
  - [开源GPU社区](https://web.archive.org/web/20190122085224/http://www.opengpu.org/)

## 参见

  - [GPGPU](https://zh.wikipedia.org/wiki/GPGPU "wikilink")
  - [CUDA](../Page/CUDA.md "wikilink")
  - [DirectCompute](../Page/DirectCompute.md "wikilink")
  - [C++ AMP](../Page/C++_AMP.md "wikilink")
  - [比特币](../Page/比特币.md "wikilink")的挖礦

{{-}}

[Category:计算机语言](https://zh.wikipedia.org/wiki/Category:计算机语言 "wikilink") [Category:GPGPU](https://zh.wikipedia.org/wiki/Category:GPGPU "wikilink")

1.
2.
3.
4.
5.
6.
7.  .