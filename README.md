# Setup Guide: How to Run GLM Locally in VS Code

This guide shows you how to run a GLM model completely offline, free, and local inside VS Code using **Ollama** and the **Continue** extension.

> **Note on model naming:** There is no model called "GLM 5.2." The current GLM lineup from Z.ai (Zhipu AI) includes **GLM-5.1** (their large flagship agentic/coding model, 744B total parameters / 40B active) and **GLM-4.7-Flash** (a lighter 30B-A3B MoE model built for local/consumer-hardware deployment). The old `glm4` identifier some guides reference is a much smaller, outdated ~9B-class model from 2024 — pulling it will not get you a modern GLM model. This guide uses **GLM-4.7-Flash**, which is the realistic choice for most local setups.

---

### Step 0: Check your hardware first

- **GLM-4.7-Flash** (30B-A3B MoE): runs on consumer hardware — a modern GPU with ~16–24GB VRAM (or strong unified memory on Apple Silicon) is a reasonable target. This is the one this guide installs.
- **GLM-5.1** (744B total / 40B active): this is a massive model. It needs hundreds of GB of combined RAM/VRAM to run at any reasonable quality/speed. Not realistic for a laptop or typical desktop — skip this unless you have workstation/server-class hardware.

---

### Step 1: Install Ollama (The AI Engine)
Ollama runs large language models locally on your system CPU/GPU.

1. Go to [ollama.com](https://ollama.com) and download the version for your OS (Windows, macOS, or Linux).
2. Install the application and verify it is running in your taskbar (you will see the Ollama llama icon).
3. **Important:** GLM-4.7-Flash requires **Ollama 0.14.3**, which is currently in pre-release. Make sure your installed version meets this, or update Ollama if a newer build is available.

---

### Step 2: Download the GLM Model
Open your terminal (PowerShell, Command Prompt, or terminal in VS Code) and run:

```bash
ollama run glm-4.7-flash
```

*This pulls GLM-4.7-Flash from Ollama's official library and starts the local model server at `http://localhost:11434`.*

To test that it's working, type a prompt directly in your terminal, then type `/exit` to close it.

---

### Step 3: Install the "Continue" Extension in VS Code
Continue is an open-source AI assistant extension for VS Code that connects to local model endpoints.

1. Open **VS Code**.
2. Click on the **Extensions** icon on the left sidebar (or press `Ctrl+Shift+X`).
3. Search for **"Continue"** (by `continue.dev`) and click **Install**.
4. You will see a new **Continue icon** (a stylized "C") appear on your far left toolbar.

---

### Step 4: Configure VS Code to use GLM
Now we need to tell VS Code to talk to your local Ollama GLM model instead of standard cloud services.

1. Click on the **Continue** icon in the VS Code sidebar.
2. Click the **Gear/Settings icon** at the bottom right of the Continue panel. This opens your local `config.json` configuration file.
3. Replace or edit the `"models"` block with the following configuration:

```json
{
  "models": [
    {
      "title": "GLM-4.7-Flash (Local)",
      "provider": "ollama",
      "model": "glm-4.7-flash"
    }
  ],
  "tabAutocompleteModel": {
    "title": "GLM-4.7-Flash Autocomplete",
    "provider": "ollama",
    "model": "glm-4.7-flash"
  }
}
```

4. Save the file (`Ctrl+S`).

---

### Step 5: Test Your Setup
1. Open a new code file in VS Code.
2. Press **`Ctrl+L`** (or `Cmd+L` on Mac) to open the Continue Chat panel on the left.
3. Select **"GLM-4.7-Flash (Local)"** from the dropdown menu at the bottom.
4. Type a coding prompt (e.g., `"Write a fast binary search function in Python"`) and watch the local model stream the code in your editor window.
5. For autocomplete, simply start writing a function declaration and press **`Tab`** when the gray suggestion text appears.
