# Enhanced Image Generation System for AI Copilot

This document describes the enhanced image generation system implemented for the AI Copilot application, including the setup for Automatic1111 and ComfyUI, model management, and automatic updates.

## Overview

The AI Copilot image generation system now supports:

1. **Multiple Model Sizes**: Properly handles both SD1.5 and SDXL models with optimized configurations
2. **Automatic Updates**: Scheduled updates for both Automatic1111 and ComfyUI
3. **Enhanced Model Management**: Automatic model syncing between Automatic1111 and ComfyUI
4. **Improved ComfyUI Workflows**: Better workflows for different model types and image styles
5. **Expanded Uncensored Models**: Additional high-quality uncensored models
6. **Performance Optimizations**: Environment variables for better VRAM management

## Components

### 1. Automatic1111 (Stable Diffusion WebUI)

- **Path**: `E:\stable-diffusion-webui`
- **Web Interface**: http://localhost:7860
- **API Endpoint**: http://localhost:7860/sdapi/v1
- **Launch Script**: `webui-api.bat`

#### Key Enhancements:

- Support for multiple models with identical names but different hashes
- Memory optimizations for both low and high VRAM systems
- Auto browser launch option
- Model caching system
- API-first configuration for headless operation
- Enhanced sampler configurations

### 2. ComfyUI

- **Path**: `E:\comfyui`
- **Web Interface**: http://localhost:8188
- **API Endpoint**: http://localhost:8188/prompt
- **Launch Script**: `run_comfyui.bat`

#### Key Enhancements:

- Intelligent workflow detection for SD1.5 vs SDXL models
- Performance optimizations with memory management
- Expanded custom nodes collection
- Model sharing with Automatic1111
- Auto-launch and browser configuration

### 3. Model Management

The new model management system (`model-manager.ps1`) provides:

- Automatic model synchronization between Automatic1111 and ComfyUI
- Model integrity verification
- Hash-based model identification
- Support for downloading new models
- Model type detection (SD1.5, SDXL, VAE, LoRA)

### 4. Automatic Updates

The automatic update system (`setup-auto-updates.ps1`) provides:

- Scheduled updates through Windows Task Scheduler
- Repository updates for both main applications
- Extension/custom node updates
- Dependency management
- Detailed logging

## Usage

### Setting Up the Image Generation Stack

Run the main setup script to install and configure both Automatic1111 and ComfyUI:

```powershell
.\setup-ai-image-stack.ps1
```

Options:
- `-SDInstallPath`: Custom installation path for Automatic1111
- `-ComfyUIInstallPath`: Custom installation path for ComfyUI
- `-SkipModelDownload`: Skip downloading default models
- `-InstallUncensoredModels`: Include uncensored models
- `-SkipComfyUI`: Install only Automatic1111
- `-AutomaticUpdates`: Enable automatic updates during setup

### Managing Models

Use the model manager to handle model operations:

```powershell
.\model-manager.ps1
```

Options:
- `-SyncModels`: Synchronize models between Automatic1111 and ComfyUI
- `-CheckForUpdates`: Check for model updates
- `-VerifyIntegrity`: Verify the integrity of installed models
- `-DownloadModel <url>`: Download a specific model

### Setting Up Automatic Updates

Configure automatic updates with:

```powershell
.\setup-auto-updates.ps1
```

Options:
- `-EnableScheduledUpdates`: Set up a scheduled task for updates
- `-UpdateNow`: Run an update immediately
- `-UpdateIntervalDays`: Set the interval between updates (default: 7)

## Configuration Files

### Automatic1111 Configuration

The main configuration is in `config.json` in the Automatic1111 directory, with optimized settings for:

- Memory management
- Sampling methods
- Interface preferences
- Output formats and paths

### ComfyUI Configuration

ComfyUI configurations are stored in its main directory with settings for:

- Model paths
- Memory allocation
- Performance optimizations

## API Integration

The backend service (`localImageGeneration.enhanced.js`) integrates with both APIs and provides:

- Automatic provider selection
- Optimized parameter selection based on model type
- Style-based configuration
- Error handling and fallback mechanisms

## Maintenance

Regular maintenance tasks:

1. **Update the Applications**: Run `update.bat` in each application's directory or use the auto-update system
2. **Synchronize Models**: Run `.\model-manager.ps1 -SyncModels`
3. **Check Model Integrity**: Run `.\model-manager.ps1 -VerifyIntegrity`

## Troubleshooting

Common issues and solutions:

1. **Model Loading Errors**: Ensure the model exists in both directories using `model-manager.ps1`
2. **API Connection Issues**: Check that the servers are running and the correct ports are used
3. **Image Generation Failures**: Verify VRAM availability and optimize parameters for your system
4. **Update Failures**: Check for local changes in git repositories that may block pulls

## Future Enhancements

Planned improvements:

1. Integration with additional image generation APIs
2. Support for more model types (ControlNet, IP-Adapter)
3. Enhanced workflow templates for different use cases
4. Web-based model management interface
5. Cloud model repository integration
