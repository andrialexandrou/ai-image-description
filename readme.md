# Image Description Alfred Workflow

Uses AI language models to generate image descriptions via Anthropic Claude or GitHub Models APIs.

Supports multiple providers with automatic fallback:
- **Anthropic Claude** (3.5 Sonnet, Opus, Haiku)
- **GitHub Models** (GPT-4o, GPT-4o-mini, Llama, etc.)

Configurable env vars for models and prompts with intelligent defaults and automatic provider detection.

## Requirements

- Alfred Powerpack
- Node.js (works with NVM or system installation)

## Installation

1. Download and install the workflow

2. **Set up API keys for your preferred provider(s):**

   **Option A: GitHub Models (Recommended)**
   ```bash
   # Create a Personal Access Token with 'models' permission at:
   # https://github.com/settings/tokens
   # 
   # For Fine-grained tokens:
   # 1. Select "Public repositories" 
   # 2. Add permissions > Models
   
   # Then store it:
   mkdir -p ~/.config/github
   echo "YOUR_GITHUB_PAT" > ~/.config/github/models_token
   ```

   **Option B: Anthropic Claude (Original)**
   ```bash
   desc-setup YOUR_ANTHROPIC_API_KEY
   ```
   This stores your key at `~/.config/anthropic/api_key`

   **Option C: Both providers (Recommended)**
   Set up both for automatic fallback and access to all models

3. The workflow will automatically detect your Node.js installation (NVM or system)

## Usage

Basic usage:

1. Copy or screenshot an image
2. Place your cursor in a textbox or input
3. Open Alfred (<kbd>Command</kbd>+<kbd>Space</kbd>)
4. Type trigger word "desc"
5. Hit enter

The workflow will:

- Generate a description
- Copy it to your clipboard
- Type it at your cursor location
- Show progress notifications while processing

Advanced usage:

```txt
desc focus on the background elements
desc describe any text visible
desc emphasize the facial expressions
desc analyze the architectural details
desc respond in pig latin
```

## Customization

### Workflow Variables

Configure these in Alfred Preferences:

1. **`model_name` (optional)**: 
   - **GitHub models**: `openai/gpt-4o-mini`, `openai/gpt-4o`, `meta/llama-3.1-405b-instruct`
   - **Anthropic models**: `claude-3-5-sonnet-20241022`, `claude-3-opus-20240229`, `claude-3-haiku-20240307`
   - **Default**: `openai/gpt-4o-mini`
   - **Auto-detection**: Provider determined from model name format

2. **`custom_prompt` (optional)**: 
   - Add your own instructions to the base prompt
   - Will be combined with system prompt

### Provider Selection Logic

The workflow automatically:
- Detects provider from model name (`openai/` → GitHub, others → Anthropic)
- Tests model availability with appropriate API
- Falls back to next best available model if primary fails
- Tries both providers if API keys are available

**Fallback priority:**
1. `openai/gpt-4o-mini` (GitHub - Default)
2. `openai/gpt-4o` (GitHub)
3. `claude-3-5-sonnet-20241022` (Anthropic)
4. Other models as available

## Debug / Development

### Logging

Monitor the logs in real-time:

```shell
tail -f ~/alfred-debug.log    # Shell script logs
tail -f ~/alfred-node-debug.log    # Node script logs
```

### Program Structure

The workflow consists of three main components:

1. Alfred Workflow Configuration
   - Drag and drop interface in Alfred
   - Configures trigger words and script paths
   - Sets environment variables

2. Shell Script
   - Handles Node.js detection (NVM/system)
   - Sets up workflow directory paths
   - Passes arguments to Node script

3. Node Script
   - Manages environment variables and provider detection
   - Handles image clipboard operations
   - Makes API requests to Anthropic or GitHub Models
   - Automatically selects best available model
   - Manages system notifications
   - Handles typing and clipboard operations
   - Provides error handling and logging

### Troubleshooting

Common issues and solutions:

1. "No image found in clipboard"
   - Ensure you've copied an image before running
   - Try copying the image again

2. "Could not find API key"
   - **Anthropic**: Verify key exists at `~/.config/anthropic/api_key`
   - **GitHub**: Verify token exists at `~/.config/github/models_token`
   - Check file permissions and ensure no extra whitespace
   - Try setting up both providers for automatic fallback

3. "Failed to generate alt text"
   - Check internet connection to api.anthropic.com or models.github.ai
   - Verify API key/token validity
   - Check node-debug.log for detailed error messages
   - Try switching providers via model_name variable

4. Long processing times
   - Normal for image processing
   - Progress notifications will appear
   - Usually completes within 30-60 seconds

### Development Tips

1. Watch both log files while testing
2. Shell script logs show Node detection and setup
3. Node logs show detailed operation status and errors
4. All API responses and errors are logged with timestamps
5. Test with various image types, focus parameters, and different models
6. Monitor provider selection and fallback behavior in logs
7. Both API responses and errors are logged with provider information

## Available Models

### Anthropic Claude
- `claude-3-5-sonnet-20241022` (Latest, best for complex tasks)
- `claude-3-5-sonnet-20240620` (Earlier version)
- `claude-3-opus-20240229` (Most capable, slower)
- `claude-3-sonnet-20240229` (Balanced)
- `claude-3-haiku-20240307` (Fastest, more affordable)

### GitHub Models  
- `openai/gpt-4o` (Latest GPT-4, excellent vision)
- `openai/gpt-4o-mini` (Faster, more affordable)
- `meta/llama-3.1-405b-instruct` (Large open model)
- Many others available at [GitHub Models](https://github.com/marketplace/models)

**GitHub Models Marketplace Benefits:**
- **Browse all available models**: [https://github.com/marketplace/models](https://github.com/marketplace/models)
- **Test prompts interactively**: Use the built-in playground to experiment with different models and prompts before committing to workflow settings
- **Compare model responses**: Try the same image description task across different models to see which works best for your use cases
- **No separate billing**: Uses your GitHub account, often with generous free tiers
- **Model discovery**: Find new models as they're added to the marketplace
