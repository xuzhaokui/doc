## 获得指定agent版本信息
```
GET /v1/agent/version/<version>
```

#### 请求包：
```
空
```



#### 返回包：
```
200
{
  version: <string>,
  sha256: [
    <uint8>,
  ... ],
  url: <string>
}
```


参数说明：
* `version` : agent版本号
* `sha256` : 该版本agent二进制文件sha256值
* `url` : 该版本agnet下载地址



## 创建agent版本（管理员）
```
POST /v1/agent/version
```

#### 请求包：
```
{
  version: <string>,
  sha256: [
    <uint8>,
  ... ],
  url: <string>
}
```


参数说明：

* `version` : agent版本号
* `sha256` : 该版本agent二进制文件sha256值
* `url` : 该版本agnet下载地址


#### 返回包：
```
200

```




## 列出所有告警
```
GET /v1/alerts/list
```

#### 请求包：
```
{
  start: <int64>,
  end: <int64>,
  active: <bool>
}
```


参数说明：

* `start` : 查询开始时间，uinx时间戳，单位为秒
* `end` : 查询结束时间，unix时间戳，单位为秒
* `active` : 查询条件，是否只查询当前活跃告警，false为查询所有告警


#### 返回包：
```
200
[
  {
    id: <string>,
    dedup_id: <string>,
    grouping: <string>,
    start: <int64>,
    end: <int64>,
    mute_until: <int64>,
    policy_id: <string>,
    adjust_ids: [
      <string>,
    ... ],
    tags: {
      <string>: <string>,
    ... },
    logs: [
      {
        uid: <string>,
        timestamp: <int64>,
        type: <string>,
        log: <string>
      },
    ... ]
  },
... ]
```


参数说明：
* `id` : 告警ID
* `dedup_id` : 告警去重ID，相同去重ID的告警认为是重复告警
* `grouping` : 告警分组ID，相同分组ID的告警认为可以分为一组
* `start` : 告警开始时间，unix时间戳
* `end` : 告警结束时间，unix时间戳
* `mute_until` : 告警抑制到达时间，unix时间戳
* `policy_id` : 告警对应策略ID
* `adjust_ids` : 告警对应所有微调ID
* `tags` : 告警内容tags
* `logs.uid` : 日志添加者
* `logs.timestamp` : 日志时间戳
* `logs.type` : 日志类型
* `logs.log` : 日志内容
* `logs` : 告警日志记录



## 删除业务组
```
DELETE /v1/apps/<app>
```

#### 请求包：
```
空
```



#### 返回包：
```
200

```




## 获得业务组详细信息
```
GET /v1/apps/<app>/inspect
```

#### 请求包：
```
空
```



#### 返回包：
```
200
{
  id: <string>,
  org: <string>,
  name: <string>,
  desc: <string>,
  creator: <string>,
  create_t: <int64>
  services: [
    <string>,
  ... ]
}
```


参数说明：
* `id` : 业务组ID
* `org` : 业务组所属组织
* `name` : 业务组名字
* `desc` : 业务组描述
* `creator` : 业务组创建者
* `create_t` : 业务组创建时间
* `services` : 业务组所包含所有服务



## 更新业务组信息
```
POST /v1/apps/<app>/update
```

#### 请求包：
```
{
  name: <string>,
  desc: <string>,
  services: [
    <string>,
  ... ]
}
```


参数说明：

* `name` : 业务组名字
* `desc` : 业务组描述
* `services` : 业务组所包含所有服务


#### 返回包：
```
200

```




## 创建业务组
```
POST /v1/apps/create
```

#### 请求包：
```
{
  name: <string>,
  desc: <string>,
  services: [
    <string>,
  ... ]
}
```


参数说明：

* `name` : 业务组名字
* `desc` : 业务组描述
* `services` : 业务组所包含所有服务


#### 返回包：
```
200
{
  id: <string>
}
```


参数说明：
* `id` : ID



## 得到业务组列表
```
GET /v1/apps/list
```

#### 请求包：
```
空
```



#### 返回包：
```
200
[
  {
    id: <string>,
    org: <string>,
    name: <string>,
    desc: <string>,
    creator: <string>,
    create_t: <int64>
  },
... ]
```


参数说明：
* `id` : 业务组ID
* `org` : 业务组所属组织
* `name` : 业务组名字
* `desc` : 业务组描述
* `creator` : 业务组创建者
* `create_t` : 业务组创建时间



## 删除集群
```
DELETE /v1/clusters/<cluster>
```

#### 请求包：
```
空
```



#### 返回包：
```
200

```




## 获取集群详细信息
```
GET /v1/clusters/<cluster>/inspect
```

#### 请求包：
```
空
```



#### 返回包：
```
200
{
  id: <string>,
  org: <string>,
  name: <string>,
  match_rules: [
    {
      field: <string>,
      regex: <string>,
      priority: <int>
    },
  ... ],
  desc: <string>,
  creator: <string>,
  create_t: <int64>
}
```


参数说明：
* `id` : 集群ID
* `org` : 集群所属组织
* `name` : 集群名字
* `match_rules.field` : 匹配字段，如hostname
* `match_rules.regex` : 匹配正则表达式
* `match_rules.priority` : 匹配优先级
* `match_rules` : 集群匹配规则
* `desc` : 集群描述
* `creator` : 集群创建者
* `create_t` : 集群创建时间



## 更新集群
```
POST /v1/clusters/<cluster>/update
```

#### 请求包：
```
{
  name: <string>,
  match_rules: [
    {
      field: <string>,
      regex: <string>,
      priority: <int>
    },
  ... ],
  desc: <string>
}
```


参数说明：

* `name` : 集群名字
* `match_rules.field` : 匹配字段，如hostname
* `match_rules.regex` : 匹配正则表达式
* `match_rules.priority` : 匹配优先级
* `match_rules` : 集群机器匹配规则
* `desc` : 集群描述


#### 返回包：
```
200

```




## 创建集群
```
POST /v1/clusters/create
```

