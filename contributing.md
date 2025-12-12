# Contributing to Image Description Alfred Workflow

Thank you for your interest in contributing to this Alfred workflow! This guide covers development setup, testing, and distribution.

## Development Setup

### Prerequisites
- Alfred Powerpack
- Node.js (NVM or system installation)
- API keys for testing (GitHub Models and/or Anthropic)

### Local Development
1. **Clone/modify the workflow files directly** in the Alfred workflow directory
2. **Monitor logs during development:**
   ```bash
   # Terminal 1: Watch Node.js logs
   tail -f ~/alfred-node-debug.log
   
   # Terminal 2: Watch shell script logs  
   tail -f ~/alfred-debug.log
   ```

3. **Test with various scenarios:**
   - Different image types (screenshots, web images, diagrams)
   - Various focus parameters
   - Different model configurations
   - Error conditions (no API key, network issues, etc.)

## Making Changes

### Code Structure
- **`alt-text.js`** - Main Node.js script handling API calls and image processing
- **`readme.md`** - User documentation and setup instructions
- **Shell scripts** - Handle Node.js detection and environment setup (if present)
- **Alfred configuration** - Workflow triggers, environment variables, connections

### Key Areas for Contributions
1. **New AI providers** - Add support for additional APIs (OpenAI direct, Gemini, etc.)
2. **Enhanced error handling** - Better user feedback and recovery
3. **Performance improvements** - Faster image processing, better caching
4. **Documentation** - Clearer setup instructions, troubleshooting guides
5. **Testing** - Automated tests, edge case coverage

### Testing Your Changes
1. **Functional testing:**
   ```bash
   # Test basic functionality
   # 1. Copy an image
   # 2. Run: desc
   # 3. Verify alt text is generated and typed
   
   # Test with focus parameters
   desc focus on text content
   desc emphasize facial expressions
   ```

2. **Provider fallback testing:**
   - Test with only GitHub token
   - Test with only Anthropic key  
   - Test with both providers
   - Test with invalid credentials

3. **Error condition testing:**
   - No image in clipboard
   - Network connectivity issues
   - Invalid API credentials
   - Model availability issues

## Creating a Distribution

### Export Alfred Workflow Binary

1. **Open Alfred Preferences** (⌘,)
2. **Go to Workflows tab**
3. **Right-click your workflow** (or select it and click the gear icon)
4. **Choose "Export..."**
5. **Save the `.alfredworkflow` file**

### Export Options
- **Include configuration**: Exports environment variable names (but not sensitive values)
- **Strip configuration**: Clean export without user settings (recommended for distribution)

### What Gets Included/Excluded

✅ **Included in export:**
- All workflow files (`alt-text.js`, `readme.md`, `contributing.md`, etc.)
- Workflow configuration and triggers
- Environment variable names (but not values)
- Script connections and Alfred settings

❌ **Not included (good for security):**
- API keys/tokens
- User-specific file paths
- Personal configuration values

### Distribution Checklist

Before creating a release:

- [ ] **Test with fresh installation** (export and re-import)
- [ ] **Verify documentation is current** 
- [ ] **Test setup instructions** work for new users
- [ ] **Update version numbers** if applicable
- [ ] **Test fallback scenarios** work properly
- [ ] **Validate both GitHub and Anthropic providers** 

### Release Process

1. **Create the `.alfredworkflow` file** using the export process above
2. **Test the exported workflow:**
   - Import it to a clean Alfred installation
   - Follow the setup documentation exactly
   - Verify functionality works as expected

3. **For GitHub releases:**
   - Upload the `.alfredworkflow` file as a release asset
   - Include changelog/version notes
   - Link to setup documentation
   - Tag the release appropriately

## Code Style and Standards

### Logging
- Use the existing `log()` and `logError()` functions
- Include context in error messages
- Log important state changes and decisions

### Error Handling
- Provide user-friendly error notifications
- Include detailed error logging for debugging
- Graceful degradation when possible

### Provider Support
- Follow existing patterns when adding new AI providers
- Maintain backward compatibility
- Include provider auto-detection logic
- Add appropriate model validation

## Getting Help

### Debug Information
Always include when reporting issues:
- Alfred version and OS version
- Node.js version (`node --version`)
- Relevant log excerpts from `~/alfred-node-debug.log`
- Steps to reproduce the issue
- Expected vs actual behavior

### Common Development Issues

1. **API Changes** - AI providers occasionally update their APIs
2. **Model Deprecation** - Models may become unavailable over time  
3. **Authentication** - Token/key format changes
4. **Network Issues** - Connectivity and DNS problems

### Contributing Guidelines

1. **Test thoroughly** before submitting changes
2. **Update documentation** when adding features
3. **Maintain backward compatibility** when possible
4. **Follow existing code patterns** for consistency
5. **Include appropriate logging** for debugging

Thank you for contributing to make this workflow better for everyone!
