### Prerequisites

You're going to need
* npm
* nodejs
* Angular

You can install Angular with this command:
```
npm install -g @angular/cli@10.0.5 
```

**Angular is not needed if you are only doing changes to WebRTCAppEE**
**Skip to "how to package the build files" if no changes to the root folder**
  
### Installation


1. Clone the repo. If using the CLI, make sure you have an SSH key set up(or, better yet, a private key) or simply log in with Github Desktop.
   ```sh
   git clone https://github.com/ImencoAS/ims-vms-management-console
   ```
2. Install NPM packages inside the cloned repository
   ```sh
   npm install
   ```

<!-- USAGE EXAMPLES -->
## Usage

You will need Node version 16 for this to work.
I recommend using [nvm](https://github.com/nvm-sh/nvm)

Then you simply can write `nvm use 16`

To run the web interface locally, use this command:

```sh
  ng serve
```

You might want to update the endpoint to a server running Ant Media Server to be able to login.
That is done in: `rest.service.ts`

```js
        }
        if (location.port == "4200")
        {
            //if it is angular development
            HTTP_SERVER_ROOT = "//" + location.hostname + ":5080/"; //CHANGE THIS TO THE IP OF THE SERVER: HTTP_SERVER_ROOT = "//" + "10.2.34.176" + ":5080/"
        }
        else if (location.protocol.startsWith("https")){
            HTTP_SERVER_ROOT = "https://" + location.hostname + ":" + location.port + "/";
        }
```



To build the project, use this command:

```sh
  ng build
```

To package the build files, use this command:

```sh
  npm run package
```

## Making changes to IMS VMS Management Console
There are a couple different scenarios when editing the IMS VMS Management Console
### Updating AMS Version

When updating the AMS version, follow the steps below:
1. Make sure you've followed and installed all prerequisites 
1. Make sure you have make installed - To install make run `choco install make` - you can get chocolatey from here: https://chocolatey.org/install
1. Download the release from www.antmedia.io and place it in the IMS VMS root folder on your local machine
1. Open Makefile and change `DOCKER_IMAGE_AMS_BASE?=imenco/antmediaserver-base:<VERSION, e.x 2.7.0>` and `AMS_VERSION?=<filename.zip, e.x ant-media-server-enterprise-2.7.0-20231031_0626.zip>` to the correct values. 
1. Open Dockerfile and change line `FROM imenco/antmediaserver-base:<VERSION, e.x 2.7.0>`
1. Run `make docker-build-push-vms`
1. Deploy from JFrog

### Making changes to the console
If you make changes to the IMS VMS Management Console without updating the AMS version, you can do the following:
1. Make sure you've followed and installed all prerequisites 
1. Make sure you have make installed
1. Run `make build-vms push-docker`
1. Deploy from JFrog

This will create a .zip file that can be uploaded as a release to GitHub 

Info about CSS. CSS is handled by GULP, wich you can read more about here: https://gulpjs.com/
