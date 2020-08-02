# HUSTAU 场地/物资借用小程序

# 场地借用系统

## 需求

- 填表者/管理者均要登陆
- 空闲状况公示
- 前端申请者填表上交
- 后端秘书部审批(通过/不通过 + 备注)、撤回审批
- 审批通过后申请人能打印凭证(HTML/图片)
- 后台能导出表格存档

## Docs

- [开发文档](./docs/facilities.md)
- [数据库字段](./docs/facilities_database.md)
- [云函数API](./docs/cloud_function.md)

## 下一步
- 表格有附件上传需求
- 填表过程进度保存


# 物资借用系统

## 基础信息
- 目标发布日期：2019春季学期结束前
- 参与开发者：思存工作室
  @Bananana Fish @Dorence @MakingBigNewsWallace @renza101 @wnllixiao
  @zhanglongjianjie @Zhengkai456
- 对接联络人：@star-du 

## 目标
- 用户：将原有的qq联络借用物资改为小程序上操作，可查询物资的当前库存，并强制流程规范化
- 管理员：借用记录存档，方便核查物资的实时状态；线上审批
- 新增物资：新增新的物资时能直接更新数据库

## 其他功能需求
注：此部分功能不包括在一期任务内

|#| 功能名 | 描述 | 优先级
|-| ----- | ----- | ------
|1| 物资选择图片|少部分物资不易描述，需要后台预先上传图片|Should Have
|2| 管理员新增物资|管理员创建新物资项，填写数量、类别、位置|Should Have
|3| 显示所有物资|管理员查看当前所有物资，及其数量、状态|Could Have
|4| 物资搜索|方便找到物资|Could Have

## 用户交互&设计
注：展示基础版本交互逻辑
1. tab主页面：列表
   - 物资查询及借用
   - 表单状态
   - 新增仓库物资
  
   管理员审批 [仅对管理员显示]
    - 未审批
    - 未通过
    - 已通过
    - 编辑现有物资

2. 物资查询及借用
    1. 点击后首先跳转至查询选择页面：根据类别/标签找到借用物资 - 选择借用时间（2周内） - 显示该时间物资剩余数量 - 填入借用数量 - 点击确认按钮
    2. 显示“注意事项及手续流程”页面 - 点击“我已阅读”
    3. 显示表单页 - 填写表单1(见后，下同) - 点击提交 - 弹窗提示成功并返回tab主页
3. 表单状态
   - 注意事项 - 跳转到“注意事项及手续流程”
   - 借用物资表单情况（仅显示用户本人提交的表单，见表单2） - 
     1. 状态：未审批
     2. 状态：未通过 - 可以查看拒绝理由
     3. 状态：已通过- 点击按钮“去归还” - 跳转至表单3
     4. 状态：归还待审批
     5. 状态：已审批归还  
    注：
      - 希望实现状态为“已通过”时，主tab表单状态栏出现红点提示 
      - 状态3时表单增加“物资位置”信息，并突出提示
   - 新增物资表单
     1. 状态：未审批
     2. 状态：未通过 
     3. 状态：已通过
4. 新增仓库物资
   1. 显示“注意事项及手续流程”页面 - 点击“我已阅读”
   2. 显示表单4 - 点击提交 - 弹窗提示成功并返回tab主页
5. 管理员审批   
   各个类别显示对应表单 - 点击“去审批” - 跳转表单5   
   注：若是新增物资表单，管理员可以编辑物资名称/类别
6*. 管理员编辑物资   
   当前版本要求：管理员选择某物资-修改物资数量/其他信息 - 弹窗确认 

注：借用时数量可能与归还时不一致（部分消耗/遗失），只要归还时注明，得到管理员审批通过即可

## 表单

### 表单1：借用物资表单
借用物资名称、数量、借用时间（2周内）：前一页面选择

- 单位名称  部门/协会名称
- 借用用途
- 归还日期（2周内）
- 借用人姓名
- 联系方式
- 学号
- 院系班级

### 表单2：借用物资表单情况
- 借用物资
- 借用编号
- 借用时间
- 归还时间 
- 申请人／联系方式
- 学号／院系班级
- 审批状态
- 审批人
- 审批意见

### 表单3：归还物资表单
单位名称、归还物资名称、借用物资数量：直接显示

- 归还日期（默认当日，可选）
- 归还物资位置（可选）
- *归还物资数量*
- 物资使用情况（是否有损坏）（填写）

### 表单4：新增物资表单
- 单位名称  部门／协会
- 物资类别 新物资／原有物资
- 物资名称 （新物资填写名称，原有物资选择）
- 新增物资数量  数字
- 物资位置（可选）
- [对于新物资] 选择类别/标签
- 新增时间
- 负责人姓名
- 联系方式
- 学号
- 院系班级
- 备注

### 表单5：管理员审批表单
注：以借用物资为例

- 借用物资名称、数量
- 单位名称  部门/协会名称
- 借用用途
- 借用日期
- 归还日期
- 借用人姓名
- 联系方式
- 学号
- 院系班级
- 审批状态
- 审批人
- 审批意见


## 参考文档

+ [云开发文档](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/basis/getting-started.html)
