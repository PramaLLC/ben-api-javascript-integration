# Background Removal API Javascript Integration

Javascript wrapper for the Background Removal API that removes backgrounds from images.

## Installation
```bash
git clone https://github.com/PramaLLC/api-javascript-integration
cd api-javascript-integration
npm install
```

## Generate api token 
You must have a business subscription that can be found at https://backgrounderase.net/pricing. To generate the token navigate to
https://backgrounderase.net/account and scroll to the bottom of the page.

## Example Code

```javascript
const fs = require('fs');
const path = require('path');
const { predictImage } = require('./foregroundRemoval');

async function main() {
  try {
    const apiKey = 'your_ben_api_token'; // Replace with your API token
    const apiUrl = 'https://api.backgrounderase.net/v2';
    
    // Load image file
    const inputPath = path.join(__dirname, 'image.jpg'); // Replace with your image path
    const originalBuffer = fs.readFileSync(inputPath);
    
    // Get prediction
    const result = await predictImage(originalBuffer, apiKey, apiUrl);
    
    if (!result) {
      console.error('Failed to get a valid result from predictImage.');
      return;
    }
    
    // Save results
    const { mask, foreground } = result;
    fs.writeFileSync(path.join(__dirname, 'result.png'), foreground);
    fs.writeFileSync(path.join(__dirname, 'mask.png'), mask);
    
  } catch (err) {
    console.error('Error:', err);
  }
}

main();
```

## To Run The Example Code
```bash
node runForegroundRemoval.js
```


## API Documentation
For full API documentation visit: https://backgrounderase.net/api-docs
