# Image Description Alfred Workflow

Uses Anthropic LLM API to generate an image description.

Configurable env vars of the LLM model and prompt begin with reasonable and tested defaults, and allow you to modify the requests to your needs should you wish to further refine the prompt.

>[!WARNING]
>Do not use this workflow on any confidential content, as the image is uploaded to Anthropic for processing.

## Requirements

- Alfred Powerpack
- Node.js (works with NVM or system installation)

## Installation

1. Download and install the workflow
2. Open Alfred and type:

   ```txt
   desc-setup YOUR_ANTHROPIC_API_KEY
   ```

   This will store your API key in the correct location (`~/.config/anthropic/api_key`)
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

1. `custom_prompt` (optional): 
   - Add your own instructions to the base prompt
   - Will be combined with system prompt

2. `model_name` (optional): 
   - Default: claude-3-opus-20240229
   - Can be changed to other Claude models

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
   - Manages environment variables
   - Handles image clipboard operations
   - Makes API requests to Anthropic
   - Manages system notifications
   - Handles typing and clipboard operations
   - Provides error handling and logging

### Troubleshooting

Common issues and solutions:

1. "No image found in clipboard"
   - Ensure you've copied an image before running
   - Try copying the image again

2. "Could not find API key"
   - Verify key exists at `~/.config/anthropic/api_key`
   - Check file permissions

3. "Failed to generate alt text"
   - Check internet connection
   - Verify API key validity
   - Check node-debug.log for details

4. Long processing times
   - Normal for image processing
   - Progress notifications will appear
   - Usually completes within 30-60 seconds

### Development Tips

1. Watch both log files while testing
2. Shell script logs show Node detection and setup
3. Node logs show detailed operation status and errors
4. All API responses and errors are logged with timestamps
5. Test with various image types and focus parameters
