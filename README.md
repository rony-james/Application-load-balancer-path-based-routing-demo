# Application-load-balancer-path-based-routing-demo
Path-based routing is one of the unique feature offered by ALB. Path-based routing is also referred as URL based routing. The Application load balancer will forward the requests to the specific targets based on the Rules configured in the Load balancer. 


# Configure Path-based Routing on Application Load balancer
## My Environment Setup
- VPC
- EC2 instances
- ALB
- Target Groups
- AWS Certificate Manager
- Route53



[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Step 1: Created a public hosted zone on Route53 for "rony.website". The nameserves of the domaon "rony.website" changed as mentioned on the public hosted zone.
![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/53.png?raw=true)


Step 2: Initiated a Certificate request for the domain "rony.website"
![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/Certificate.png?raw=true)

Step 3: Created a Security Group for This project.

Step 4: Created 3 EC2 Instances and installed httpd service.
![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/EC2.png?raw=true)

Step 5: Create the Target Groups for 3 EC2 instances. Once It's created, register the corresponding EC2 with Target Group.
![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/TG.png?raw=true)

Step 6: Create an ALB. we can mention both 80 and 443 listener. If the AWS Ssl certificate is ready to use, we can attach the certificate details during the time of ALB creation.
![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/LB.png?raw=true)

Step 7: Rule set creation on ALB. Here we can create path based rule set for redirecting the request to corresponding Target Group. The rules we have configured for the Path based routing are an Exact Match.
For this project , We have configured rules to forward the requests from the Users to a definite Path (/credit & /debit). But There are some cases where the users requests for an information which is further down the path such as /credit/cibil and /debit/data. So In this case We have to configure a rule for the path with the wildcard , This will ensure that the any other information under this path is served for the users properly. During that time we can use wildcard as /credit* or /debit*.

![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/rule-set.png?raw=true)

Step 8: Creating Record on Route53.
![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/53-alias.png?raw=true)

![alt text](https://github.com/rony-james/Application-load-balancer-path-based-routing-demo/blob/main/53-records.png?raw=true)




## Features

- Import a HTML file and watch it magically convert to Markdown
- Drag and drop images (requires your Dropbox account be linked)
- Import and save files from GitHub, Dropbox, Google Drive and One Drive
- Drag and drop markdown and HTML files into Dillinger
- Export documents as Markdown, HTML and PDF

Markdown is a lightweight markup language based on the formatting conventions
that people naturally use in email.
As [John Gruber] writes on the [Markdown site][df1]

> The overriding design goal for Markdown's
> formatting syntax is to make it as readable
> as possible. The idea is that a
> Markdown-formatted document should be
> publishable as-is, as plain text, without
> looking like it's been marked up with tags
> or formatting instructions.

This text you see here is *actually- written in Markdown! To get a feel
for Markdown's syntax, type some text into the left window and
watch the results in the right.

## Tech

Dillinger uses a number of open source projects to work properly:

- [AngularJS] - HTML enhanced for web apps!
- [Ace Editor] - awesome web-based text editor
- [markdown-it] - Markdown parser done right. Fast and easy to extend.
- [Twitter Bootstrap] - great UI boilerplate for modern web apps
- [node.js] - evented I/O for the backend
- [Express] - fast node.js network app framework [@tjholowaychuk]
- [Gulp] - the streaming build system
- [Breakdance](https://breakdance.github.io/breakdance/) - HTML
to Markdown converter
- [jQuery] - duh

And of course Dillinger itself is open source with a [public repository][dill]
 on GitHub.

## Installation

Dillinger requires [Node.js](https://nodejs.org/) v10+ to run.

Install the dependencies and devDependencies and start the server.

```sh
cd dillinger
npm i
node app
```

For production environments...

```sh
npm install --production
NODE_ENV=production node app
```

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
