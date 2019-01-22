<h1 align="center"> weather </h1>

基于[高德开放平台](https://lbs.amap.com)的PHP天气信息组件


## 安装

```shell
$ composer require cherrybeal/weather -vvv
```

## 配置

在使用本扩展之前，你需要去 [高德开放平台](https://lbs.amap.com/dev/id/newUser) 注册账号，然后创建应用，获取应用的 API Key。

## 使用

```php
use Cherrybeal\Weather\Weather;

$key = 'xxxxxxxx';
$weather = new Weather($key);
```

### 获取实时天气

```php
$response = $weather->getWeather('长沙');
```

示例：

```json
{
    "status": "1",
    "count": "2",
    "info": "OK",
    "infocode": "10000",
    "lives": [
        {
            "province": "湖南",
            "city": "长沙市",
            "adcode": "430100",
            "weather": "晴",
            "temperature": "7",
            "winddirection": "西北",
            "windpower": "≤3",
            "humidity": "65",
            "reporttime": "2019-01-22 21:17:37"
        },
        {
            "province": "湖南",
            "city": "长沙县",
            "adcode": "430121",
            "weather": "晴",
            "temperature": "7",
            "winddirection": "西北",
            "windpower": "≤3",
            "humidity": "65",
            "reporttime": "2019-01-22 21:17:38"
        }
    ]
}
```

### 获取近期天气预报

```php
$response = $weather->getWeather('长沙', 'all');
```

示例：

```json
{
    "status": "1",
    "count": "2",
    "info": "OK",
    "infocode": "10000",
    "forecasts": [
        {
            "city": "长沙市",
            "adcode": "430100",
            "province": "湖南",
            "reporttime": "2019-01-22 21:17:38",
            "casts": [
                {
                    "date": "2019-01-22",
                    "week": "2",
                    "dayweather": "晴",
                    "nightweather": "晴",
                    "daytemp": "14",
                    "nighttemp": "3",
                    "daywind": "东南",
                    "nightwind": "东南",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                },
                {
                    "date": "2019-01-23",
                    "week": "3",
                    "dayweather": "晴",
                    "nightweather": "晴",
                    "daytemp": "15",
                    "nighttemp": "3",
                    "daywind": "东",
                    "nightwind": "东",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                },
                {
                    "date": "2019-01-24",
                    "week": "4",
                    "dayweather": "多云",
                    "nightweather": "多云",
                    "daytemp": "16",
                    "nighttemp": "4",
                    "daywind": "北",
                    "nightwind": "北",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                },
                {
                    "date": "2019-01-25",
                    "week": "5",
                    "dayweather": "多云",
                    "nightweather": "多云",
                    "daytemp": "12",
                    "nighttemp": "6",
                    "daywind": "北",
                    "nightwind": "北",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                }
            ]
        },
        {
            "city": "长沙县",
            "adcode": "430121",
            "province": "湖南",
            "reporttime": "2019-01-22 21:17:38",
            "casts": [
                {
                    "date": "2019-01-22",
                    "week": "2",
                    "dayweather": "晴",
                    "nightweather": "晴",
                    "daytemp": "13",
                    "nighttemp": "3",
                    "daywind": "东南",
                    "nightwind": "东南",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                },
                {
                    "date": "2019-01-23",
                    "week": "3",
                    "dayweather": "晴",
                    "nightweather": "晴",
                    "daytemp": "15",
                    "nighttemp": "3",
                    "daywind": "东",
                    "nightwind": "东",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                },
                {
                    "date": "2019-01-24",
                    "week": "4",
                    "dayweather": "多云",
                    "nightweather": "多云",
                    "daytemp": "16",
                    "nighttemp": "4",
                    "daywind": "北",
                    "nightwind": "北",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                },
                {
                    "date": "2019-01-25",
                    "week": "5",
                    "dayweather": "多云",
                    "nightweather": "多云",
                    "daytemp": "12",
                    "nighttemp": "6",
                    "daywind": "北",
                    "nightwind": "北",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                }
            ]
        }
    ]
}
```

### 获取 XML 格式返回值

第三个参数为返回值类型，可选 `json` 与 `xml`, 默认 `json`:

```php
$response = $weather->getWeather('长沙', 'base', 'xml');
```

示例：

```xml
<response>
    <status>1</status>
    <count>1</count>
    <info>OK</info>
    <infocode>10000</infocode>
    <lives type="list">
        <live>
            <province>广东</province>
            <city>深圳市</city>
            <adcode>440300</adcode>
            <weather>中雨</weather>
            <temperature>27</temperature>
            <winddirection>西南</winddirection>
            <windpower>5</windpower>
            <humidity>94</humidity>
            <reporttime>2018-08-21 16:00:00</reporttime>
        </live>
    </lives>
</response>
```

### 参数说明

```
array | string getWeather(string $city, string $type = 'base', string $format = 'json')
```

> - $city - 城市名，比如："长沙" 
> - $format - 输出的格式类型，默认为 json 格式，当 output 为 "`xml`" 时，输出为 xml 格式的数据

### 在 Laravel 中使用

在 Laravel 中使用也是同样的安装方式，配置写在 `config/services.php` 中

```php
'weather' => [
        'key' => env('WEATHER_API_KEY'),
    ],
```

然后在 `.env` 中配置 `WEATHER_API_KEY`:

```env
WEATHER_API_KEY=xxxxxxxxxxxxxxxxxxxxx
```

可以用两种方式来获取 `Cherrybeal\Weather\Weather` 实例：

#### 方法参数注入

```php
public function edit(Weather $weather) 
{
    $response = $weather->getLiveWeather('深圳');
}
```

#### 服务名访问

```php
public function edit() 
{
    $response = app('weather')->getLiveWeather('深圳');
}
```

## 参考

- [高德开放平台天气接口](https://lbs.amap.com/api/webservice/guide/api/weatherinfo/)

## License

MIT
