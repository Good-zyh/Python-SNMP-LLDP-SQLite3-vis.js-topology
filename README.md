# Python-SNMP-LLDP-SQLite3-vis.js-topology
Python-SNMP-LLDP-SQLite3-vis.js-topology

这个Python脚本主要用于通过SNMP协议发现网络设备并获取LLDP（链路层发现协议）信息，然后将这些信息整理并生成用于创建网络拓扑图的JavaScript文件（nodes.js和edges.js）。以下是代码的主要功能和结构：

SNMP Walk 函数 (snmp_walk):

使用 pysnmp 库执行SNMP Walk，查询指定的OID（对象标识符）并从网络设备中获取信息。
数据库操作:

创建一个SQLite内存数据库（con = sqlite3.connect(':memory:')）用于存储LLDP相关信息。
创建表格（lldpLocSysName、lldpLocPortId、lldpRemPortId）用于存储本地系统名称、本地端口ID和远程端口ID。
设备发现和LLDP信息获取:

从文件中读取有关交换机的信息（社区字符串、SNMP端口、IP）。
对于每个交换机，执行SNMP Walk以收集LLDP相关信息（本地系统名称、本地端口ID、远程系统名称、远程端口ID）。
使用获取的LLDP信息填充SQLite表格。
拓扑数据生成:

生成用于使用vis.js库创建网络拓扑图的节点（nodes.js）和边缘（edges.js）。
节点表示设备，边缘表示设备之间的连接。
输出:

打印每个交换机的LLDP信息。
将生成的节点和边缘数据写入JavaScript文件（nodes.js和edges.js）。

——————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————
从文件中读取有关交换机的信息，该文件的格式是：
community_string1, snmp_port1, ip1
community_string2, snmp_port2, ip2
community_string3, snmp_port3, ip3

其中每一行包含一个交换机的信息，包括社区字符串、SNMP端口和IP地址。您可以通过命令行参数来指定包含此信息的文件。在脚本中，使用了 -f 或 --file 参数：
python script.py -f switches.txt
