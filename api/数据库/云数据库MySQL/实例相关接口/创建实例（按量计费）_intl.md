## 1. API Description
This API (CreateCdbHour) is used to create instances with pay by usage mode, which can be used to create Cloud Database instances by passing such information as instance specification, MySQL version number, and quantity. You can create master instances, disaster recovery instances, and read-only instances via this API.
You can also use API [Query List of Instances](/doc/api/253/1266) to query the instance details.
Domain for API request: <font style='color:red'>cdb.api.qcloud.com </font>

1. Please use API [Query Supported Specifications (supporting custom availability zones and configurations)](/doc/api/253/6109) to query supported instance specifications, and use API [Query Prices (Pay by Usage)](/doc/api/253/5176) to query the supported instance prices;
2. It supports the creation of a maximum of 10 instances at one time with a maximum validity period of 36 months;
3. Instances can be created with MySQL 5.5 and MySQL 5.6;
4. Master instances, disaster recovery instances, and read-only instances can be created via this API;


## 2. Input Parameters
The following request parameter list only provides API request parameters. Common request parameters need to be added when the API is called. For more information, refer to <a href='/document/product/236/6921' title='Common Request Parameters'>Common Request Parameters</a>. The Action field for this API is CreateCdbHour.

| Parameter Name | Required  | Type | Description |
|---------|---------|---------|---------|
| cdbType | Yes | String | Instance specifications. Both fixed specification and custom specification are supported. CUSTOM means custom specification. You can use API [Query Supported Specifications](/doc/api/253/1333) to acquire the value range of fixed specification. <font style='color:red'> Fixed specification type will become unavailable in the future. It is recommended to use custom specifications. </font> |
| engineVersion | Yes | String | MySQL version; possible values include: 5.5 and 5.6. You can use API [Query Supported Specifications (supporting custom availability zones and configurations)](/doc/api/253/6109) to acquire the supported instance version number |
| goodsNum | Yes | Int | Number of instances. Default is 1, minimum is 1, and maximum is 10. You can acquire the number of instances that can be created using [Query Supported Specifications (supporting custom availability zones and configurations)](/doc/api/253/6109) API |
| vpcId | No | String | VPC ID. If left blank, the default is basic network. Please use [Query VPC List](/doc/api/245/1372) |
| subnetId | No | String | Subnet ID of an VPC. If vpcId is set, subnetId is required. Please use [Query Subnet List](/doc/api/245/1371) |
| projectId | No | Int | Project ID. If this is left empty, default project is used. Please use API [Query Project List](/document/product/378/4400) to acquire the project ID |
| memory | No | Int | Size of instance memory (in MB). This parameter is required if the value of cdbType is CUSTOM. This parameter will be ignored if the value of cdbType is an integer. You can use API [Query Supported Specifications (supporting availability zones and custom configurations)](/doc/api/253/6109) to acquire the supported memory specification |
| volume | No | Int | Size of instance disk (unit: GB). This parameter is required if the value of cdbType is CUSTOM. This parameter will be ignored if the value of cdbType is an integer. You can use API [Query Supported Specifications (supporting availability zones and custom configurations)](/doc/api/253/6109) to acquire supported disk range |
| zoneId | No | Int | Availability zone ID. By default, the system will automatically select an availability zone. You can use API [Query Supported Specifications (supporting custom availability zones and configurations)](/doc/api/253/6109) to acquire supported availability zones |
| cdbInstanceId | No | String | Instance ID, which is required when purchasing read-only instances or disaster recovery instances. This field indicates the master instance ID of read-only instances or disaster recovery instances. Please use API [Query List of Instances](/doc/api/253/1266) to query Cloud Database instance ID |
| instanceRole | No | String | Instance type. Default is master. Possible values include: master - master instance, dr - disaster recovery instance, ro - read-only instance |
| masterRegion | No | String | Region ID of master instances, which is required when purchasing disaster recovery instance. For more information, refer to [Common Request Parameters](/doc/api/229/6976) |
| port | No | Int | Custom port, value range: [1024-65535] |
| password | No | String | Password of root account, which should be a combination of 8-16 characters comprised of at least two of the following types: letters, numbers, special characters (!, @, #, $, %, ^, *, ()). You can specify this parameter when purchasing master instances, while this parameter will be ignored when purchasing read-only instances or disaster recovery instances |
| protectMode | No | Int | Data copy method. Default is 0. Possible values include: 0 - indicates asynchronous copy, 1 - indicates semi-synchronized copy, 2 - indicates strong synchronized copy. You can specify this parameter when purchasing master instances, while this parameter will be ignored when purchasing read-only instances or disaster recovery instances |
| deployMode | No | Int | Multiple availability zones. Default is 0. Possible values include: 0 - single availability zone, 1 - multiple availability zones. You can specify this parameter when purchasing master instances, while this parameter will be ignored when purchasing read-only instances or disaster recovery instances |
| slaveZoneFirst | No | Int | Availability zone ID of slave 1. Default is the value of zoneId. You can specify this parameter when purchasing master instances, while this parameter will be ignored when purchasing read-only instances or disaster recovery instances |
| slaveZoneSecond | No | Int | Availability zone ID of slave 2. Default is 0. You can specify this parameter when purchasing master instances, while this parameter will be ignored when purchasing read-only instances or disaster recovery instances |

paramlList is the parameter list of modified instances. As an array, each of its element contains name and value fields as follows (You can specify this parameter when purchasing master instances, while this parameter will be ignored when purchasing read-only instances or disaster recovery instances):

| Parameter Name | Required  | Type | Description |
|---------|---------|---------|---------|
| paramList.n.name | No | String | Parameter name to be modified |
| paramList.n.value | No | String | Parameter value to be modified |


## 3. Output Parameters
| Parameter Name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code; 0: Succeeded; other values: Failed. For more information, please refer to <a href='https://intl.cloud.tencent.com/document/product/236/1743' title='Common Error Codes'>Common Error Codes</a> on the Error Code page. |
| message | String | Module error message description depending on API. |
| codeDesc | String | Error description |
| dealIds | Array | Pay-by-usage order ID, which is used to report the order-related problems to Tencent Cloud customer service |

Parameter data is composed of the following parameters:

| Parameter Name | Type | Description |
|---------|---------|---------|
| dealIds | Array | Pay-by-usage order ID, which is used to report the order-related problems to Tencent Cloud customer service |
| cdbInstanceIds | Object | Instance ID list, with pay-by-usage order ID as the key and instance ID as the value. |


## 4. Error Codes
The following error codes only include the business logic error codes for this API.

| Error Code | Error Message | Error Description |
|---------|---------|---------|
| 9301 | InvalidParameter | Incorrect transaction parameter. Detailed error information will be returned in reality |
| 9006 | InternalError | Database internal error |
| 9003 | InvalidParameter | Incorrect parameter. Detailed error information will be returned in reality |


## 5. Example
Input
<pre>
https://cdb.api.qcloud.com/v2/index.php?Action=CreateCdbHour
&<<a href="/document/product/236/6921">Common request parameters</a>>
&engineVersion=5.6
&cdbType=custom
&goodsNum=1
&memory=360
&volume=10
&zoneId=100002
&instanceRo=master
&amp;paramList.0.name=connect_timeout
&amp;paramList.0.value=11
</pre>

Output
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "dealIds": [
        "20161123160000035194657627030673"
    ],
    "data": {
        "dealIds": [
            "20161123160000035194657627030673"
        ],
        "cdbInstanceIds": {
            "20161123160000035194657627030673": "cdb-o00n5u7k"
        }
    }
}

```

