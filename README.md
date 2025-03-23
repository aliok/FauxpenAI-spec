# FauxpenAI Spec

This repository contains recorded API calls to OpenAI's Chat Completions and Embeddings endpoints.
The goal is to provide a dataset that can be used to verify whether other API servers claiming
OpenAI compatibility are actually conformant.

## Project Purpose

Many API servers advertise OpenAI compatibility, but their actual behavior may differ in subtle or
significant ways. By using this dataset, you can:

- Compare responses from alternative API implementations to OpenAI's actual responses.
- Identify discrepancies in behavior, response structure, and token usage.
- Validate whether an API server meets conformance expectations.

For a fake but conformant OpenAI API server, see [FauxpenAI](https://github.com/aliok/FauxpenAI) project.

## How the Data is Recorded

The data in this repository is recorded using the
[FauxpenAI Conformance](https://github.com/aliok/FauxpenAI-conformance) tool. This tool makes calls to
OpenAI's API and captures both the request and response for future analysis.

### Recording Process

1. The [`FauxpenAI Conformance`](https://github.com/aliok/FauxpenAI-conformance) tool is configured with an OpenAI API
   key.
2. It sends requests to the OpenAI API for chat completions and embeddings.
3. The tool logs both the request payload and the API's response.
4. The recorded data is stored in JSON format in this repository.
    - The recorded data includes:
        - Request parameters
        - Response data
        - Metadata such as timestamps and request IDs
    - The data is stored in a separate file for each API type:
        - [`chatcompletions/results.json.gz`](chatcompletions/results.json.gz)
        - [`embeddings/results.json.gz`](embeddings/results.json.gz)
    - Since the responses can be large and there are many requests, the files are compressed using gzip.

## Using the Data

You can use this dataset to test any API server that claims OpenAI compatibility by replaying the requests and
comparing the results.

See [FauxpenAI Conformance](https://github.com/aliok/FauxpenAI-conformance) for more details on how to set up the tool
and run the tests.

The data is structured in a way that allows you to easily identify the parameters used in each request and the
corresponding
response.

Some stats:

```text
Chat Completions:
- Total scenarios: 2768

Embeddings:
- Total scenarios: 52
```

A sample scenario looks like this:

```json
{
   "0051684de3d5135274d9e8cb3946338962c21b9451949d04f86b5449a2df19c3": {
      "key": "0051684de3d5135274d9e8cb3946338962c21b9451949d04f86b5449a2df19c3",
      "spec": {
         "name": "n=1+seed=-1",
         "factors": [
            {
               "negative": false,
               "primary": false,
               "name": "seed=-1",
               "key": "44e9ec9f7bc72631cf5465761bab1a349bae8c85dfc5e2e6f1e0af605895984e",
               "val": -1
            },
            {
               "negative": false,
               "primary": false,
               "name": "model=gpt-4",
               "key": "5287055d0a0418e8937ef7f8942657dd25100462c8e99e612d428e4117ad76b6",
               "val": "gpt-4"
            },
            {
               "negative": false,
               "primary": true,
               "name": "n=1",
               "key": "a269f7e0d4a254365349105ee199a0ce49a424c9e6d1af17b2a25d32258c6ad5",
               "val": 1
            },
            {
               "negative": false,
               "primary": true,
               "name": "ONLY_SYSTEM_AND_USER_MESSAGE",
               "key": "c2b7a8cd0f6ba6ff970c257405323312569605c39e437da06d2c8171d6e6e2fb",
               "messages": [
                  {
                     "parts": "You are a helpful assistant."
                  },
                  {
                     "parts": "Hello"
                  }
               ]
            }
         ],
         "key": "0051684de3d5135274d9e8cb3946338962c21b9451949d04f86b5449a2df19c3",
         "group": "pairwise"
      },
      "requestBody": {
         "seed": -1,
         "model": "gpt-4",
         "n": 1,
         "messages": [
            {
               "role": "system",
               "content": "You are a helpful assistant."
            },
            {
               "role": "user",
               "content": "Hello"
            }
         ]
      }
   }
}
```

A sample response looks like this (for this scenario):

```json
{
   "0051684de3d5135274d9e8cb3946338962c21b9451949d04f86b5449a2df19c3": {
      "key": "0051684de3d5135274d9e8cb3946338962c21b9451949d04f86b5449a2df19c3",
      "scenario": {
         "key": "0051684de3d5135274d9e8cb3946338962c21b9451949d04f86b5449a2df19c3",
         "spec": {
            "name": "n=1+seed=-1",
            "factors": [
               {
                  "negative": false,
                  "primary": false,
                  "name": "seed=-1",
                  "key": "44e9ec9f7bc72631cf5465761bab1a349bae8c85dfc5e2e6f1e0af605895984e",
                  "val": -1
               },
               {
                  "negative": false,
                  "primary": false,
                  "name": "model=gpt-4",
                  "key": "5287055d0a0418e8937ef7f8942657dd25100462c8e99e612d428e4117ad76b6",
                  "val": "gpt-4"
               },
               {
                  "negative": false,
                  "primary": true,
                  "name": "n=1",
                  "key": "a269f7e0d4a254365349105ee199a0ce49a424c9e6d1af17b2a25d32258c6ad5",
                  "val": 1
               },
               {
                  "negative": false,
                  "primary": true,
                  "name": "ONLY_SYSTEM_AND_USER_MESSAGE",
                  "key": "c2b7a8cd0f6ba6ff970c257405323312569605c39e437da06d2c8171d6e6e2fb",
                  "messages": [
                     {
                        "parts": "You are a helpful assistant."
                     },
                     {
                        "parts": "Hello"
                     }
                  ]
               }
            ],
            "key": "0051684de3d5135274d9e8cb3946338962c21b9451949d04f86b5449a2df19c3",
            "group": "pairwise"
         },
         "requestBody": {
            "seed": -1,
            "model": "gpt-4",
            "n": 1,
            "messages": [
               {
                  "role": "system",
                  "content": "You are a helpful assistant."
               },
               {
                  "role": "user",
                  "content": "Hello"
               }
            ]
         }
      },
      "response": {
         "status": 200,
         "headers": {
            "access-control-expose-headers": "X-Request-ID",
            "alt-svc": "h3=\":443\"; ma=86400",
            "cf-cache-status": "DYNAMIC",
            "cf-ray": "9******************T",
            "connection": "keep-alive",
            "content-encoding": "br",
            "content-type": "application/json",
            "date": "S***************************T",
            "openai-organization": "a**********b",
            "openai-processing-ms": "407",
            "openai-version": "2020-10-01",
            "server": "cloudflare",
            "set-cookie": "_**************************************************************************************************************************************************e",
            "strict-transport-security": "max-age=31536000; includeSubDomains; preload",
            "transfer-encoding": "chunked",
            "x-content-type-options": "nosniff",
            "x-ratelimit-limit-requests": "10000",
            "x-ratelimit-limit-tokens": "10000",
            "x-ratelimit-remaining-requests": "8030",
            "x-ratelimit-remaining-tokens": "9988",
            "x-ratelimit-reset-requests": "4h43m36.314s",
            "x-ratelimit-reset-tokens": "72ms",
            "x-request-id": "r**********************************f"
         },
         "body": {
            "id": "c************************************a",
            "object": "chat.completion",
            "created": 1234567890,
            "model": "gpt-4-0613",
            "choices": [
               {
                  "index": 0,
                  "message": {
                     "role": "assistant",
                     "content": "Hello! How can I assist you today?",
                     "refusal": null,
                     "annotations": []
                  },
                  "logprobs": null,
                  "finish_reason": "stop"
               }
            ],
            "usage": {
               "prompt_tokens": 18,
               "completion_tokens": 10,
               "total_tokens": 28,
               "prompt_tokens_details": {
                  "cached_tokens": 0,
                  "audio_tokens": 0
               },
               "completion_tokens_details": {
                  "reasoning_tokens": 0,
                  "audio_tokens": 0,
                  "accepted_prediction_tokens": 0,
                  "rejected_prediction_tokens": 0
               }
            },
            "service_tier": "default",
            "system_fingerprint": null
         }
      },
      "errors": []
   }
}
```

### Example Usage

- Send the recorded requests to an alternative API endpoint.
- Compare the responses against the original OpenAI responses.
- Identify compatibility gaps and discrepancies.

## Contributing

If you have additional recorded data or improvements, feel free to submit a pull request!
However make sure you go through the recording process.