#### 请求包：
```
{
  name: <string>,
  match_rules: [
    {
      field: <string>,
      regex: <string>,
      priority: <int>
    },
  ... ],
  desc: <string>
}
```


参数说明：

* `name` : 集群名字
* `match_rules.field` : 匹配字段，如hostname
* `match_rules.regex` : 匹配正则表达式
* `match_rules.priority` : 匹配优先级
* `match_rules` : 集群服务器匹配规则
* `desc` : 集群描述


#### 返回包：
```
200
{
  id: <string>
}
```


参数说明：
* `id` : ID



## 获得集群列表
```
GET /v1/clusters/list
```

#### 请求包：
```
空
```



#### 返回包：
```
200
[
  {
    id: <string>,
    org: <string>,
    name: <string>,
    match_rules: [
      {
        field: <string>,
        regex: <string>,
        priority: <int>
      },
    ... ],
    desc: <string>,
    creator: <string>,
    create_t: <int64>
  },
... ]
```


参数说明：
* `id` : 集群ID
* `org` : 集群所属组织
* `name` : 集群名字
* `match_rules.field` : 匹配字段，如hostname
* `match_rules.regex` : 匹配正则表达式
* `match_rules.priority` : 匹配优先级
* `match_rules` : 集群匹配规则
* `desc` : 集群描述
* `creator` : 集群创建者
* `create_t` : 集群创建时间



## 升级指定机器的agent版本
```
POST /v1/dog/upgrade
```

#### 请求包：
```
{
  org: <string>,
  host: <string>,
  dog_version: <string>
}
```


参数说明：

* `org` : 组织ID
* `host` : 服务器
* `dog_version` : agent版本号


#### 返回包：
```
200

```




## 列出所有事件
```
POST /v1/events/list
```

#### 请求包：
```
{
  time_start: <int64>,
  time_end: <int64>,
  hostnames: [
    <string>,
  ... ]
}
```


参数说明：

* `time_start` : TODO
* `time_end` : TODO
* `hostnames` : TODO


#### 返回包：
```
200
[
  {
    timestamp: <int64>,
    hostname: <string>,
    ts: <int64>,
    category: <string>,
    submod: <string>,
    target: <string>,
    change_type: <string>,
    case: [
      <uint8>,
    ... ]
    case: <data>
  },
... ]
```


参数说明：
* `timestamp` : 事件时间戳
* `hostname` : 事件发生机器
* `ts` : 事件发生时间（agent上报时间）
* `category` : 事件分类
* `submod` : 事件所属模块
* `target` : 事件目标
* `change_type` : 事件变更类型
* `case` : 事件原始信息
* `case` : TODO



## -
```
POST /v1/gate/report
```

#### 请求包：
```
空
```



#### 返回包：
```
200
{
  service_diff: {
    ver: <string>,
    ts: <int64>,
    full_dose: <bool>,
    add: {
      <string>: {
        apis: [
          <string>,
        ... ],
        eps: [
          <string>,
        ... ]
      },
    ... },
    del: {
      <string>: {
        apis: [
          <string>,
        ... ],
        eps: [
          <string>,
        ... ]
      },
    ... }
  },
  tversion: <string>
}
```


参数说明：
* `service_diff.ver` : TODO
* `service_diff.ts` : TODO
* `service_diff.full_dose` : TODO
* `service_diff.add.apis` : TODO
* `service_diff.add.eps` : TODO
* `service_diff.add` : TODO
* `service_diff.del.apis` : TODO
* `service_diff.del.eps` : TODO
* `service_diff.del` : TODO
* `service_diff` : TODO
* `tversion` : TODO



## 获得X-Service详细信息
```
POST /v1/groups/inspect
```

#### 请求包：
```
{
  service: <string>,
  cluster: <string>,
  app: <string>,
  version: <int64>
}
```


参数说明：

* `service` : X-Service所属服务
* `cluster` : X-Service所属集群
* `app` : X-Service所属业务
* `version` : X-Service版本号


#### 返回包：
```
200
{
  org: <string>,
  app: <string>,
  cluster: <string>,
  service: <string>,
  hosts: [
    <string>,
  ... ],
  cspg: [
    {
      proto: <string>,
      sto: <string>,
      ato: <string>,
      stage: <string>,
      tsc: <string>
      metrics: {
        <string>: {
          dt: {
            base: <int32>,
            step: <float64>,
            slots: [
              <int64>,
            ... ],
            phis: {
              <string>: <int32>,
            ... }
          },
          n: <float64>,
          iops: {
            <string>: <float64>,
          ... }
        },
      ... }
    },
  ... ],
  dep_cspg: [
    {
      proto: <string>,
      sto: <string>,
      ato: <string>,
      stage: <string>,
      tsc: <string>
      metrics: {
        <string>: {
          dt: {
            base: <int32>,
            step: <float64>,
            slots: [
              <int64>,
            ... ],
            phis: {
              <string>: <int32>,
            ... }
          },
          n: <float64>,
          iops: {
            <string>: <float64>,
          ... }
        },
      ... }
    },
  ... ],
  version: <int64>,
  is_aggr: <bool>
}
```


