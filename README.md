# Laravel IDOR Tester

## Description

A Python tool designed to test for Insecure Direct Object References (IDOR) vulnerabilities in Laravel applications. It systematically scans endpoints by replacing ID parameters with different values and compares responses against a baseline to detect potential unauthorized access to sensitive data.

## Features

- Supports numeric and wordlist-based ID enumeration
- Multi-threaded scanning for efficiency
- Flexible authentication (Bearer token, cookies, custom headers)
- Response comparison with configurable field ignoring
- Multiple output formats (console, JSON, CSV)
- Configurable via YAML or command-line arguments

## Installation

1. Ensure Python 3.6+ is installed
2. Clone or download the project files
3. Install dependencies:

```bash
pip install -r requirements.txt
```

## Usage

### Using Configuration File (Recommended)

Create a `config.yaml` file based on the provided example. Then run:

```bash
python idor_tester.py --config config.yaml
```

### Using Command-Line Arguments

For quick testing without a config file:

```bash
python idor_tester.py --url "https://example.com/api/user/{id}" --method GET --token "your_bearer_token" --range 1 100 --baseline 1 --threads 10 --output results.json --format json
```

## Command-Line Options

- `--config`: Path to YAML configuration file
- `--url`: URL template with `{id}` placeholder (required if no config)
- `--method`: HTTP method (GET, POST, etc.) - default: GET
- `--token`: Bearer token for authentication
- `--range`: Numeric range for ID testing (start end) - default: 1 100
- `--wordlist`: Path to wordlist file containing IDs to test
- `--baseline`: Your own valid ID for baseline response comparison (required)
- `--threads`: Number of concurrent threads - default: 10
- `--output`: Output file path for results
- `--format`: Output format (console/json/csv) - default: console

## Configuration File Example

See `config.yaml` for a complete example. Key sections:

- `target`: URL template and HTTP method
- `auth`: Authentication settings
- `scan`: ID enumeration parameters
- `diff`: Baseline comparison settings
- `output`: Result output configuration

## Output

The tool reports potential IDOR vulnerabilities by comparing responses:

- JSON responses are diffed against the baseline, ignoring specified fields
- Status code differences are flagged
- Results can be displayed in console or saved to JSON/CSV files

## Security Note

Use this tool responsibly and only on systems you have permission to test. Unauthorized security testing may be illegal.