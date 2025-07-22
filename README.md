---
markdown
# Connecting NBFiddle to a Local JupyterLab Server

This guide explains how to connect a remote frontend like [NBFiddle](https://nbfiddle.app) to a local JupyterLab server running in this project’s virtual environment (`.venv`).

---

## 🚀 Quick Setup Instructions

### 1. Activate the virtual environment

```bash
source .venv/bin/activate
````

> Make sure `.venv` was previously created with:
>
> ```bash
> uv venv .venv
> ```

---

### 2. Install JupyterLab and DANDI (if not already done)

```bash
uv add jupyterlab dandi
```

---

### 3. Start the JupyterLab server with NBFiddle support

```bash
jupyter lab \
  --ServerApp.allow_origin='https://nbfiddle.app' \
  --no-browser \
  --port=8888
```

This command:

* Starts JupyterLab without opening a browser
* Allows CORS from NBFiddle
* Uses port 8888 (you can change it if needed)

---

### 4. Copy the Jupyter token from the terminal

Example output:

```
http://localhost:8888/lab?token=abc123def456...
```

Copy the part after `token=`.

---

### 5. Connect from [https://nbfiddle.app](https://nbfiddle.app)

1. Click **“Connect to Jupyter Server”**
2. Enter:

   * **Server URL**: `http://localhost:8888`
   * **Token**: the token from step 4
3. Click **Connect**

---

## 🔌 To Disconnect NBFiddle

### Option 1: Kill the Jupyter server

In the terminal:

```bash
Ctrl + C
```

### Option 2: Restart without CORS access

```bash
jupyter lab --no-browser --port=8888
```

This disables access from NBFiddle by removing `allow_origin`.

---

## 🛡️ Security Tips

* Do **not** disable the token (`--ServerApp.token=''`) unless in a secure, isolated setup.
* Tokens expire each time the server restarts.
* Avoid using `--disable_check_xsrf=True` in any shared or public network.

---

## 🧠 Optional: Register `.venv` as a Jupyter kernel

This allows you to select the environment explicitly in NBFiddle or JupyterLab:

```bash
pip install ipykernel
python -m ipykernel install --user --name=dandi-analysis --display-name "Python (dandi-analysis)"
```

---

## 📁 Project Path

Make sure you're inside your project folder (e.g., `pynwb_dandi/dandihub-analysis`) when running the commands above.

---
