# sql脚本
```js
// --run--
//新增自定义列脚本
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '多选' as column_name, 0 as is_default, sysdate() as create_date, 'usecaseDesign' as ascription, 'selection' as column_prop;

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '用例编号' as column_name, 1 as is_default, sysdate() as create_date, 'usecaseDesign' as ascription, 'usecaseCode' as column_prop;

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '用例名称' as column_name, 1 as is_default, sysdate() as create_date, 'usecaseDesign' as ascription, 'usecaseName' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '操作人' as column_name, 1 as is_default, sysdate() as create_date, 'usecaseDesign' as ascription, 'updateUser' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '关联业需' as column_name, 1 as is_default, sysdate() as create_date, 'usecaseDesign' as ascription, 'businessReqNameStr' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '关联软需' as column_name, 1 as is_default, sysdate() as create_date, 'usecaseDesign' as ascription, 'softwareReqNameStr' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '涉及功能' as column_name, 1 as is_default, sysdate() as create_date, 'usecaseDesign' as ascription, 'functionNameStr' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '关联用例' as column_name, 1 as is_default, sysdate() as create_date, 'usecaseDesign' as ascription, 'existUsecaseR' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '操作' as column_name, 0 as is_default, sysdate() as create_date, 'usecaseDesign' as ascription, 'operation' as column_prop;

//需求分析-软需

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '需求编号' as column_name, 0 as is_default, sysdate() as create_date, 'softRequirement' as ascription, 'requirementCode' as column_prop;

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '需求名称' as column_name, 0 as is_default, sysdate() as create_date, 'softRequirement' as ascription, 'requirementName' as column_prop;

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '需求状态' as column_name, 0 as is_default, sysdate() as create_date, 'softRequirement' as ascription, 'requirementStatusStr' as column_prop;

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '需求负责人' as column_name, 0 as is_default, sysdate() as create_date, 'softRequirement' as ascription, 'responsiblePerson' as column_prop;

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '预估工作量' as column_name, 0 as is_default, sysdate() as create_date, 'softRequirement' as ascription, 'expectWorkload' as column_prop;

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, 'FPA工作量' as column_name, 0 as is_default, sysdate() as create_date, 'softRequirement' as ascription, 'workLoad' as column_prop;

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '需求用例数' as column_name, 0 as is_default, sysdate() as create_date, 'softRequirement' as ascription, 'mainCaseNum' as column_prop;

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '操作' as column_name, 0 as is_default, sysdate() as create_date, 'softRequirement' as ascription, 'mainOpt' as column_prop;

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '阶段标识' as column_name, 0 as is_default, sysdate() as create_date, 'softRequirement' as ascription, 'sectionCode' as column_prop;

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '阶段状态' as column_name, 0 as is_default, sysdate() as create_date, 'softRequirement' as ascription, 'sectionStatusStr' as column_prop;

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '自动化/手工用例数' as column_name, 0 as is_default, sysdate() as create_date, 'softRequirement' as ascription, 'autotestCaseNum' as column_prop;

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '缺陷数' as column_name, 0 as is_default, sysdate() as create_date, 'softRequirement' as ascription, 'defectNum' as column_prop;

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '阶段操作' as column_name, 0 as is_default, sysdate() as create_date, 'softRequirement' as ascription, 'opt' as column_prop;



//业需自定义列
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '需求编号' as column_name, 0 as is_default, sysdate() as create_date, 'businessRequirement' as ascription, 'requirementCode' as column_prop;

INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '需求名称' as column_name, 0 as is_default, sysdate() as create_date, 'businessRequirement' as ascription, 'businessReqName' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '需求状态' as column_name, 0 as is_default, sysdate() as create_date, 'businessRequirement' as ascription, 'businessReqStatusName' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '创建日期' as column_name, 0 as is_default, sysdate() as create_date, 'businessRequirement' as ascription, 'createDate' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '需求负责人' as column_name, 0 as is_default, sysdate() as create_date, 'businessRequirement' as ascription, 'dutyUser' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '操作' as column_name, 0 as is_default, sysdate() as create_date, 'businessRequirement' as ascription, 'mainOpt' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '产品线' as column_name, 0 as is_default, sysdate() as create_date, 'businessRequirement' as ascription, 'productName' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, 'PO' as column_name, 0 as is_default, sysdate() as create_date, 'businessRequirement' as ascription, 'poName' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '需求用例数' as column_name, 0 as is_default, sysdate() as create_date, 'businessRequirement' as ascription, 'caseNum' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '操作' as column_name, 0 as is_default, sysdate() as create_date, 'businessRequirement' as ascription, 'opt' as column_prop;


//后台资产自定义列
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '多选' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'selection' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '涉及需求' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'requirementId' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '一级域' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'domainName1' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '二级域' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'domainName2' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '三级域' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'domainName3' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '应用英文名' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'enName' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '应用中文名' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'name' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '应用功能简述' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'description' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '应用类型' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'type' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '开发语言' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'developLanguage' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '开发框架' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'developFrameworkId' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '是否容器化' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'container' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '开发厂商' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'developer' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '业需编号' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'businessReqId' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '软需编号' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'requirementCode' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '评审通过时间' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'reviewPassData' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '责任团队' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'responsibleTeam' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '厂家责任人' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'productResponsiblePerson' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '局方责任人' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'officialResponsiblePerson' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '创建时间' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'createTime' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '创建人' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'createUser' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '修改时间' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'updateTime' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '修改人' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'updateUser' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '关联FPA' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'fpa' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '标签' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'tag' as column_prop;
INSERT INTO newland_assetmanage.t_custom_column(column_id, column_name, is_default, create_date, ascription, column_prop)
select replace(uuid(),'-','') as column_id, '操作' as column_name, 0 as is_default, sysdate() as create_date, 'backserviceAsset' as ascription, 'operation' as column_prop;



```

