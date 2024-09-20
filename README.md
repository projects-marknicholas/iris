
# API Documentation

## Overview
This API allows users to generate images and text based on provided prompts. It uses bearer token authentication to manage access and has request limits based on user status.

## Endpoint
- URL: `/path/to/your/api.php`
- Method: `POST`
- Content-Type: `application/json`
- Authorization: `Bearer <your_api_key>`

## Request Structure

### Headers
- Authorization: Bearer token for authentication.

### Body
The request body should be a JSON object containing the following fields:

- `action`: The action to perform (`generate_image` or `generate_text`).
- `prompt`: The prompt for generating the image or text.

### Example Request Body

```json
{
  "action": "generate_image",
  "prompt": "A beautiful sunset over a mountain range."
}
```

## Response Structure
The API responds with a JSON object that contains:

- status: Indicates success or error.
- message (optional): Error message in case of an error.
- image (if action is generate_image): Base64-encoded image data.
- text (if action is generate_text): Generated text response.

Example Response
```json
{
  "status": "success",
  "image": "<base64_encoded_image_data>"
}
```

## Error Responses
- Missing API Key: 
    ```json
    {
        "status": "error", 
        "message": "API key (Bearer token) is missing."
    }
    ```
- Invalid API Key: 
    ```json
    {
        "status": "error", 
        "message": "Invalid API key."
    }
    ```
- Exceeded Request Limit: 
    ```json
    {
        "status": "error", 
        "message": "You have exceeded the limit of requests per day."
    }
    ```
- Invalid Action: 
    ```json
    {
        "status": "error", 
        "message": "Invalid action."
    }
    ```
- Failed to Generate Image/Text: 
    ```
    {
        "status": "error", 
        "message": "Failed to generate image."
    }
    ```
    or

    ```
    {
        "status": "error", 
        "message": "Failed to generate text."
    }
    ```

## Sample HTML, CSS, and JavaScript Code

### HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="styles.css">
    <title>Image/Text Generator</title>
</head>
<body>
    <div class="container">
        <h1>Image/Text Generator</h1>
        <div>
            <label for="action">Select Action:</label>
            <select id="action">
                <option value="generate_image">Generate Image</option>
                <option value="generate_text">Generate Text</option>
            </select>
        </div>
        <textarea id="prompt" placeholder="Enter your prompt here..."></textarea>
        <button id="submit">Submit</button>
        <div id="result"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>
```

## CSS (styles.css)

```css
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    padding: 20px;
}

.container {
    max-width: 600px;
    margin: auto;
    background: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

h1 {
    text-align: center;
}

label {
    display: block;
    margin: 10px 0 5px;
}

textarea {
    width: 100%;
    height: 100px;
    margin-bottom: 10px;
    padding: 10px;
}

button {
    display: block;
    width: 100%;
    padding: 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

#result {
    margin-top: 20px;
}
```

## JavaScript (script.js)

```javascript
document.getElementById('submit').addEventListener('click', async () => {
    const action = document.getElementById('action').value;
    const prompt = document.getElementById('prompt').value;
    const apiKey = 'YOUR_API_KEY_HERE'; // Replace with your actual API key

    const response = await fetch('/path/to/your/api.php', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': `Bearer ${apiKey}`
        },
        body: JSON.stringify({ action, prompt })
    });

    const result = await response.json();
    document.getElementById('result').innerText = JSON.stringify(result, null, 2);
});
```

## How to Use

    1. Replace YOUR_API_KEY_HERE in the JavaScript file with your actual API key.
    2. Ensure your API is hosted and accessible at the specified path.
    3. Open the HTML file in a browser, enter a prompt, select an action, and click "Submit".
    4. The result will display the generated image or text in the result div.
