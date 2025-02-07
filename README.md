# OpenAI API client library for Rust
unofficial

## Installation:
Cargo.toml
```toml
[dependencies]
openai-api-rs = "0.1.5"
```

## Example:
```bash
export OPENAI_API_KEY={YOUR_API_KEY}
```

### Chat
```rust
use openai_api_rs::v1::api::Client;
use openai_api_rs::v1::chat_completion::{self, ChatCompletionRequest};
use std::env;

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    let client = Client::new(env::var("OPENAI_API_KEY").unwrap().to_string());
    let req = ChatCompletionRequest {
        model: chat_completion::GPT4.to_string(),
        messages: vec![chat_completion::ChatCompletionMessage {
            role: chat_completion::MessageRole::user,
            content: String::from("NFTとは？"),
        }],
    };
    let result = client.chat_completion(req).await?;
    println!("{:?}", result.choices[0].message.content);

    Ok(())
}
```

### Completion
```rust
use openai_api_rs::v1::completion::{self, CompletionRequest};
use openai_api_rs::v1::api::Client;
use std::env;

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    let client = Client::new(env::var("OPENAI_API_KEY").unwrap().to_string());
    let req = CompletionRequest {
        model: completion::GPT3_TEXT_DAVINCI_003.to_string(),
        prompt: Some(String::from("NFTとは？")),
        suffix: None,
        max_tokens: Some(3000),
        temperature: Some(0.9),
        top_p: Some(1.0),
        n: None,
        stream: None,
        logprobs: None,
        echo: None,
        stop: None,
        presence_penalty: Some(0.6),
        frequency_penalty: Some(0.0),
        best_of: None,
        logit_bias: None,
        user: None,
      };
    let result = client.completion(req).await?;
    println!("{:?}", result.choices[0].text);

    Ok(())
}
```