参数说明：
* `org` : X-Service所属组织
* `app` : X-Service所属业务组
* `cluster` : X-Service所属集群
* `service` : X-Service所属服务
* `hosts` : X-Service包括服务器
* `cspg.proto` : 网络协议
* `cspg.sto` : 源服务名称
* `cspg.ato` : 目标服务名称
* `cspg.stage` : 网络请求阶段
* `cspg.tsc` : 网络请求类型
* `cspg.metrics.dt.base` : http://misso.opsmind.com/cspg
* `cspg.metrics.dt.step` : http://misso.opsmind.com/cspg
* `cspg.metrics.dt.slots` : http://misso.opsmind.com/cspg
* `cspg.metrics.dt.phis` : http://misso.opsmind.com/cspg
* `cspg.metrics.dt` : CSPG DT结构（见CSPG文档: http://misso.opsmind.com/cspg）
* `cspg.metrics.n` : 值（见CSPG文档: http://misso.opsmind.com/cspg）
* `cspg.metrics.iops` : 网络请求每秒请求数
* `cspg.metrics` : CSPG数据体
* `cspg` : CSPG（见CSPG文档: http://misso.opsmind.com/cspg）
* `dep_cspg.proto` : 网络协议
* `dep_cspg.sto` : 源服务名称
* `dep_cspg.ato` : 目标服务名称
* `dep_cspg.stage` : 网络请求阶段
* `dep_cspg.tsc` : 网络请求类型
* `dep_cspg.metrics.dt.base` : http://misso.opsmind.com/cspg
* `dep_cspg.metrics.dt.step` : http://misso.opsmind.com/cspg
* `dep_cspg.metrics.dt.slots` : http://misso.opsmind.com/cspg
* `dep_cspg.metrics.dt.phis` : http://misso.opsmind.com/cspg
* `dep_cspg.metrics.dt` : CSPG DT结构（见CSPG文档: http://misso.opsmind.com/cspg）
* `dep_cspg.metrics.n` : 值（见CSPG文档: http://misso.opsmind.com/cspg）
* `dep_cspg.metrics.iops` : 网络请求每秒请求数
* `dep_cspg.metrics` : CSPG数据体
* `dep_cspg` : 服务依赖方CSPG（见CSPG文档: http://misso.opsmind.com/cspg）
* `version` : X-Service版本号
* `is_aggr` : 是否优化存储



## X-Service查询
```
POST /v1/groups/query
```

#### 请求包：
```
{
  service: [
    <string>,
  ... ],
  cluster: [
    <string>,
  ... ],
  app: [
    <string>,
  ... ]
}
```


参数说明：

* `service` : 查询服务列表
* `cluster` : 查询集群列表
* `app` : 查询业务组列表


#### 返回包：
```
200
[
  {
    service: <string>,
    cluster: <string>,
    app: <string>,
    version: <int64>
  },
... ]
```


参数说明：
* `service` : X-Service所属服务
* `cluster` : X-Service所属集群
* `app` : X-Service所属业务
* `version` : X-Service版本号



## X-Host查询
```
POST /v1/groups/xhost
```

#### 请求包：
```
{
  clusters: [
    <string>,
  ... ],
  apps: [
    <string>,
  ... ],
  services: [
    <string>,
  ... ],
  hosts: [
    <string>,
  ... ],
  version: <int64>
}
```


参数说明：

* `clusters` : X-Host集群列表
* `apps` : X-Host业务组列表
* `services` : X-Host服务列表
* `hosts` : X-Host服务器列表
* `version` : X-Host版本号（与X-Service通用）


#### 返回包：
```
200
{
  clusters: [
    <string>,
  ... ],
  apps: [
    <string>,
  ... ],
  services: [
    <string>,
  ... ],
  hosts: [
    <string>,
  ... ],
  version: <int64>
}
```


参数说明：
* `clusters` : X-Host集群列表
* `apps` : X-Host业务组列表
* `services` : X-Host服务列表
* `hosts` : X-Host服务器列表
* `version` : X-Host版本号（与X-Service通用）



## 删除服务器
```
POST /v1/hosts/delete
```

#### 请求包：
```
{
  hosts: [
    <string>,
  ... ]
}
```


参数说明：

* `hosts` : 服务器列表


#### 返回包：
```
200

```




## 获得服务器详情
```
POST /v1/hosts/inspect
```

#### 请求包：
```
{
  hosts: [
    <string>,
  ... ]
}
```


参数说明：

* `hosts` : 服务器列表


#### 返回包：
```
200
{
  <string>: {
    hostname: <string>,
    agent: {
      version: <string>,
      uptime: <int64>,
      warnings: [
        {
          level: <string>,
          mod: <string>,
          code: <string>,
          desc: <string>,
          detail: <string>
        },
      ... ],
      last_feedback: {
        srv: {
          ver: <string>,
          ts: <int64>
        }
      }
    },
    os: {
      host_id: <string>,
      os_name: <string>,
      os_dist: <string>,
      kernel_ver: <string>,
      mem_size: <uint64>,
      cpu_core: <uint32>,
      networks: {
        netdevs: [
          {
            name: <string>,
            addrs: [
              <string>,
            ... ],
            hw_addr: <string>,
            mtu: <int>,
            type: <uint32>
          },
        ... ]
      },
      services: [
        {
          name: <string>,
          listen: [
            {
              proto: <string>,
              addr: <string>
            },
          ... ]
        },
      ... ],
      procs: [
        {
          service: <string>,
          ctime: <int64>,
          name: <string>,
          pid: <int>,
          user: <string>,
          cpu: <float32>,
          mem: <uint64>
        },
      ... ],
      storage: [
        {
          device: <string>,
          mount_point: <string>,
          fstype: <string>
        },
      ... ]
    },
    update_time: <int64>,
    tags: [
      <string>,
    ... ],
    debug_boot: [
      <string>,
    ... ]
  },
... }
```


参数说明：
* `hostname` : TODO
* `agent.version` : TODO
* `agent.uptime` : TODO
* `agent.warnings.level` : TODO
* `agent.warnings.mod` : TODO
* `agent.warnings.code` : TODO
* `agent.warnings.desc` : TODO
* `agent.warnings.detail` : TODO
* `agent.warnings` : TODO
* `agent.last_feedback.srv.ver` : TODO
* `agent.last_feedback.srv.ts` : TODO
* `agent.last_feedback.srv` : TODO
* `agent.last_feedback` : TODO
* `agent` : TODO
* `os.host_id` : TODO
* `os.os_name` : TODO
* `os.os_dist` : TODO
* `os.kernel_ver` : TODO
* `os.mem_size` : TODO
* `os.cpu_core` : TODO
* `os.networks.netdevs.name` : TODO
* `os.networks.netdevs.addrs` : TODO
* `os.networks.netdevs.hw_addr` : TODO
* `os.networks.netdevs.mtu` : TODO
* `os.networks.netdevs.type` : TODO
* `os.networks.netdevs` : TODO
* `os.networks` : TODO
* `os.services.name` : TODO
* `os.services.listen.proto` : TODO
* `os.services.listen.addr` : TODO
* `os.services.listen` : TODO
* `os.services` : TODO
* `os.procs.service` : TODO
* `os.procs.ctime` : TODO
* `os.procs.name` : TODO
* `os.procs.pid` : TODO
* `os.procs.user` : TODO
* `os.procs.cpu` : TODO
* `os.procs.mem` : TODO
* `os.procs` : TODO
* `os.storage.device` : TODO
* `os.storage.mount_point` : TODO
* `os.storage.fstype` : TODO
* `os.storage` : TODO
* `os` : TODO
* `update_time` : TODO
* `tags` : TODO
* `debug_boot` : TODO



