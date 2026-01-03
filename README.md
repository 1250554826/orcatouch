Orca Core 是 ORCA Hand 的核心控制包。它用于抽象硬件，提供校准和张紧脚本，并在关节空间中使用简单的高级控制方法来控制机械手。





![image-20260104005223715](D:\orcatouch\image\image1.png)

[**采购链接**](https://item.jd.com/10167956815203.html#switch-sku)

### **开始**

要开始使用 Orca Core，请按照以下步骤操作：

下载代码：

```
git clone https://ghfast.top/https://github.com/orcahand/orca_core.git
```

![2](D:\orcatouch\image\2.png)

### **1.****创建虚拟环境（推荐）：**

```
python3 -m venv venv

source venv/bin/activate
```

![3](D:\orcatouch\image\3.png)

如果您愿意，您还可以使用Poetry、pyenv、conda或任何其他环境管理器。

### **2.****安装依赖项：**

```
pip install pyserial


```

 ![4](D:\orcatouch\image\4.png)

```
cd projects/OrcaHand/orca_core/

pip install -e .
```

 ![5](D:\orcatouch\image\5.png)

![6](D:\orcatouch\image\6.png)

### **3.****检查配置文件：**

```
检查配置文件（例如orca_core/orca_core/models/orcahand_v1_right/config.yaml）


```

 ![7](D:\orcatouch\image\7.png)

并确保它与您的硬件设置相匹配。

修改

```
linux端：端口改为/dev/ttyUSB0
```

 ![8](D:\orcatouch\image\8.png)

### **4.**运行**张力和校准脚本**：

```
python scripts/tension.py orca_core/models/orcahand_v1_right
```

 ![9](D:\orcatouch\image\9.png)

```
python scripts/calibrate.py orca_core/models/orcahand_v1_right
```

 ![10](D:\orcatouch\image\10.png)

如果需要，用特定的手模文件夹替换该路径。

### **5.****将手移至中立位置****：**

```
python scripts/neutral.py orca_core/models/orcahand_v1_right
```



### **6.****示例用法：test.py**

这是一个可用于测试设置的最小示例脚本：

Python

```python
from orca_core import OrcaHand
import time
 
hand = OrcaHand('orca_core/models/orcahand_v1_right')
status = hand.connect()
print(status)
if not status[0]:
    print("Failed to connect to the hand.")
    exit(1)
 
hand.enable_torque()
 
joint_dict = {
    "index_mcp": 90,
    "middle_pip": 30,
}
 
hand.set_joint_pos(joint_dict, num_steps=25, step_size=0.001)
 
time.sleep(2)
hand.disable_torque()
hand.disconnect()
```

![11](D:\orcatouch\image\11.png)

### **笔记**

² 始终确保您的config.yaml硬件和接线相匹配。

² 文件夹中的所有脚本都scripts/将模型路径作为其第一个参数。

² 有关更高级的用法，请参阅其他脚本和 API 文档。

 

ID图

   ![12](D:\orcatouch\image\12.png)

![13](D:\orcatouch\image\13.png)



# 启动测试（右手）

```
检查配置文件（例如orca_core/orca_core/models/orcahand_v1_right/config.yaml）
```

![1.1](D:\orcatouch\image\1.1.png)

并确保它与您的硬件设置相匹配。

修改

```
linux端：端口改为/dev/ttyUSB0
```

![right_Orca Hand-2.png](D:\orcatouch\image\1.2.png)

```
python3 -m venv venv_right #执行一遍，后面启动就不需要再次执行了

source venv_right/bin/activate
```

![right_Orca Hand-0.png](D:\orcatouch\image\1.3.png)

运行**张力和校准脚本**：

**张力**

```
cd /home/robot/projects/OrcaHand/orca_core

python scripts/tension.py orca_core/models/orcahand_v1_right
```

**![right_Orca Hand-3.png](D:\orcatouch\image\1.4.png)**



灵巧手的手指使能，用手无法扳动。

**校准**

```
cd /home/robot/projects/OrcaHand/orca_core

python scripts/calibrate.py orca_core/models/orcahand_v1_right
```

校准前：

![right_Orca Hand-4.png](D:\orcatouch\image\1.5.png)

校准后：

![right_Orca Hand-5.png](D:\orcatouch\image\1.6.png)

### **将手移至中立位置****：**

```
python scripts/neutral.py orca_core/models/orcahand_v1_right


```

![right_Orca Hand-6.png](D:\orcatouch\image\1.7.png)

案例Demo

```
python3 scripts/main_demo.py orca_core/models/orcahand_v1_right


```

![right_Orca Hand-7.png](D:\orcatouch\image\1.8.png)

```
python3 scripts/main_demo_abduction.py orca_core/models/orcahand_v1_right


```

![right_Orca Hand-8.png](D:\orcatouch\image\1.9.png)

```
python scripts/zero.py orca_core/models/orcahand_v1_right


```

![right_Orca Hand-9.png](D:\orcatouch\image\2.0.png)

```
python3 scripts/slider_joint.py orca_core/models/orcahand_v1_right


```

![right_Orca Hand-10.png](D:\orcatouch\image\2.1.png)

```python
python3 scripts/slider_motor.py orca_core/models/orcahand_v1_right
```

![right_Orca Hand-11.png](D:\orcatouch\image\2.2.png)

python3 scripts/test.py

![right_Orca Hand-12.png](D:\orcatouch\image\2.3.png)

```
python 3 scripts/record_angles.py orca_core/models/orcahand_v1_right
```

![right_Orca Hand-20.png](D:\orcatouch\image\2,4.png)

Ctrl+C后自动保存成带有时间的yaml文件

![right_Orca Hand-21.png](D:\orcatouch\image\2.5.png)

选取其中一个录制好的动作序列，指定文件名，例如：

```python
python3 scripts/replay_angles.py orca_core/models/orcahand_v1_right  --replay_file  /home/robot/projects/OrcaHand/orca_core/replay_sequences/replay_sequence_20251224_155748.yaml
```

![right_Orca Hand-22.png](D:\orcatouch\image\2.6.png)