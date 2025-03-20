# Sparrow
[![PyPI - Python](https://img.shields.io/badge/python-v3.10+-blue.svg)]
[![GitHub Stars](https://img.shields.io/github/stars/katanaml/sparrow.svg)]
[![GitHub Issues](https://img.shields.io/github/issues/katanaml/sparrow.svg)]
[![Current Version](https://img.shields.io/badge/version-0.3.0-green.svg)]


Data processing with ML, LLM and Vision LLM

<p align="center">
  <img width="300" height="300" src="https://github.com/katanaml/sparrow/blob/main/sparrow-ui/assets/sparrow_logo_5.png">
</p>

## Overview

Sparrow is an innovative open-source solution for efficient data extraction and processing from various documents and images. It seamlessly handles forms, bank statements, invoices, receipts, and other unstructured data sources. Sparrow stands out with its modular architecture, offering independent services and pipelines all optimized for robust performance. One of the critical functionalities of Sparrow - pluggable architecture. You can easily integrate and run data extraction pipelines using Sparrow Parse (with vision-language models support) or Instructor. Sparrow enables local LLM data extraction pipelines through various backends, such as vLLM, Ollama, PyTorch or Apple MLX. Sparrow Parse with VL model can run either on premise, or it can execute inference on cloud GPU. With Sparrow solution you get API, which helps to process and transform your data into structured output, ready to be integrated with custom workflows.

Sparrow Pipelines - with Sparrow you can build independent LLM pipelines, and use API to invoke them from your system.

![Sparrow](https://github.com/katanaml/sparrow/blob/main/sparrow-ui/assets/sparrow_architecture.jpeg)

### Sparrow Components

* **[Sparrow ML LLM]** - Sparrow main engine that runs various pipelines
* **[Sparrow Agents]** - Sparrow Agent framework
* **[Sparrow Parse]** - Sparrow library enabling Sparrow Parse pipeline functionality using VL LLM. Works great for structured JSON response generation
* **[Sparrow OCR]** - OCR service, providing optical character recognition
* **[Sparrow UI]** - Dashboard UI for Sparrow

## Sparrow UI

Try [Sparrow](https://sparrow.katanaml.io) UI, this runs on my local Mac Mini M4 Pro machine with MLX

![Sparrow UI](https://github.com/katanaml/sparrow/blob/main/sparrow-ui/assets/sparrow_ui.png)

## Examples - data extraction with Sparrow

### Bank statement

![Bank statement](https://github.com/katanaml/sparrow/blob/main/sparrow-ui/assets/bank_statement.png)

```json
{
  "bank": "First Platypus Bank",
  "address": "1234 Kings St., New York, NY 12123",
  "account_holder": "Mary G. Orta",
  "account_number": "1234567890123",
  "statement_date": "3/1/2022",
  "period_covered": "2/1/2022 - 3/1/2022",
  "account_summary": {
    "balance_on_march_1": "$25,032.23",
    "total_money_in": "$10,234.23",
    "total_money_out": "$10,532.51"
  },
  "transactions": [
    {
      "date": "02/01",
      "description": "PGD EasyPay Debit",
      "withdrawal": "203.24",
      "deposit": "",
      "balance": "22,098.23"
    },
    {
      "date": "02/02",
      "description": "AB&B Online Payment*****",
      "withdrawal": "71.23",
      "deposit": "",
      "balance": "22,027.00"
    },
    {
      "date": "02/04",
      "description": "Check No. 2345",
      "withdrawal": "",
      "deposit": "450.00",
      "balance": "22,477.00"
    },
    {
      "date": "02/05",
      "description": "Payroll Direct Dep 23422342 Giants",
      "withdrawal": "",
      "deposit": "2,534.65",
      "balance": "25,011.65"
    },
    {
      "date": "02/06",
      "description": "Signature POS Debit - TJP",
      "withdrawal": "84.50",
      "deposit": "",
      "balance": "24,927.15"
    },
    {
      "date": "02/07",
      "description": "Check No. 234",
      "withdrawal": "1,400.00",
      "deposit": "",
      "balance": "23,527.15"
    },
    {
      "date": "02/08",
      "description": "Check No. 342",
      "withdrawal": "",
      "deposit": "25.00",
      "balance": "23,552.15"
    },
    {
      "date": "02/09",
      "description": "FPB AutoPay***** Credit Card",
      "withdrawal": "456.02",
      "deposit": "",
      "balance": "23,096.13"
    },
    {
      "date": "02/08",
      "description": "Check No. 123",
      "withdrawal": "",
      "deposit": "25.00",
      "balance": "23,552.15"
    },
    {
      "date": "02/09",
      "description": "FPB AutoPay***** Credit Card",
      "withdrawal": "156.02",
      "deposit": "",
      "balance": "23,096.13"
    },
    {
      "date": "02/08",
      "description": "Cash Deposit",
      "withdrawal": "",
      "deposit": "25.00",
      "balance": "23,552.15"
    }
  ],
  "valid": "true"
}
```

### Bonds table

![Bank statement](https://github.com/katanaml/sparrow/blob/main/sparrow-ui/assets/bonds_table.png)

```json
{
  "data": [
    {
      "instrument_name": "UNITS BLACKROCK FIX INC DUB FDS PLC ISHS EUR INV GRD CP BD IDX/INST/E",
      "valuation": 19049
    },
    {
      "instrument_name": "UNITS ISHARES III PLC CORE EUR GOVT BOND UCITS ETF/EUR",
      "valuation": 83488
    },
    {
      "instrument_name": "UNITS ISHARES III PLC EUR CORP BOND 1-5YR UCITS ETF/EUR",
      "valuation": 213030
    },
    {
      "instrument_name": "UNIT ISHARES VI PLC/JP MORGAN USD E BOND EUR HED UCITS ETF DIST/HDGD/",
      "valuation": 32774
    },
    {
      "instrument_name": "UNITS XTRACKERS II SICAV/EUR HY CORP BOND UCITS ETF/-1D-/DISTR.",
      "valuation": 23643
    }
  ],
  "valid": "true"
}
```

## Quickstart

1. Install `pyenv` and then install Python into your environment
2. Create virtual environment for the Sparrow pipeline you want to run
3. Install requirements for the Sparrow pipeline you want to use. Keep in mind, depending on OS, it could be required to do additional install steps for some of the libraries (for example PaddleOCR)
4. Run Sparrow either from CLI or from API. You need to start API endpoint
5. Pass query in the form of JSON schema to extract data from the document

See detailed instructions below.

## Installation

1. Python environment

For more details, check out the [extended section].

2. Run Sparrow

You can run Sparrow on CLI or through API. To run on CLI, use `sparrow.sh` script. Run it from corresponding virtual environment, depending which pipeline you want to execute. `sparrow-parse` pipeline is using VL LLM model. `sparrow-parse` pipeline runs VL LLM either locally with MLX, Ollama, or using cloud GPU. `instructor` pipeline is using Ollama backend. Make sure to pull LLM model for Ollama using name specified in config.yml to run `instructor` pipeline.

3. Private deployment

There is a property `PROTECTED_ACCESS: False` in config.yml. When set to `False`, `sparrow_key` is not verified on API call. Otherwise correct `sparrow-key` needs to be provided for API call.

## Inference

Arguments:

`query` - JSON query string argument with field names and types to fetch

`file-path` - input document. This can be image or multipage PDF

`pipeline` - Sparrow pipeline used to process query request

`crop_size=N` (where N is an integer) to crop N pixels from all borders of the input images. This can be helpful for removing unwanted borders or frame artifacts from scanned documents

`debug-dir` - folder where processed images are stored

`debug` - if True, additional messages will be printed

Options:

`--options mlx` - this will set MLX as backend for local inference

`--options mlx-community/Qwen2.5-VL-72B-Instruct-4bit` - name for Vision LLM model, supported by MLX

`--options tables_only` - set this option, if you want to process tables only

`--options validation_off` - set this option, if you want to disable response validation

`--page-type invoice --page-type adjudication_table --page-type adjudication_details` - used when `query=*`, specify a list of page type labels to be used to classify document pages

First two options are always set first.

It is possible to extract non-existing fields (fields missing from the document, NULL values will be assigned) with Sparrow. Use `or null` format for the query, example:

```
[{"instrument_name":"str", "valuation":0, "transaction_fees":"0.0 or null"}]
```


✅ Sparrow Parse pipeline, running locally with Apple MLX backend.

Sparrow validates response against request schema. Result of validation is automatically included into response, see property `valid`.

```
./sparrow.sh "[{"instrument_name":"str", "valuation":0}]" --pipeline "sparrow-parse" --debug --options mlx --options mlx-community/Qwen2.5-VL-72B-Instruct-4bit --file-path "/data/bonds_table.png"
```

Answer:

```json
{
  "data": [
    {
      "instrument_name": "UNITS BLACKROCK FIX INC DUB FDS PLC ISHS EUR INV GRD CP BD IDX/INST/E",
      "valuation": 19049
    },
    {
      "instrument_name": "UNITS ISHARES III PLC CORE EUR GOVT BOND UCITS ETF/EUR",
      "valuation": 83488
    },
    {
      "instrument_name": "UNITS ISHARES III PLC EUR CORP BOND 1-5YR UCITS ETF/EUR",
      "valuation": 213030
    },
    {
      "instrument_name": "UNIT ISHARES VI PLC/JP MORGAN USD E BOND EUR HED UCITS ETF DIST/HDGD/",
      "valuation": 32774
    },
    {
      "instrument_name": "UNITS XTRACKERS II SICAV/EUR HY CORP BOND UCITS ETF/-1D-/DISTR.",
      "valuation": 23643
    }
  ],
  "valid": "true"
}
```

✅ Sparrow Parse pipeline, with GPU backend on Hugging Face. GPU backend `katanaml/sparrow-qwen2-vl-7b` is private, to be able to run below command, you need to create your own backend on Hugging Face space using [code](https://github.com/katanaml/sparrow/tree/main/sparrow-data/parse/sparrow_parse/vllm/infra/qwen2_vl_7b) from Sparrow Parse.

```
./sparrow.sh "[{"instrument_name":"str", "valuation":0}]" --pipeline "sparrow-parse" --debug --options huggingface --options katanaml/sparrow-qwen2-vl-7b --file-path "/data/bonds_table.png"
```

✅ Sparrow Parse pipeline supports multi-page PDF documents. Running locally with Apple MLX backend. Response will be structured per page with page number indicators.

```
./sparrow.sh "{"table": [{"description": "str", "latest_amount": 0, "previous_amount": 0}]}" --pipeline "sparrow-parse" --debug --options mlx --options mlx-community/Qwen2.5-VL-72B-Instruct-4bit --file-path "/data/oracle_10k_2014_q1_small.pdf" --debug-dir "/data/"
```

Example running private GPU backend `katanaml/sparrow-qwen2-vl-7b`:

```
./sparrow.sh "{"table": [{"description": "str", "latest_amount": 0, "previous_amount": 0}]}" --pipeline "sparrow-parse" --debug --options huggingface --options katanaml/sparrow-qwen2-vl-7b --file-path "/data/oracle_10k_2014_q1_small.pdf" --debug-dir "/data/"
```

Sample answer:

```json
[
    {
        "table": [
            {
                "description": "Revenues",
                "latest_amount": 12453,
                "previous_amount": 11445
            },
            {
                "description": "Operating expenses",
                "latest_amount": 9157,
                "previous_amount": 8822
            }
        ],
        "valid": "true",
        "page": 1
    },
    {
        "table": [
            {
                "description": "Revenues",
                "latest_amount": 12453,
                "previous_amount": 11445
            },
            {
                "description": "Operating expenses",
                "latest_amount": 9157,
                "previous_amount": 8822
            }
        ],
        "valid": "true",
        "page": 2
    }
]
```

✅ Sparrow Parse pipeline running with cropping functionality

```
./sparrow.sh "*" --pipeline "sparrow-parse" --debug --options mlx --options mlx-community/Qwen2.5-VL-72B-Instruct-4bit --crop-size 60 --file-path "/data/invoice_1.pdf"
```

Sample answer:

```
{
  "invoice_number": "61356291",
  "date_of_issue": "09/06/2012",
  "seller": {
    "name": "Chapman, Kim and Green",
    "address": "64731 James Branch, Smithmouthouth, NC 26872",
    "tax_id": "949-84-9105",
    "iban": "GB50ACIE59715038217063"
  },
  "client": {
    "name": "Rodriguez-Stevens",
    "address": "2280 Angela Plain, Plain, MS 93248",
    "tax_id": "939-98-8477"
  },
  "items": [
    {
      "description": "Wine Glasses Goblets Pair Clear",
      "quantity": 5,
      "unit": "each",
      "net_price": 12.0,
      "net_worth": 60.0,
      "vat_percentage": 10,
      "gross_worth": 66.0
    },
    {
      "description": "With Hooks Stemware Storage Multiple Multiple Uses Iron Wine Rack Hanging",
      "quantity": 4,
      "unit": "each",
      "net_price": 28.08,
      "net_worth": 112.32,
      "vat_percentage": 10,
      "gross_worth": 123.55
    },
    {
      "description": "Replacement Corkscrew Parts Spiral Worm Worm Wine Opener Bottle Houdini",
      "quantity": 1,
      "unit": "each",
      "net_price": 7.5,
      "net_worth": 7.5,
      "vat_percentage": 10,
      "gross_worth": 8.25
    },
    {
      "description": "HOME ESSENTIALS GRADIENT STEMLESS WINE GLASSES SET OF 4 20 FL OZ (591 ml) NEW",
      "quantity": 1,
      "unit": "each",
      "net_price": 12.99,
      "net_worth": 12.99,
      "vat_percentage": 10,
      "gross_worth": 14.29
    }
  ],
  "summary": {
    "total_net_worth": 192.81,
    "total_vat": 19.28,
    "total_gross_worth": 212.09
  }
}
```

✅ LLM function call example:

```
./sparrow.sh assistant --pipeline "stocks" --query "Oracle"
```

Answer:

```json
{
  "company": "Oracle Corporation",
  "ticker": "ORCL"
}
```

```
The stock price of the Oracle Corporation is 186.3699951171875. USD
```

## Sparrow FastAPI Endpoint

Sparrow enables you to run a local LLM RAG as an API using FastAPI, providing a convenient and efficient way to interact with our services. You can pass the name of the plugin to be used for the inference. By default, `sparrow-parse` pipeline is used.

To set this up:

1. Start the Endpoint

Launch the endpoint by executing the following command in your terminal:

```
python api.py
```

If you want to run pipelines from different Python virtual environments simultaneously, you can specify port, to avoid conflicts:

```
python api.py --port 8001
```

2. Access the Endpoint Documentation

You can view detailed documentation for the API by navigating to:

```
http://127.0.0.1:8000/api/v1/sparrow-llm/docs
```

For visual reference, a screenshot of the FastAPI endpoint

![FastAPI endpoint](https://github.com/katanaml/sparrow/blob/main/sparrow-ui/assets/sparrow_api.png)

### API call inference

Arguments:

`query` - JSON query string argument with field names and types to fetch

`file-path` - input document. This can be image or multipage PDF

`pipeline` - Sparrow pipeline used to process query request

`crop_size=N` (where N is an integer) to crop N pixels from all borders of the input images. This can be helpful for removing unwanted borders or frame artifacts from scanned documents

`debug-dir` - folder where processed images are stored

`debug` - if True, additional messages will be printed

Options:

`--options mlx` - this will set MLX as backend for local inference

`--options mlx-community/Qwen2.5-VL-72B-Instruct-4bit` - name for Vision LLM model, supported by MLX

`--options tables_only` - set this option, if you want to process tables only

`--options validation_off` - set this option, if you want to disable response validation

`--page-type invoice --page-type adjudication_table --page-type adjudication_details` - used when `query=*`, specify a list of page type labels to be used to classify document pages

First two options are always set first.

It is possible to extract non-existing fields (fields missing from the document, NULL values will be assigned) with Sparrow. Use `or null` format for the query, example:

```
[{"instrument_name":"str", "valuation":0, "transaction_fees":"0.0 or null"}]
```

✅ `sparrow-parse` pipeline. This pipeline runs locally with Apple MLX backend.

```
curl -X 'POST' \
  'http://127.0.0.1:8000/api/v1/sparrow-llm/inference' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'query=[{"instrument_name":"str","valuation":0}]' \
  -F 'page_type=' \
  -F 'pipeline=sparrow-parse' \
  -F 'options=mlx,mlx-community/Qwen2.5-VL-72B-Instruct-4bit' \
  -F 'crop_size=' \
  -F 'debug_dir=' \
  -F 'debug=false' \
  -F 'sparrow_key=' \
  -F 'file=@bonds_table.png;type=image/png'
```

Alternatively, pipeline can run Visual LLM with GPU backend on Hugging Face. GPU backend `katanaml/sparrow-qwen2-vl-7b` is private, to be able to run below command, you need to create your own backend on Hugging Face space using [code] from Sparrow Parse.

```
curl -X 'POST' \
  'http://127.0.0.1:8000/api/v1/sparrow-llm/inference' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'query=[{"instrument_name":"str","valuation":0}]' \
  -F 'page_type=' \
  -F 'pipeline=sparrow-parse' \
  -F 'options=huggingface,katanaml/sparrow-qwen2-vl-7b' \
  -F 'crop_size=' \
  -F 'debug_dir=' \
  -F 'debug=false' \
  -F 'sparrow_key=' \
  -F 'file=@bonds_table.png;type=image/png'
```

Sparrow Parse pipeline supports multi-page PDF documents. You can pass PDF document through the API endpoint, response will be structured per page with page number indicators:

```json
[
    {
        "table": [
            {
                "description": "Revenues",
                "latest_amount": 12453,
                "previous_amount": 11445
            },
            {
                "description": "Operating expenses",
                "latest_amount": 9157,
                "previous_amount": 8822
            }
        ],
        "valid": "true",
        "page": 1
    },
    {
        "table": [
            {
                "description": "Revenues",
                "latest_amount": 12453,
                "previous_amount": 11445
            },
            {
                "description": "Operating expenses",
                "latest_amount": 9157,
                "previous_amount": 8822
            }
        ],
        "valid": "true",
        "page": 2
    }
]
```

## 🤖 Sparrow Agent

![Sparrow Agents](https://github.com/katanaml/sparrow/blob/main/sparrow-ui/assets/sparrow_agent.png)

Sparrow Agent provides a unified workflow system for orchestrating complex document processing tasks. It allows you to combine multiple document data extraction operations into a single coherent flow, with visual monitoring and tracking powered by Prefect. The agent system intelligently routes documents through classification, extraction, and validation steps, handling the entire pipeline from document ingestion to structured data output. Extensible by design, it currently supports document processing workflows and can be expanded to accommodate additional use cases.

Example:

```
curl -X 'POST' \
  'http://127.0.0.1:8001/api/v1/sparrow-agents/execute/file' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'agent_name=medical_prescriptions' \
  -F 'extraction_params={"sparrow_key":"123456"}' \
  -F 'file=@your_doc.pdf;type=application/pdf'
```

## Commercial usage

Sparrow is available under the GPL 3.0 license, promoting freedom to use, modify, and distribute the software while ensuring any modifications remain open source under the same license. This aligns with our commitment to supporting the open-source community and fostering collaboration.

Additionally, we recognize the diverse needs of organizations, including small to medium-sized enterprises (SMEs). Therefore, Sparrow is also offered for free commercial use to organizations with gross revenue below $5 million USD in the past 12 months, enabling them to leverage Sparrow without the financial burden often associated with high-quality software solutions.

For businesses that exceed this revenue threshold or require usage terms not accommodated by the GPL 3.0 license—such as integrating Sparrow into proprietary software without the obligation to disclose source code modifications—we offer dual licensing options. Dual licensing allows Sparrow to be used under a separate proprietary license, offering greater flexibility for commercial applications and proprietary integrations. This model supports both the project's sustainability and the business's needs for confidentiality and customization.

If your organization is seeking to utilize Sparrow under a proprietary license, or if you are interested in custom workflows, We're here to provide tailored solutions that meet your unique requirements, ensuring you can maximize the benefits of Sparrow for your projects and workflows.