## 获得服务器列表
```
GET /v1/hosts/list
```

#### 请求包：
```
{
  detail: <int>
}
```


参数说明：

* `detail` : 是否列出详情


#### 返回包：
```
200
<data>
```


参数说明：



## 按tags查询服务器列表
```
POST /v1/hosts/tags/query
```

#### 请求包：
```
{
  tags: [
    {
      key: <string>,
      val: [
        <string>,
      ... ]
    },
  ... ]
}
```


参数说明：

* `tags.key` : tag键值
* `tags.val` : tag键值对应的值（多个）
* `tags` : 查询条件，tags列表


#### 返回包：
```
200
{
  hosts: [
    <string>,
  ... ]
}
```


参数说明：
* `hosts` : 服务器列表



## 更新服务器tags
```
POST /v1/hosts/tags/update
```

#### 请求包：
```
{
  tag: {
    <string>: {
      <string>: [
        <string>,
      ... ],
    ... },
  ... }
}
```


参数说明：

* `tag` : tags


#### 返回包：
```
200

```




## 获得监控项详情
```
GET /v1/metric/<metric>/config
```

#### 请求包：
```
空
```



#### 返回包：
```
200
{
  name: <string>,
  query: <string>,
  tags: {
    <string>: {
      desc: <string>,
      values: [
        <string>,
      ... ]
    },
  ... },
  desc: <string>,
  sparse: <bool>
}
```


参数说明：
* `name` : 监控项名字
* `query` : 监控项原始查询语句，兼容prometheus
* `tags.desc` : tag描述
* `tags.values` : tag可选value，可以为空
* `tags` : 监控项支持的查询条件
* `desc` : 监控项描述
* `sparse` : 是否为稀疏监控项



## 删除监控项
```
POST /v1/metric/config/delete/<delete>
```

#### 请求包：
```
空
```



#### 返回包：
```
200

```




## 列出所有监控项
```
GET /v1/metric/config/list
```

#### 请求包：
```
空
```



#### 返回包：
```
200
[
  {
    name: <string>,
    query: <string>,
    tags: {
      <string>: {
        desc: <string>,
        values: [
          <string>,
        ... ]
      },
    ... },
    desc: <string>,
    sparse: <bool>
  },
... ]
```


参数说明：
* `name` : 监控项名字
* `query` : 监控项原始查询语句，兼容prometheus
* `tags.desc` : tag描述
* `tags.values` : tag可选value，可以为空
* `tags` : 监控项支持的查询条件
* `desc` : 监控项描述
* `sparse` : 是否为稀疏监控项



## 新建或更新监控项
```
POST /v1/metric/config/save
```

#### 请求包：
```
{
  name: <string>,
  query: <string>,
  tags: {
    <string>: {
      desc: <string>,
      values: [
        <string>,
      ... ]
    },
  ... },
  desc: <string>,
  sparse: <bool>
}
```


参数说明：

* `name` : 监控项名字
* `query` : 监控项原始查询语句，兼容prometheus
* `tags.desc` : tag描述
* `tags.values` : tag可选value，可以为空
* `tags` : 监控项支持的查询条件
* `desc` : 监控项描述
* `sparse` : 是否为稀疏监控项


#### 返回包：
```
200

```




## 列出所有系统内置监控项
```
GET /v1/metric/template/list
```

#### 请求包：
```
空
```



#### 返回包：
```
200
[
  {
    name: <string>,
    query: <string>,
    tags: {
      <string>: {
        desc: <string>,
        values: [
          <string>,
        ... ]
      },
    ... },
    desc: <string>,
    sparse: <bool>
  },
... ]
```


参数说明：
* `name` : 监控项名字
* `query` : 监控项原始查询语句，兼容prometheus
* `tags.desc` : tag描述
* `tags.values` : tag可选value，可以为空
* `tags` : 监控项支持的查询条件
* `desc` : 监控项描述
* `sparse` : 是否为稀疏监控项



## 按查询条件读取时间序列
```
POST /v1/metrics/query
```

#### 请求包：
```
{
  mc: {
    name: <string>,
    query: <string>,
    tags: {
      <string>: {
        desc: <string>,
        values: [
          <string>,
        ... ]
      },
    ... },
    desc: <string>,
    sparse: <bool>
  },
  tags: {
    <string>: [
      <string>,
    ... ],
  ... },
  without: [
    <string>,
  ... ],
  start: <int64>,
  end: <int64>
}
```


参数说明：

* `mc.name` : 监控项名字
* `mc.query` : 监控项原始查询语句，兼容prometheus
* `mc.tags.desc` : tag描述
* `mc.tags.values` : tag可选value，可以为空
* `mc.tags` : 监控项支持的查询条件
* `mc.desc` : 监控项描述
* `mc.sparse` : 是否为稀疏监控项
* `mc` : 监控项
* `tags` : 查询条件
* `without` : 聚合算法将排除指定的tags，此选项用于在某些维度上聚合数据
* `start` : 查询时间序列的开始时间，unix时间戳
* `end` : 查询时间序列的结束时间，unix时间戳


#### 返回包：
```
200
{
  tss: [
    {
      tags: {
        <string>: <string>,
      ... },
      points: [
        {
          t: <int64>,
          v: <float64>
        },
      ... ]
    },
  ... ],
  sparse: <bool>
}
```


