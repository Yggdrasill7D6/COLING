### 安装

- 推荐使用 conda 先构建一个 Python-3.10 的虚拟环境

  ```bash
  conda create --name xtuner-env python=3.10 -y
  conda activate xtuner-env
  ```

- 通过 pip 安装 XTuner，并集成 DeepSpeed 安装：

  ```shell
  pip install -U 'xtuner[deepspeed]'
  ```

### 微调

- **步骤 1**，修改文件夹中的的参数文件，将数据集地址设置为自己的机器上的地址后，开始微调。

  ```shell
  xtuner train internlm2_chat_7b_law
  ```

  多卡运行指令如下：

  ```shell
  # 多卡
  NPROC_PER_NODE=64 xtuner train internlm2_chat_7b_law --deepspeed deepspeed_zero2
  ```
  
  - `--deepspeed` 表示使用 [DeepSpeed](https://github.com/microsoft/DeepSpeed) 🚀 来优化训练过程。


- **步骤 2**，将保存的 PTH 模型（如果使用的DeepSpeed，则将会是一个文件夹）转换为 HuggingFace 模型：

  ```shell
  xtuner convert pth_to_hf internlm2_chat_7b_law ${PTH} ${SAVE_PATH}
  ```

这样就能够得到我们训练的模型。