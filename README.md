
# Create-React-App-Lambda-from-scratch
WARNING this tutorial is using yarn. Big oof.
## Step 1)
### Create a react app
```bash
npx create-react-app <folder-name>
```
## Step 2)
### inside the react app folder just created, install the following two packages:
```bash
yarn add run-p
```
```bash
yarn add netlify-lambda
```
## Step 3)
### Add the netlify.toml file in the root of the project and fill it with the needed config
```toml
[build]
    command = "yarn build"
    functions = "built-lambda"
    publish = "build"
```
## Step 4)
### Setup the package.json scripts to build both the front end and the backend at the same time using run-p
```json
"scripts": {
    "start": "react-scripts start",
    "build": "run-p build:**",
    "build-app": "react-scripts build",
    "build-lambda": "netlify-lambda build src/lambda"
}
```
## Step 5)
### Create the lambda folder inside the src folder,
### add a simple lambda inside a file called src/lambda/test.js:
```javascript
exports.handler = (event, context, callback) => {
    callback(null, {
        statusCode: 200,
        body: 'this is text.js'
    });
}
```
## Step 6)
### test your app by running the netlify dev command
### you will need to install netlify-dev globally for this to work:
``` bash
ntl dev -p 9000
```
### Once your app is running, browse to ```localhost:9000``` to see your front end
### Browse to ```localhost:9000/.netlify/functions/test``` to see you backend
## Step 7)
### If step 6 worked, theoretically, if you commit your code, push to git, and then deploy to netlify, you would have a serverless full stack project running on the web.