参数说明：
* `tss.tags` : 单条序列的数据标签
* `tss.points.t` : 时间戳
* `tss.points.v` : 值
* `tss.points` : 单条序列的数据点
* `tss` : 时间序列
* `sparse` : 是否为稀疏序列，稀疏序列一般不连续，有较多数据点缺失



## 按监控项取读时间序列
```
POST /v1/metrics/read
```

#### 请求包：
```
{
  metric: <string>,
  tags: {
    <string>: [
      <string>,
    ... ],
  ... },
  without: [
    <string>,
  ... ],
  start: <int64>,
  end: <int64>
}
```


参数说明：

* `metric` : 监控项
* `tags` : 查询条件
* `without` : 聚合算法将排除指定的tags，此选项用于在某些维度上聚合数据
* `start` : 查询时间序列的开始时间，unix时间戳
* `end` : 查询时间序列的结束时间，unix时间戳


#### 返回包：
```
200
{
  tss: [
    {
      tags: {
        <string>: <string>,
      ... },
      points: [
        {
          t: <int64>,
          v: <float64>
        },
      ... ]
    },
  ... ],
  sparse: <bool>
}
```


参数说明：
* `tss.tags` : 单条序列的数据标签
* `tss.points.t` : 时间戳
* `tss.points.v` : 值
* `tss.points` : 单条序列的数据点
* `tss` : 时间序列
* `sparse` : 是否为稀疏序列，稀疏序列一般不连续，有较多数据点缺失



## 创建组织
```
POST /v1/org
```

#### 请求包：
```
{
  name: <string>,
  desc: <string>
}
```


参数说明：

* `name` : 组织名
* `desc` : 组织描述


#### 返回包：
```
200

```




## 删除组织
```
POST /v1/org/delete
```

#### 请求包：
```
{
  id: <string>,
  name: <string>,
  desc: <string>,
}
```


参数说明：

* `id` : 组织ID
* `name` : 组织名字
* `desc` : 组织描述


#### 返回包：
```
200

```




## 列出所有组织
```
GET /v1/org/list
```

#### 请求包：
```
空
```



#### 返回包：
```
200
[
  {
    id: <string>,
    name: <string>,
    desc: <string>,
  },
... ]
```


参数说明：
* `id` : 组织ID
* `name` : 组织名字
* `desc` : 组织描述



## 给组织创建团队
```
POST /v1/org/team
```

#### 请求包：
```
{
  id: <string>,
  name: <string>,
  acl: [
    <string>,
  ... ],
  desc: <string>,
  email: <string>,
  email_flood: <bool>,
  subscribe: {
    <string>: [
      <string>,
    ... ],
  ... },
  host_scopes: [
    {
      key: <string>,
      val: [
        <string>,
      ... ]
    },
  ... ]
}
```


参数说明：

* `id` : 团队ID
* `name` : 团队名字
* `acl` : ACL列表
* `desc` : 团队描述
* `email` : 团队电子信箱
* `email_flood` : 告警是否发送给团队所有成员的email
* `subscribe` : 团队订阅的告警，告警tags与此字段匹配则该告警发送给此团队
* `host_scopes.key` : tag键值
* `host_scopes.val` : tag键值对应的值（多个）
* `host_scopes` : 团队管辖机器范围，与权限、告警等相关


#### 返回包：
```
200

```




## 删除团队
```
POST /v1/org/team/delete
```

#### 请求包：
```
{
  id: <string>,
  name: <string>,
  acl: [
    <string>,
  ... ],
  desc: <string>,
  email: <string>,
  email_flood: <bool>,
  subscribe: {
    <string>: [
      <string>,
    ... ],
  ... },
  host_scopes: [
    {
      key: <string>,
      val: [
        <string>,
      ... ]
    },
  ... ]
}
```


参数说明：

* `id` : 团队ID
* `name` : 团队名字
* `acl` : ACL列表
* `desc` : 团队描述
* `email` : 团队电子信箱
* `email_flood` : 告警是否发送给团队所有成员的email
* `subscribe` : 团队订阅的告警，告警tags与此字段匹配则该告警发送给此团队
* `host_scopes.key` : tag键值
* `host_scopes.val` : tag键值对应的值（多个）
* `host_scopes` : 团队管辖机器范围，与权限、告警等相关


#### 返回包：
```
200

```




## 更新团队信息
```
POST /v1/org/team/update
```

#### 请求包：
```
{
  id: <string>,
  name: <string>,
  acl: [
    <string>,
  ... ],
  desc: <string>,
  email: <string>,
  email_flood: <bool>,
  subscribe: {
    <string>: [
      <string>,
    ... ],
  ... },
  host_scopes: [
    {
      key: <string>,
      val: [
        <string>,
      ... ]
    },
  ... ]
}
```


参数说明：

* `id` : 团队ID
* `name` : 团队名字
* `acl` : ACL列表
* `desc` : 团队描述
* `email` : 团队电子信箱
* `email_flood` : 告警是否发送给团队所有成员的email
* `subscribe` : 团队订阅的告警，告警tags与此字段匹配则该告警发送给此团队
* `host_scopes.key` : tag键值
* `host_scopes.val` : tag键值对应的值（多个）
* `host_scopes` : 团队管辖机器范围，与权限、告警等相关


#### 返回包：
```
200

```




## 获得团队信息
```
GET /v1/org/teams
```

#### 请求包：
```
空
```



#### 返回包：
```
200
[
  {
    id: <string>,
    name: <string>,
    acl: [
      <string>,
    ... ],
    desc: <string>,
    email: <string>,
    email_flood: <bool>,
    subscribe: {
      <string>: [
        <string>,
      ... ],
    ... },
    host_scopes: [
      {
        key: <string>,
        val: [
          <string>,
        ... ]
      },
    ... ]
  },
... ]
```


