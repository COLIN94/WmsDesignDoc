# WMS业务功能&单据
## 问题点
1. 空的容器是否需要进行库位管理? 
    - 管理，空容器进行移动时，需要进行转移操作，操作不便。
    - **不管理，拆托时进行判断是否为空，为空则去掉与库位之间得联系。** 

## 收货
![avatar](png/arrival.png)
- 业务需求
    - 货拉到仓库门口，仓库进行收货
          
       1. 无来源收货，直接扫序列或者批次，
       2. 有来源收货
       
    ```flow
    st=>start: 开始
    isReferenceTask=>condition: 根据收货类型判断即菜单，是否参考源单收货
    scanSnLot=>operation: 扫描批次码或者序列码
    findTask=>condition: 根据扫描序列件或 批次码(批次+物料编码)，是否能查到唯一的一条入库任务
    returnTaskDetailId=>operation: 返回入库任务明细id
    tipSelectTask=>operation: 提示选择入库任务，对于是否选择明细，前台处理，扫描的批次或序列需要带一个入库任务明细id即可
    recoredScanSnLot=>operation: 记录扫描的序列，批次数量，入库任务明细id(可为空)
    scanCt=>operation: 扫描容器(可选步骤，扫了则代表收货时组托)
    scanWorkCell=>operation: 扫描或选择库位，或默认库位
    submitScanData=>operation: 数据提交：批次 数量   序列   库位   容器(可为空)   任务明细id(可为空) 
    createAriivalBill=>operation: 生成收货单：批次 数量   序列   库位   容器(可为空)   任务明细id  
    createStockTransaction=>operation: 根据收货单生成库存事务，货主通过任务id查询
    modifyStock=>operation: 库存更改
    e=>end: 结束
    st->isReferenceTask(yes)->scanSnLot->findTask(yes)->returnTaskDetailId->recoredScanSnLot->scanCt->scanWorkCell->submitScanData->createAriivalBill->createStockTransaction->modifyStock->e
    isReferenceTask(no)->recoredScanSnLot
    findTask(no)->tipSelectTask->recoredScanSnLot
    tipSelectTask->recoredScanSnLot
    &```
- 业务单据
## 质检
- 业务需求
- 业务单据
## 组托
- 业务需求
- 业务单据
## 上架
- 业务需求
- 业务单据
## 出库
- 业务需求
- 业务单据
