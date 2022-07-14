# 条件字段

## 简介
使用`processor_fields_with_condition`插件匹配多个条件，如果其中一个条件得到满足，就会执行相应的行动。

## 配置参数

### `processor_fields_with_condition`配置

| 参数                     | 类型      | 是否必选 | 说明                                                |
| ---------------------- | ------- | ---- | ------------------------------------------------- |
| DropIfNotMatchCondition | Boolean  | 否 | 当条均件不满足时，日志是被丢弃（true）还是被保留（false），默认保留（false）。|
| Switch | Array，类型为Condition | 是 | 切换行动的条件。 |

### `Condition`类型说明

| 参数                     | 类型      | 是否必选 | 说明                                                |
| ---------------------- | ------- | ---- | ------------------------------------------------- |
| Case | ConditionCase  | 是 | 日志数据满足的条件。|
| Actions | Array，类型为ConditionAction | 是 | 满足条件时执行的动作。 |

### `ConditionCase`类型说明

| 参数                     | 类型      | 是否必选 | 说明                                                |
| ---------------------- | ------- | ---- | ------------------------------------------------- |
| LogicalOperator | String| 否 | 多个条件字段之间的逻辑运算符（and/or），默认值为and。 |
| RelationOperator | String | 否 | 条件字段的关系运算符（equals/regexp/contains/startwith），默认值为equals。 |
| FieldConditions | Map，其中fieldKey和fieldValue为String类型 | 是 | 字段名和表达式的键值对。 |

### `ConditionAction`类型说明

| 参数                     | 类型      | 是否必选 | 说明                                                |
| ---------------------- | ------- | ---- | ------------------------------------------------- |
| type | String | 是 |  行动类型，可选值是`processor_add_fields`/`processor_drop`。|
| IgnoreIfExist | Boolean | 否 | 当相同的键存在时是否要忽略，默认值是false |
| Fields | Map，其中fieldKey和fieldValue为String类型 | 是 | 附加字段的键值对。 |
| DropKeys | Array，类型为String | 是 | 丢弃字段。 |

## 样例

* 根据不同条件字段执行不同任务的采集配置
```
enable: true
inputs:
  - Type: metric_mock
    Fields:
      1111: "2222"
processors:
  - Type: processor_fields_with_condition
    SourceKey: content
    DropIfNotMatchCondition: true
    Switch:
      - Case:
          LogicalOperator: and
          RelationOperator: regexp
          FieldConditions:
            key1: "^value1.*"
            key2: "value1"
        Actions:
          - type: processor_add_fields
            IgnoreIfExist: false
            Fields:
              eventCode: "event_00001"
              name: "error_oom"
          - type: processor_drop
            DropKeys:
              - aaa1
              - aaa2
      - Case:
          LogicalOperator: and
          RelationOperator: regexp
          FieldConditions:
            key1: "^value2.*"
            key2: "value2"
        Actions:
          - type: processor_add_fields
            IgnoreIfExist: false
            Fields:
              eventCode: "event_00002"
              name: "error_oom2"
          - type: processor_drop
            DropKeys:
              - aaa1
              - aaa2

flushers:
  - Type: flusher_stdout
    OnlyStdout: true
```