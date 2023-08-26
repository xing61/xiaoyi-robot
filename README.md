# 优质稳定的OpenAI的API接口-For开发者

#### 介绍
为开发者提供优质稳定的OpenAI相关的API调用接口。  
智增增-大模型的API接口服务商，提供ChatGPT的API调用，支持openai的API接口，支持：gpt-4，gpt-3.5。      
要买openai的账号？  
要科学上网？  
要美元的银行卡？  
通通不用的，直接调用就行，简单粗暴，关键稳定，超级好用！！  
openai的国内代理，国内接口请求转发，api proxy  
各种示例代码：https://github.com/xing61/xiaoyi-robot/tree/main/%E7%A4%BA%E4%BE%8B%E4%BB%A3%E7%A0%81    

- **项目主要优势**  
  * 不限制使用，可以用微信充值，没有封号风险。
  * 不用买openai的账号，不用美元的银行卡。 
  * 无需代理即可访问，没有x的阻拦。  
  * 支持GPT4，并且没有每3小时25条消息的限制。  
  * 兼容OpenAI接口格式，可以做到平替。支持vscode插件，支持autoGPT，agentGPT。API用法也可参考官方文档  
  * 新增对Embeddings支持，可以用接口运行AutoGPT等应用。
  * 新增对stream模式的支持，可以支持原生的各种应用
  * 支持文字生成图片
  * 更多特性支持，敬请期待。也可直接向我们提交需求哦

