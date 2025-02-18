---
_build:
  publishResources: false
  render: never
  list: never
---

`https://gateway.ai.cloudflare.com/v1/{account_id}/{gateway_slug}/openai`

When making requests to OpenAI, replace `https://api.openai.com/v1` in the URL you’re currently using with `https://gateway.ai.cloudflare.com/v1/{account_id}/{gateway_slug}/openai`.


```bash
---
header: Request
---

curl https://gateway.ai.cloudflare.com/v1/{account_id}/{gateway_slug}/openai/chat/completions \
  --header 'Authorization: Bearer {openai_token}' \
  --header 'Content-Type: application/json' \
  --data ' {
   		 "model": "gpt-3.5-turbo",
   		 "messages": [
        {
          "role": "user",
          "content": "What is Cloudflare"
        }
   		 ]
   	 }
'
```


If you’re using a library like openai-node, set the `baseURL` to your OpenAI endpoint like this:

```javascript
---
filename: index.js
---
import OpenAI from 'openai';

const openai = new OpenAI({
	apiKey: 'my api key', // defaults to process.env["OPENAI_API_KEY"]
	baseURL: "https://gateway.ai.cloudflare.com/v1/{account_id}/{gateway_slug}/openai"
});

try {
  const chatCompletion = await openai.chat.completions.create({
    model: "gpt-3.5-turbo-0613",
    messages: [{ role: "user", content: "What is a neuron?" }],
    max_tokens: 100,
  });

  const response = chatCompletion.choices[0].message;

  return new Response(JSON.stringify(response));
} catch (e) {
  return new Response(e);
}

```