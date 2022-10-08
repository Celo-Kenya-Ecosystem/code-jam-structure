# Code Jam Structure
##  ✨Code Jam: Getting Started with Celo✨

Dillinger is a cloud-enabled, mobile-ready, offline-storage compatible,
AngularJS-powered HTML5 Markdown editor.

## Objectives

- Learn more about Celo
- Be able to explain how Celo is similar to and different from Ethereum
- Send Celo Dollars on the Alfajores Testnet
     - Create an account
     - Connect to the testnet
     - Fund the account
     - Send funds
- Run a Celo Node
- Learn how to make a simple web page that connects to Celo
- Learn how to make a simple mobile dapp that connects to Celo

## Requirements
- A computer with an internet connection
- Node.js (version 10+) and yarn installed on your computer
- Git installed on your computer
- Familiarity with Javascript and basic web development concepts
- Celo extension wallet (requires a Chrome-based web browser, like Chrome or Brave)

## Modules

### Jam 0: Learn about Celo

To learn more about the background of Celo, the technology stack, and the fundamental protocol, see the Celo Overview page of the Celo documentation. Here are some examples of video tutorials you can use if you prefer:

- [https://www.youtube.com/watch?v=LN7p6mB1t4k] - How to Build a DApp on Celo
- [https://www.youtube.com/watch?v=kO6Wm8pgKXU] - Developing & deploying your first DApp on Celo
- [https://www.youtube.com/watch?v=bp2loYXPhbM&t=16s] - Celo Tech Talks Building a mobile first blockchain platform.

## Jam 1. Sending Transactions
### Step up

1. Clone this GitHub repo: [https://github.com/critesjosh/celo-transactions-lesson]

```sh
 git clone https://github.com/critesjosh/celo-transactions-lesson.git
```

2. Go into the cloned project and install the dependencies

```sh
 cd celo-transactions-lesson && yarn install
```
3. Once the dependencies are installed, create a new file in the project root called .env. Then run

```sh
 node createAccount.js
```

This will print new Celo account details. Copy the private key for your new account into a _PRIVATE_KEY_ variable in .env. It should look something like this

```sh
PRIVATE_KEY="0x7b756cc34cdd08dfc96bea50101fdd62abb8a7ba9c083881dc6f6bd3bda35408"
```
Congratulations! You just created a new account on Celo! This private key controls access to the associated account, so this is highly sensitive data. Anyone with this key can send transactions on behalf of the account. You can see how this account is created in the ```sh createAccount.js ``` file.

4. Copy the address that is printed. Fund the account address on the Alfajores test net here: [https://celo.org/developers/faucet]

5. Create an account on Figment Data Hub [https://figment.io/datahub/celo/] and get your API key and add it to the FIGMENT_API_KEY in .env. This will allow you to connect to the Celo networks. Your .env file should now look something like this.


## Plugins

Dillinger is currently extended with the following plugins.
Instructions on how to use them in your own application are linked below.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Development

Want to contribute? Great!

Dillinger uses Gulp + Webpack for fast developing.
Make a change in your file and instantaneously see your updates!

Open your favorite Terminal and run these commands.

First Tab:

```sh
node app
```

Second Tab:

```sh
gulp watch
```

(optional) Third:

```sh
karma test
```

#### Building for source

For production release:

```sh
gulp build --prod
```

Generating pre-built zip archives for distribution:

```sh
gulp build dist --prod
```

## Docker

Dillinger is very easy to install and deploy in a Docker container.

By default, the Docker will expose port 8080, so change this within the
Dockerfile if necessary. When ready, simply use the Dockerfile to
build the image.

```sh
cd dillinger
docker build -t <youruser>/dillinger:${package.json.version} .
```

This will create the dillinger image and pull in the necessary dependencies.
Be sure to swap out `${package.json.version}` with the actual
version of Dillinger.

Once done, run the Docker image and map the port to whatever you wish on
your host. In this example, we simply map port 8000 of the host to
port 8080 of the Docker (or whatever port was exposed in the Dockerfile):

```sh
docker run -d -p 8000:8080 --restart=always --cap-add=SYS_ADMIN --name=dillinger <youruser>/dillinger:${package.json.version}
```

> Note: `--capt-add=SYS-ADMIN` is required for PDF rendering.

Verify the deployment by navigating to your server address in
your preferred browser.

```sh
127.0.0.1:8000
```

## License

MIT

**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