参数说明：
* `id` : 团队ID
* `name` : 团队名字
* `acl` : ACL列表
* `desc` : 团队描述
* `email` : 团队电子信箱
* `email_flood` : 告警是否发送给团队所有成员的email
* `subscribe` : 团队订阅的告警，告警tags与此字段匹配则该告警发送给此团队
* `host_scopes.key` : tag键值
* `host_scopes.val` : tag键值对应的值（多个）
* `host_scopes` : 团队管辖机器范围，与权限、告警等相关



## 更新组织
```
POST /v1/org/update
```

#### 请求包：
```
{
  id: <string>,
  name: <string>,
  desc: <string>,
}
```


参数说明：

* `id` : 组织ID
* `name` : 组织名字
* `desc` : 组织描述


#### 返回包：
```
200

```




## 在组织下删除用户
```
POST /v1/org/user/delete
```

#### 请求包：
```
{
  id: <string>,
  name: <string>,
  email: <string>,
  desc: <string>,
  team: <string>
}
```


参数说明：

* `id` : 用户ID
* `name` : 用户显示名
* `email` : 用户电子信箱
* `desc` : 用户描述
* `team` : 用户所属团队


#### 返回包：
```
200

```




## 获得组织下所有用户信息
```
GET /v1/org/users
```

#### 请求包：
```
空
```



#### 返回包：
```
200
[
  {
    id: <string>,
    name: <string>,
    email: <string>,
    desc: <string>
  },
... ]
```


参数说明：
* `id` : 用户ID
* `name` : 用户名
* `email` : 用户电子邮件
* `desc` : 用户描述



## 删除告警策略微调
```
POST /v1/policies/<policie>/adjusts/<adjust>/delete
```

#### 请求包：
```
空
```



#### 返回包：
```
200

```




## 更新告警策略微调
```
POST /v1/policies/<policie>/adjusts/<adjust>/update
```

#### 请求包：
```
{
{
  threshold: <float64>,
  expired_at: <int64>,
  host_scopes: [
    {
      key: <string>,
      val: [
        <string>,
      ... ]
    },
  ... ],
  tags: {
    <string>: [
      <string>,
    ... ],
  ... },
  name: <string>,
  desc: <string>
}}
```


参数说明：

