# CPU info

cpu_model=`cat /proc/cpuinfo | grep 'model name' | sort | uniq`
cpu_num=`cat /proc/cpuinfo | grep 'physical id' | sort | uniq | wc -l`
core_num=`cat /proc/cpuinfo |grep "cores"|uniq|awk '{print $4}'`
logic_core_num=`cat /proc/cpuinfo |grep "processor"|wc -l`

echo "CPU 的型号: $cpu_model"
echo "CPU 颗数: $cpu_num"
echo "CPU 核数: $core_num"
echo "逻辑 CPU 核数: $logic_core_num"

