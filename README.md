# Crie seu próprio ChatGPT e adicione em qualquer aplicação, usando a API da OpenAI 
![Open AI](https://i.ibb.co/LS4DRhb/image-257.png)


first run 

Para ter sua chave da OpenAI você deve criar a conta e criar uma chave no [link](https://platform.openai.com/account/api-keys)

Crie o arquivo .env na pasta server com a api_key:
```jsx
OPENAI_API_KEY="<sua chave>"
```
E no arquivo server.js dentro da pasta server: 

```jsx
const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
});
```


Configuração do ChatGPT, no arquivo server.js, para mais informações de configuração a OpenIA tem uma plataforma nesse [link](https://platform.openai.com/playground)

```jsx
app.post('/', async (req, res) => {
  try {
    const prompt = req.body.prompt;

    const response = await openai.createCompletion({
      model: "text-davinci-003", // modelo de IA 
      prompt: `${prompt}`,
      temperature: 0, // Higher values means the model will take more risks.
      max_tokens: 3000, // The maximum number of tokens to generate in the completion. Most models have a context length of 2048 tokens (except for the newest models, which support 4096).
      top_p: 1, // alternative to sampling with temperature, called nucleus sampling
      frequency_penalty: 0.5, // Number between -2.0 and 2.0. Positive values penalize new tokens based on their existing frequency in the text so far, decreasing the model's likelihood to repeat the same line verbatim.
      presence_penalty: 0, // Number between -2.0 and 2.0. Positive values penalize new tokens based on whether they appear in the text so far, increasing the model's likelihood to talk about new topics.
    });

    res.status(200).send({
      bot: response.data.choices[0].text
    });

  } catch (error) {
    console.error(error)
    res.status(500).send(error || 'Something went wrong');
  }
})
```


# npm create vite@lastest client --template vanilla
# Rodando 
Abra dois terminais um na pasta client e outro na pasta server
Em client rode o código:

```shell
npm run server
```
e em server o código:

```shell
npm run dev
```