* `threshold` : 微调的新阀值
* `expired_at` : 微调过期时间，unix时间戳，单位为秒
* `host_scopes.key` : tag键值
* `host_scopes.val` : tag键值对应的值（多个）
* `host_scopes` : 微调作用的机器范围
* `tags` : 微调作用的tags范围，如 {device:[sda
* `name` : 微调名字
* `desc` : 微调描述


#### 返回包：
```
200

```




## 创建告警策略微调
```
POST /v1/policies/<policie>/adjusts/create
```

#### 请求包：
```
{
{
  threshold: <float64>,
  expired_at: <int64>,
  host_scopes: [
    {
      key: <string>,
      val: [
        <string>,
      ... ]
    },
  ... ],
  tags: {
    <string>: [
      <string>,
    ... ],
  ... },
  name: <string>,
  desc: <string>
}}
```


参数说明：

* `threshold` : 微调的新阀值
* `expired_at` : 微调过期时间，unix时间戳，单位为秒
* `host_scopes.key` : tag键值
* `host_scopes.val` : tag键值对应的值（多个）
* `host_scopes` : 微调作用的机器范围
* `tags` : 微调作用的tags范围，如 {device:[sda
* `name` : 微调名字
* `desc` : 微调描述


#### 返回包：
```
200
{
  adjust_id: <string>
}
```


参数说明：
* `adjust_id` : 告警微调ID



## 删除告警策略
```
POST /v1/policies/<policie>/delete
```

#### 请求包：
```
空
```



#### 返回包：
```
200

```




## 更新告警策略
```
POST /v1/policies/<policie>/update
```

#### 请求包：
```
{
{
  name: <string>,
  metric: <string>,
  tags: {
    <string>: [
      <string>,
    ... ],
  ... },
  operator: <string>,
  for: <int>,
  threshold: <float64>,
  desc: <string>,
  level: <string>
}}
```


参数说明：

* `name` : 策略名称
* `metric` : 策略对应监控项，只能给已存在的监控项填加策略
* `tags` : 监控项的查询条件
* `operator` : 判断条件，< > <= >= == != 之一
* `for` : 策略阈值持续触发时间
* `threshold` : 策略阈值
* `desc` : 策略描述
* `level` : 策略级别，warn info 之一


#### 返回包：
```
200

```




## 创建告警策略
```
POST /v1/policies/create
```

#### 请求包：
```
{
  name: <string>,
  metric: <string>,
  tags: {
    <string>: [
      <string>,
    ... ],
  ... },
  operator: <string>,
  for: <int>,
  threshold: <float64>,
  desc: <string>,
  level: <string>
}
```


参数说明：

* `name` : 策略名称
* `metric` : 策略对应监控项，只能给已存在的监控项填加策略
* `tags` : 监控项的查询条件
* `operator` : 判断条件，< > <= >= == != 之一
* `for` : 策略阈值持续触发时间
* `threshold` : 策略阈值
* `desc` : 策略描述
* `level` : 策略级别，warn info 之一


#### 返回包：
```
200
{
  policy_id: <string>
}
```


参数说明：
* `policy_id` : 告警策略ID



## 列出所有告警策略及所属微调
```
GET /v1/policies/list
```

#### 请求包：
```
空
```



#### 返回包：
```
200
[
  {
    id: <string>,
    creator: <string>,
    ctime: <int64>,
    mtime: <int64>,
    name: <string>,
    metric: <string>,
    tags: {
      <string>: [
        <string>,
      ... ],
    ... },
    operator: <string>,
    for: <int>,
    threshold: <float64>,
    desc: <string>,
    level: <string>
    adjusts: [
      {
        id: <string>,
        policy_id: <string>,
        creator: <string>,
        ctime: <int64>,
        mtime: <int64>,
        threshold: <float64>,
        expired_at: <int64>,
        host_scopes: [
          {
            key: <string>,
            val: [
              <string>,
            ... ]
          },
        ... ],
        tags: {
          <string>: [
            <string>,
          ... ],
        ... },
        name: <string>,
        desc: <string>
      },
    ... ]
  },
... ]
```


参数说明：
* `id` : 策略ID
* `creator` : 策略创建者
* `ctime` : 策略创建时间
* `mtime` : 策略最后修改时间
* `name` : 策略名称
* `metric` : 策略对应监控项，只能给已存在的监控项填加策略
* `tags` : 监控项的查询条件
* `operator` : 判断条件，< > <= >= == != 之一
* `for` : 策略阈值持续触发时间
* `threshold` : 策略阈值
* `desc` : 策略描述
* `level` : 策略级别，warn info 之一
* `adjusts.id` : TODO
* `adjusts.policy_id` : TODO
* `adjusts.creator` : TODO
* `adjusts.ctime` : TODO
* `adjusts.mtime` : TODO
* `adjusts.threshold` : 微调的新阀值
* `adjusts.expired_at` : 微调过期时间，unix时间戳，单位为秒
* `adjusts.host_scopes.key` : tag键值
* `adjusts.host_scopes.val` : tag键值对应的值（多个）
* `adjusts.host_scopes` : 微调作用的机器范围
* `adjusts.tags` : 微调作用的tags范围，如 {device:[sda
* `adjusts.name` : 微调名字
* `adjusts.desc` : 微调描述
* `adjusts` : 策略所包含所有微调



## 列出所有系统内置告警策略
```
GET /v1/policy/templates/list
```

#### 请求包：
```
空
```



#### 返回包：
```
200
[
  {
    id: <string>,
    creator: <string>,
    ctime: <int64>,
    mtime: <int64>,
    name: <string>,
    metric: <string>,
    tags: {
      <string>: [
        <string>,
      ... ],
    ... },
    operator: <string>,
    for: <int>,
    threshold: <float64>,
    desc: <string>,
    level: <string>
    adjusts: [
      {
        id: <string>,
        policy_id: <string>,
        creator: <string>,
        ctime: <int64>,
        mtime: <int64>,
        threshold: <float64>,
        expired_at: <int64>,
        host_scopes: [
          {
            key: <string>,
            val: [
              <string>,
            ... ]
          },
        ... ],
        tags: {
          <string>: [
            <string>,
          ... ],
        ... },
        name: <string>,
        desc: <string>
      },
    ... ]
  },
... ]
```


参数说明：
* `id` : 策略ID
* `creator` : 策略创建者
* `ctime` : 策略创建时间
* `mtime` : 策略最后修改时间
* `name` : 策略名称
* `metric` : 策略对应监控项，只能给已存在的监控项填加策略
* `tags` : 监控项的查询条件
* `operator` : 判断条件，< > <= >= == != 之一
* `for` : 策略阈值持续触发时间
* `threshold` : 策略阈值
* `desc` : 策略描述
* `level` : 策略级别，warn info 之一
* `adjusts.id` : TODO
* `adjusts.policy_id` : TODO
* `adjusts.creator` : TODO
* `adjusts.ctime` : TODO
* `adjusts.mtime` : TODO
* `adjusts.threshold` : 微调的新阀值
* `adjusts.expired_at` : 微调过期时间，unix时间戳，单位为秒
* `adjusts.host_scopes.key` : tag键值
* `adjusts.host_scopes.val` : tag键值对应的值（多个）
* `adjusts.host_scopes` : 微调作用的机器范围
* `adjusts.tags` : 微调作用的tags范围，如 {device:[sda
* `adjusts.name` : 微调名字
* `adjusts.desc` : 微调描述
* `adjusts` : 策略所包含所有微调



## prometheus兼容(/v1/label/*/values)
```
GET /v1/prom/api/v1/label/<label>/values
```

#### 请求包：
```
空
```



#### 返回包：
```
200
<data>
```


参数说明：



## prometheus兼容(/v1/query)
```
GET /v1/prom/api/v1/query
```

#### 请求包：
```
空
```



#### 返回包：
```
200
<data>
```


参数说明：



## prometheus兼容(/v1/query_range)
```
GET /v1/prom/api/v1/query_range
```

#### 请求包：
```
空
```



#### 返回包：
```
200
<data>
```


参数说明：



## prometheus兼容(/v1/series)
```
GET /v1/prom/api/v1/series
```

#### 请求包：
```
空
```



#### 返回包：
```
200
<data>
```


参数说明：



## 删除服务
```
DELETE /v1/services/<service>
```

#### 请求包：
```
空
```



#### 返回包：
```
200

```




## 列出服务所有已配置api
```
GET /v1/services/<service>/listapi
```

#### 请求包：
```
空
```



#### 返回包：
```
200
[
  <string>,
... ]
```


参数说明：



## 为服务设置api
```
POST /v1/services/<service>/setapi
```

#### 请求包：
```
{
  apis: [
    <string>,
  ... ]
}
```


参数说明：

* `apis` : api列表


#### 返回包：
```
200

```




## 列出所有服务
```
GET /v1/services/list
```

#### 请求包：
```
空
```



#### 返回包：
```
200
[
  <string>,
... ]
```


参数说明：



## 从团队中删除用户
```
POST /v1/team/<team>/user/delete
```

#### 请求包：
```
{
  id: <string>,
  name: <string>,
  email: <string>,
  desc: <string>,
  team: <string>
}
```


参数说明：

* `id` : 用户ID
* `name` : 用户显示名
* `email` : 用户电子信箱
* `desc` : 用户描述
* `team` : 用户所属团队


#### 返回包：
```
200

```




## 获得团队所有用户信息
```
GET /v1/teams/<team>/users
```

#### 请求包：
```
空
```



#### 返回包：
```
200
[
  {
    id: <string>,
    name: <string>,
    email: <string>,
    desc: <string>
  },
... ]
```


参数说明：
* `id` : 用户ID
* `name` : 用户名
* `email` : 用户电子邮件
* `desc` : 用户描述



## 获得用户信息
```
GET /v1/user
```

#### 请求包：
```
{
  id: <string>,
  name: <string>,
  email: <string>,
  desc: <string>,
  team: <string>
}
```


参数说明：

* `id` : 用户ID
* `name` : 用户显示名
* `email` : 用户电子信箱
* `desc` : 用户描述
* `team` : 用户所属团队


#### 返回包：
```
200
{
  id: <string>,
  name: <string>,
  email: <string>,
  desc: <string>
}
```


参数说明：
* `id` : 用户ID
* `name` : 用户名
* `email` : 用户电子邮件
* `desc` : 用户描述



## 创建用户
```
POST /v1/user
```

#### 请求包：
```
{
  id: <string>,
  name: <string>,
  email: <string>,
  desc: <string>,
  team: <string>
}
```


参数说明：

* `id` : 用户ID
* `name` : 用户显示名
* `email` : 用户电子信箱
* `desc` : 用户描述
* `team` : 用户所属团队


#### 返回包：
```
200

```




## 加用户加到团队
```
POST /v1/user/<user>/team
```

#### 请求包：
```
{
  id: <string>,
  name: <string>,
  email: <string>,
  desc: <string>,
  team: <string>
}
```


参数说明：

* `id` : 用户ID
* `name` : 用户显示名
* `email` : 用户电子信箱
* `desc` : 用户描述
* `team` : 用户所属团队


#### 返回包：
```
200

```




## 更新用户信息
```
POST /v1/user/update
```

#### 请求包：
```
{
  id: <string>,
  name: <string>,
  email: <string>,
  desc: <string>,
  team: <string>
}
```


参数说明：

* `id` : 用户ID
* `name` : 用户显示名
* `email` : 用户电子信箱
* `desc` : 用户描述
* `team` : 用户所属团队


#### 返回包：
```
200

```




## 删除授权key
```
POST /v1/userkey/delete
```

#### 请求包：
```
{
  name: <string>,
  public: <string>,
  private: <string>,
  acl: [
    <string>,
  ... ]
}
```


参数说明：

* `name` : 授权key名字
* `public` : 授权key公钥
* `private` : 授权key私钥（服务端不保存）
* `acl` : 授权key对应acl


#### 返回包：
```
200

```




## 列出所有授权key
```
GET /v1/userkey/list
```

#### 请求包：
```
空
```



#### 返回包：
```
200
[
  {
    name: <string>,
    public: <string>,
    private: <string>,
    acl: [
      <string>,
    ... ]
  },
... ]
```


参数说明：
* `name` : 授权key名字
* `public` : 授权key公钥
* `private` : 授权key私钥（服务端不保存）
* `acl` : 授权key对应acl



## 创建授权key
```
POST /v1/userkey/make
```

#### 请求包：
```
{
  name: <string>,
  public: <string>,
  private: <string>,
  acl: [
    <string>,
  ... ]
}
```


参数说明：

* `name` : 授权key名字
* `public` : 授权key公钥
* `private` : 授权key私钥（服务端不保存）
* `acl` : 授权key对应acl


#### 返回包：
```
200
{
  name: <string>,
  public: <string>,
  private: <string>,
  acl: [
    <string>,
  ... ]
}
```


参数说明：
* `name` : 授权key名字
* `public` : 授权key公钥
* `private` : 授权key私钥（服务端不保存）
* `acl` : 授权key对应acl



## 更新授权key
```
POST /v1/userkey/update
```

#### 请求包：
```
{
  name: <string>,
  public: <string>,
  private: <string>,
  acl: [
    <string>,
  ... ]
}
```


参数说明：

* `name` : 授权key名字
* `public` : 授权key公钥
* `private` : 授权key私钥（服务端不保存）
* `acl` : 授权key对应acl


#### 返回包：
```
200

```




## 列出所有用户存储
```
GET /v1/ustg/category/<category>/list
```

#### 请求包：
```
空
```



#### 返回包：
```
200
[
  {
    org: <string>,
    category: <string>,
    name: <string>
    creator: <string>,
    ctime: <int64>,
    mtime: <int64>,
    atime: <int64>,
    private: <bool>,
    meta: <string>,
    body: <string>
  },
... ]
```


参数说明：
* `org` : 用户存储所属组织
* `category` : 用户存储所属所类
* `name` : 用户存储名字
* `creator` : 用户存储创建者
* `ctime` : 用户存储创建时间
* `mtime` : 用户存储最后修改时间
* `atime` : 用户存储最后访问时间
* `private` : 是否为用户私有，私有存储只能被用户使用，公有存储被组织下所有有使用
* `meta` : 用户存储元信息
* `body` : 用户存储数据体



## 删除用户存储
```
POST /v1/ustg/category/<category>/name/<name>/delete
```

#### 请求包：
```
空
```



#### 返回包：
```
200

```




## 获得用户存储详细内容
```
GET /v1/ustg/category/<category>/name/<name>/read
```

#### 请求包：
```
空
```



#### 返回包：
```
200
{
  org: <string>,
  category: <string>,
  name: <string>
  creator: <string>,
  ctime: <int64>,
  mtime: <int64>,
  atime: <int64>,
  private: <bool>,
  meta: <string>,
  body: <string>
}
```


参数说明：
* `org` : 用户存储所属组织
* `category` : 用户存储所属所类
* `name` : 用户存储名字
* `creator` : 用户存储创建者
* `ctime` : 用户存储创建时间
* `mtime` : 用户存储最后修改时间
* `atime` : 用户存储最后访问时间
* `private` : 是否为用户私有，私有存储只能被用户使用，公有存储被组织下所有有使用
* `meta` : 用户存储元信息
* `body` : 用户存储数据体



## 创建或更新用户存储
```
POST /v1/ustg/category/<category>/name/<name>/upsert
```

#### 请求包：
```
{
  private: <bool>,
  meta: <string>,
  body: <string>
}
```


参数说明：

* `private` : 是否为用户私有，私有存储只能被用户使用，公有存储被组织下所有有使用
* `meta` : 用户存储元信息
* `body` : 用户存储数据体


#### 返回包：
```
200

```