- **项目地址**   
1、项目官方网址：http://gpt.zhizengzeng.com/, 智增增-大模型的API接口服务商
2、移动端查看数据，微信公众号：小一机器人，开发者单独的Secret Key、余额查询、示例代码等请从微信公众号“小一机器人”，点击菜单“Chat的API”查看。           
 ![小一机器人-公众号二维码-small](https://github.com/xing61/xiaoyi-robot/assets/38256442/c3a00169-d51b-48f7-b969-2303e9916886)  
3、微信交流群（如果你也对本项目感兴趣，欢迎加入群聊参与讨论交流）：    
![微信截图_20230723120823](https://github.com/xing61/xiaoyi-robot/assets/38256442/2d2ad0af-a3ba-4d7f-9ddb-ef0204efc0ac)  
4、QQ群（彩蛋：群里有qq机器人：小一机器人，@他即可像访问chatgpt一样）  
![qq群-微信截图_20230723120926](https://github.com/xing61/xiaoyi-robot/assets/38256442/7805499d-e0e5-41fb-b5a3-a90237b76730)  
- **注意事项**   
注意事项！！ 
``` 
现在主要发现是有2个问题，  
1、要加一个请求头，api接口文档中有说明：
curl -H "Content-Type: application/json" -H "Authorization: Bearer $api_secret_key" -XPOST http://flag.smarttrot.com/index.php/api/v1/chat/completions -d '{"messages": [{"role":"user","content":"请介绍一下你自己"}]}'  | iconv -f utf-8 -t utf-8  
2、messages传的不对，messages是array  
```
注：<br>
1、以下所有接口的base_url: http://flag.smarttrot.com/index.php/api/   
2、API通过HTTP请求调用。每次请求，需要在HTTP头中携带用户的api_secret_key，用于认证。 开发者单独的api_secret_key，请从微信公众号“小一机器人”，点击菜单“Chat的API”获得。 
请求头形如：  
```
Content-Type: application/json
Authorization: Bearer $api_secret_key
```
- **典型用法**    
典型用法：<br>
1、设置OPENAI_API_KEY环境变量为：小一后台获取的api_secret_key，替换官方的API_KEY: sk-****** <br>
2、设置OPENAI_API_BASE_URL环境变量为：http://flag.smarttrot.com/index.php/api/v1,  替换官方的域名:  https://api.openai.com/v1 <br>
![官方库支持示例](https://github.com/xing61/xiaoyi-robot/assets/38256442/97326d94-9297-4edb-9c06-df658d10e356)

- **场景示例**    
更多场景陆续演示：<br>
![微信截图_20230823152755](https://github.com/xing61/xiaoyi-robot/assets/38256442/490f592d-85ba-42ff-bf85-801d6c459c9c)


## API文档 ##
#### 1、创建chat

调用本接口，发起一次对话请求

- **请求URL**
> [v1/chat/completions](#)

- **请求方式** 
>**POST**

- **Header参数**
>
| 名称      |     值 | 参数说明   |
| :-------- | :--------| :------ |
| Content-Type| application/json| | 
| Authorization| Bearer $api_secret_key| 开发者单独的api_secret_key，请从微信公众号“小一机器人”，点击菜单“Chat的API”获得。推荐在header中设置此字段 | 

- **请求参数**
>
| 请求参数      |     参数类型 |   是否必须   |参数说明   |
| :-------- | :--------| :------ | :------ |
| model| string| 否| 大模型的类别，目前支持：gpt-4, gpt-4-0613, gpt-4-32k, gpt-4-32k-0613, gpt-3.5-turbo, gpt-3.5-turbo-0613, gpt-3.5-turbo-16k, gpt-3.5-turbo-16k-0613。默认gpt-3.5-turbo|
| messages| List(message)| 是| 聊天上下文信息。说明:<br>（1）messages成员不能为空，1个成员表示单轮对话，多个成员表示多轮对话。<br>（2）最后一个message为当前请求的信息，前面的message为历史对话信息。<br>（3）必须为奇数个成员，成员中message的role必须依次为user、assistant。<br>（4）最后一个message的content长度（即此轮对话的问题）不能超过2000个字符；如果messages中content总长度大于2000字符，系统会依次遗忘最早的历史会话，直到content的总长度不超过2000个字符。  |
| stream| bool| 否| 是否以流式接口的形式返回数据，默认false。|
| user| string| 否| 表示最终用户的唯一标识符，可以监视和检测滥用行为，防止接口恶意调用。|

其它高级参数：
>    
| 请求参数      |     参数类型 |   是否必须   |参数说明   |  
| :-------- | :--------| :------ | :------ |  
| api_secret_key| string| 否| 兼容老版接口，api_secret_key在header和此字段二者传其一即可。<br>注意：此字段将在后续版本中逐渐废弃
| temperature| number| 否| What sampling temperature to use, between 0 and 2. Higher values like 0.8 will make the output more random, while lower values like 0.2 will make it more focused and deterministic.We generally recommend altering this or top_p but not both.，默认：1。|  
| top_p| number| 否| An alternative to sampling with temperature, called nucleus sampling, where the model considers the results of the tokens with top_p probability mass. So 0.1 means only the tokens comprising the top 10% probability mass are considered.We generally recommend altering this or temperature but not both.，默认：1。|  
| n| number| 否| How many chat completion choices to generate for each input message. 默认:1。|  
| stop| string| 否| Up to 4 sequences where the API will stop generating further tokens.，默认null。|
| max_tokens| number| 否| The maximum number of tokens to generate in the chat completion.The total length of input tokens and generated tokens is limited by the model's context length. Example Python code for counting tokens.默认: 不限制。|
| presence_penalty| number| 否| Number between -2.0 and 2.0. Positive values penalize new tokens based on whether they appear in the text so far, increasing the model's likelihood to talk about new topics.，默认:0。|
| frequency_penalty| number| 否| Number between -2.0 and 2.0. Positive values penalize new tokens based on their existing frequency in the text so far, decreasing the model's likelihood to repeat the same line verbatim.，默认：0。|
| logit_bias| map| 否| Modify the likelihood of specified tokens appearing in the completion.Accepts a json object that maps tokens (specified by their token ID in the tokenizer) to an associated bias value from -100 to 100. Mathematically, the bias is added to the logits generated by the model prior to sampling. The exact effect will vary per model, but values between -1 and 1 should decrease or increase likelihood of selection; values like -100 or 100 should result in a ban or exclusive selection of the relevant token.，默认:null。|

- **message说明**
>
| 名称      |     类型 |   描述   |
| :-------- | :--------| :------ |
| role|   string|  The role of the messages author. One of system, user, assistant, or function.<br> user: 表示用户<br>assistant: 表示对话助手<br>function：表示函数调用<br>|
| content|   string|  对话内容，不能为空。|

- **返回参数**
>
| 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| code|   int|  执行结果code，0表示成功，其它表示失败，失败信息见msg字段|
| msg|   String|  执行结果消息|
| id| string| 本轮对话的id。|
| created| int| 时间戳。|
| choices| List(choice)| 对话返回结果。|
| usage| usage| token统计信息，token数 = 汉字数+单词数*1.3 （仅为估算逻辑）。|

- **choice说明**
>
| 名称      |     类型 |   描述   |
| :-------- | :--------| :------ |
| message|   message|  见上文message说明。|
| index|   int|  当前choice的序号。|
| finish_reason|   string|  结束原因。|

- **usage说明**
>
| 名称      |     类型 |   描述   |
| :-------- | :--------| :------ |
| prompt_tokens|   int|  问题tokens数。|
| completion_tokens|   int|  回答tokens数。|
| total_tokens|   int|  tokens总数。|

- **请求示例**
>    
更多示例见本页：https://github.com/xing61/xiaoyi-robot/tree/main/%E7%A4%BA%E4%BE%8B%E4%BB%A3%E7%A0%81   
```
curl -H "Content-Type: application/json" 
     -H "Authorization: Bearer $api_secret_key" 
     -XPOST http://flag.smarttrot.com/index.php/api/v1/chat/completions -d '{
  "messages": [
    {"role":"user","content":"请介绍一下你自己"},
    {"role":"assistant","content":"您好，我是小一机器人。我能够与人对话互动，回答问题，协助创作，高效便捷地帮助人们获取信息、知识和灵感。"},
    {"role":"user","content": "1+100="}
  ]
}'  | iconv -f utf-8 -t utf-8
```
```
php示例代码：  
// 设置请求头
$api_secret_key = 'xxxxxxxxxxxxxxxxxx'; // 你的api_secret_key
$headers = array(
    "Content-Type: application/json",
    "Authorization: Bearer ".$api_secret_key
);
// 设置请求参数
$params = array();
$params['user'] = '张三';
{
    $one = ["role" => 'user', "content" => "1+100="];
    $messages = array(); $messages[] = $one;
    $params['messages'] = $messages;
}
// 调用请求
$cburl = 'http://flag.smarttrot.com/index.php/api/v1/chat/completions';
$chatgpt_resp = Tool::_request('post', $cburl, $params, $headers);
$data = json_decode($chatgpt_resp, true);
```
```
python使用官方库示例代码：
import os
import openai

openai.api_key = "您的api_secret_key"
openai.api_base = "http://flag.smarttrot.com/index.php/api/v1"

chat_completion = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[{ "role": "user", "content": "Hello world" }]
)
print(chat_completion.choices[0].message.content) 
```
```
python示例代码：
import os
import requests
import time
import json

def chat_completions():
    url="http://flag.smarttrot.com/index.php/api/v1/chat/completions"
    api_secret_key = 'xxxxxxxxx';  # 你的api_secret_key
    headers = {'Content-Type': 'application/json', 'Accept':'application/json',
               'Authorization': "Bearer "+api_secret_key}
    params = {'user':'张三',
              'messages':[{'role':'user', 'content':'1+100='}]};
    r = requests.post(url, json.dumps(params), headers=headers)
    print(r.json())

if __name__ == '__main__':
    chat_completions();
```
- **返回示例**
>    
```
{
  "code": 0,
  "msg": "",
  "id": "as-bcmt5ct4iy",
  "created": 1680167072,
  "choices":[{"message":{"role":"assistant","content":"1+100=101"},"finish_reason":"stop","index":0}],
  "usage": {
    "prompt_tokens": 470,
    "completion_tokens": 198,
    "total_tokens": 668
  }
}
```
#### 2、Completions

Given a prompt, the model will return one or more predicted completions, and can also return the probabilities of alternative tokens at each position.

#### 2.1、Create completion
Creates a completion for the provided prompt and parameters.

- **请求URL**
> [v1/completions](#)

- **请求方式** 
>**POST**

- **Header参数**
>
| 名称      |     值 | 
| :-------- | :--------|
| Content-Type| application/json|  
| Authorization| Bearer $api_secret_key|  

- **请求参数**
>
| 请求参数      |     参数类型 |   是否必须   |参数说明   |
| :-------- | :--------| :------ | :------ |
| model| string| 是| ID of the model to use. You can use the List models API to see all of your available models, <br>or see our Model overview for descriptions of them.|
| prompt| string or array| 否| The prompt(s) to generate completions for, encoded as a string, array of strings,<br> array of tokens, or array of token arrays.<br>Note that <|endoftext|> is the document separator that the model sees during training, <br>so if a prompt is not specified the model will generate as if from the beginning of a new document. <br>Defaults to <|endoftext|>|
| suffix| string | 否| The suffix that comes after a completion of inserted text.Defaults to null|
| max_tokens| int| 否| The maximum number of tokens to generate in the completion.<br>The token count of your prompt plus max_tokens cannot exceed the model's context length. <br>Example Python code for counting tokens.Defaults to 16|
| temperature| number| 否| What sampling temperature to use, between 0 and 2. <br>Higher values like 0.8 will make the output more random, while lower values like 0.2 will make it more focused and deterministic.<br>We generally recommend altering this or top_p but not both.Defaults to 1|
| top_p| number| 否| An alternative to sampling with temperature, called nucleus sampling, <br>where the model considers the results of the tokens with top_p probability mass. <br>So 0.1 means only the tokens comprising the top 10% probability mass are considered.<br>We generally recommend altering this or temperature but not both.Defaults to 1|
| n| number| 否| How many completions to generate for each prompt.<br>Note: Because this parameter generates many completions, <br>it can quickly consume your token quota. Use carefully and ensure that you have reasonable settings for max_tokens and stop.Defaults to 1|
| stream| bool| 否| Whether to stream back partial progress. <br>If set, tokens will be sent as data-only server-sent events as they become available, <br>with the stream terminated by a data: [DONE] message. Example Python code.Defaults to false|
| logprobs| int| 否| Include the log probabilities on the logprobs most likely tokens, <br>as well the chosen tokens. For example, if logprobs is 5, the API will return a list of the 5 most likely tokens. <br>The API will always return the logprob of the sampled token, so there may be up to logprobs+1 elements in the response.<br>The maximum value for logprobs is 5. If you need more than this, <br>please contact us through our Help center and describe your use case.Defaults to null|
| echo| bool| 否| Echo back the prompt in addition to the completion。Defaults to false|
| stop| int| 是| Up to 4 sequences where the API will stop generating further tokens. <br>The returned text will not contain the stop sequence.Defaults to null  |Number between -2.0 and 2.0. <br>Positive values penalize new tokens based on whether they appear in the text so far, increasing the model's likelihood to talk about new topics.<br>See more information about frequency and presence penalties.Defaults to 0|
| presence_penalty| int| 否| Number between -2.0 and 2.0. Positive values penalize new tokens <br>based on whether they appear in the text so far, <br>increasing the model's likelihood to talk about new topics.<br>See more information about frequency and presence penalties.Defaults to 0|
| frequency_penalty| int| 否| Number between -2.0 and 2.0. <br>Positive values penalize new tokens based on their existing frequency in the text so far,<br> decreasing the model's likelihood to repeat the same line verbatim.<br>See more information about frequency and presence penalties.Defaults to 0|
| best_of| int| 否| Generates best_of completions server-side and returns the "best" (the one with the highest log probability per token). <br>Results cannot be streamed.<br>When used with n, best_of controls the number of candidate completions and n specifies how many to return – <br>best_of must be greater than n.<br>Note: Because this parameter generates many completions, it can quickly consume your token quota. <br>Use carefully and ensure that you have reasonable settings for max_tokens and stop.Defaults to 1|
| logit_bias| map| 否| Modify the likelihood of specified tokens appearing in the completion.<br>Accepts a json object that maps tokens (specified by their token ID in the GPT tokenizer) to an associated bias value from -100 to 100.<br> You can use this tokenizer tool (which works for both GPT-2 and GPT-3) to convert text to token IDs.<br> Mathematically, the bias is added to the logits generated by the model prior to sampling. The exact effect will vary per model, <br>but values between -1 and 1 should decrease or increase likelihood of <br>selection; values like -100 or 100 should result in a ban or exclusive selection of the relevant token.<br>As an example, you can pass {"50256": -100} to prevent the <|endoftext|> <br>token from being generated.Defaults to null|
| user| string| 否| 表示最终用户的唯一标识符，可以监视和检测滥用行为，防止接口恶意调用。|

- **返回参数**
>
| 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| code|   int|  执行结果code|
| msg|   String|  执行结果消息|
| id| string| 本轮对话的id。|
| object| string| text_completion|
| created| int| 时间戳。|
| model| string| 本次调用的模型|
| choices| List(choice)| 对话返回结果。|
| usage| usage| token统计信息，token数 = 汉字数+单词数*1.3 （仅为估算逻辑）。|

- **choice说明**
>
| 名称      |     类型 |   描述   |
| :-------- | :--------| :------ |
| text|   string|  返回的文本|
| index|   int|  当前choice的序号。|
| logprobs|   int|  当前choice的logprobs。|
| finish_reason|   string|  结束原因。|

- **usage说明**
>
| 名称      |     类型 |   描述   |
| :-------- | :--------| :------ |
| prompt_tokens|   int|  问题tokens数。|
| completion_tokens|   int|  回答tokens数。|
| total_tokens|   int|  tokens总数。|

- **请求示例**
>    
```
curl -H "Content-Type: application/json" -H "Authorization: Bearer $api_secret_key" -XPOST xxxxx/v1/chat/completions -d '{
  "messages": [
    {"role":"user","content":"请介绍一下你自己"}
  ]
}'  | iconv -f utf-8 -t utf-8
```

- **返回示例**
>    
```
{
  "code": 0,
  "msg": "",
  "id": "cmpl-uqkvlQyYK7bGYrRHQ0eXlWi7",
  "object": "text_completion",
  "created": 1589478378,
  "model": "text-davinci-003",
  "choices": [
    {
      "text": "\n\nThis is indeed a test",
      "index": 0,
      "logprobs": null,
      "finish_reason": "length"
    }
  ],
  "usage": {
    "prompt_tokens": 5,
    "completion_tokens": 7,
    "total_tokens": 12
  }
}
```

#### 3、图片-创建图片

Given a prompt and/or an input image, the model will generate a new image. 

- **请求URL**
> [v1/images/generations](#)

- **请求方式** 
>**POST**

- **Header参数**
>
| 名称      |     值 | 
| :-------- | :--------|
| Content-Type| application/json| 
| Authorization| Bearer $api_secret_key|  

- **请求参数**
>
| 请求参数      |     参数类型 |   是否必须   |参数说明   |
| :-------- | :--------| :------ | :------ |
| prompt| string| 是| A text description of the desired image(s). The maximum length is 1000 characters.  |
| n| int| 否| The number of images to generate. Must be between 1 and 10. Defaults to 1|
| size| string| 否| The size of the generated images. Must be one of 256x256, 512x512, or 1024x1024. Defaults to 1024x1024|
| response_format| string| 否| The format in which the generated images are returned. Must be one of url or b64_json. Defaults to url|
| user| string| 否| 表示最终用户的唯一标识符，可以监视和检测滥用行为，防止接口恶意调用。|

- **返回参数**
>
| 返回参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| code|   int|  执行结果code|
| msg|   String|  执行结果消息|
| created| int| 时间戳。|
| data| List(img)| 对话返回结果。|

- **img说明**
>
| 名称      |     类型 |   描述   |
| :-------- | :--------| :------ |
| url|   string|  当前图片的地址url|

- **请求示例**
>    
```
curl -H "Content-Type: application/json" -H "Authorization: Bearer $api_secret_key" -XPOST xxxxx/v1/images/generations -d '{
  "prompt": "A cute baby sea otter",
}'  | iconv -f utf-8 -t utf-8
```

- **返回示例**
>    
```
{
  "code": 0,
  "msg": "",
  "created": 1680167072,
  "data": [
    {
      "url": "https://..."
    },
    {
      "url": "https://..."
    }
  ]
}
```

#### 4、Embeddings

Get a vector representation of a given input that can be easily consumed by machine learning models and algorithms.
Related guide: Embeddings

#### 4.1、Create embeddings
Creates an embedding vector representing the input text.

- **请求URL**
> [v1/embeddings](#)

- **请求方式** 
>**POST**

- **Header参数**
>
| 名称      |     值 | 
| :-------- | :--------|
| Content-Type| application/json| 
| Authorization| Bearer $api_secret_key|  

- **请求参数**
>
| 请求参数      |     参数类型 |   是否必须   |参数说明   |
| :-------- | :--------| :------ | :------ |   
| model| string| 是| ID of the model to use. You can use the List models API to see all of your available models, or see our Model overview for descriptions of them. 默认：text-embedding-ada-002（官方推荐） |  
| input| string| 是| Input text to embed, encoded as a string or array of tokens. To embed multiple inputs in a single request, pass an array of strings or array of token arrays. Each input must not exceed the max input tokens for the model (8191 tokens for text-embedding-ada-002). Example Python code for counting tokens.|  
| user| string| 否| A unique identifier representing your end-user, which can help OpenAI to monitor and detect abuse. |

- **请求示例**
>    
```
curl -H "Content-Type: application/json" -H "Authorization: Bearer $api_secret_key" -XPOST xxxxx/v1/embeddings -d '{
  "input": "The food was delicious and the waiter...",
    "model": "text-embedding-ada-002"
}'  | iconv -f utf-8 -t utf-8
```

- **返回示例**
>    
```
{
"code": 0,
  "msg": "",
  "object": "list",
  "data": [
    {
      "object": "embedding",
      "embedding": [
        0.0023064255,
        -0.009327292,
        .... (1536 floats total for ada-002)
        -0.0028842222,
      ],
      "index": 0
    }
  ],
  "model": "text-embedding-ada-002",
  "usage": {
    "prompt_tokens": 8,
    "total_tokens": 8
  }
}

```
