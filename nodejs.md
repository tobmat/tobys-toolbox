# Node.js

Draft - not currently using Node, will cleanup at some point...

**forever – run node as daemon**

```text
forever start chef_bridge.js 
forever stop chef_bridge.js
forever logs – see path to log files
```

**testing -** will restart on file changes

```text
npm install -g nodemon
nodemon <name>.js
```

**list packages**

npm list -g --depth=0

* -

   -g indicates global, depth is how many level deep you want to go

**new nodejs package**

make a new directory

cd into new dir

npm ini

npm install &lt;pkg&gt; --save

save as repo put node\_modules in .gitignore

**Install npm package**

option 1 – directly

npm install git+ssh://git@bitbucket.org:caas2os/chef-bridge.git

* -

   this creates a node\_modules dir and places package in it

option 2 – git clone

clone the repo, cd into repo

npm install .

**Install commands**

curl --silent --location [https://rpm.nodesource.com/setup](https://rpm.nodesource.com/setup) \|sudo bash -

sudo yum -y install nodejs

sudo yum install gcc-c++ make

sudo npm install chef-api

sudo npm install express

**Example code to test chef-api npm:**

var ChefApi = require\("chef-api"\);

var chef = new ChefApi\(\);

var options = {

user\_name: "caas2-admin",

key\_path: "caas2-admin.pem",

organization: "caas2-dev"

}

chef.config\(options\);

////chef.getNodeCookbooks\("tor1", function\(err, res\){

//chef.getDataBags\(function\(err, res\){

//chef.getNodes\(function\(err, res\){

chef.getNode\("tor1", function\(err, res\){

//chef.getDataBag\("tobytest", function\(err, res\){

if\(err\)

throw err;

console.log\(res\);

}\);

**Example code to create a web service against hosted chef:**

var express = require\('express'\);

var app = express\(\);

var ChefApi = require\("chef-api"\);

var chef = new ChefApi\(\);

var options = {

user\_name: "caas2-admin",

key\_path: "caas2-admin.pem",

organization: "caas2-dev"

}

chef.config\(options\);

app.get\('/getNodes', function \(req, res\) {

chef.getNodes\(function\(err, data\) {

console.log\( data \);

res.end\( JSON.stringify\(data\) \);

}\);

}\)

app.get\('/getNode/:id', function \(req, res\) {

chef.getNode\(req.params.id, function\(err, data\){

console.log\( data \);

res.end\( JSON.stringify\(data\) \);

}\);

}\)

app.get\('/getDataBags', function \(req, res\) {

chef.getDataBags\(function\(err, data\) {

console.log\( data \);

res.end\( JSON.stringify\(data\) \);

}\);

}\)

app.get\('/getDataBag/:db', function \(req, res\) {

chef.getDataBag\(req.params.db, function\(err, data\) {

console.log\( data \);

res.end\( JSON.stringify\(data\) \);

}\);

}\)

app.get\('/getDataBagItem/:db/:it', function \(req, res\) {

chef.getDataBagItem\(req.params.db, req.params.it, function\(err, data\) {

console.log\( data \);

res.end\( JSON.stringify\(data\) + "\n" \);

}\);

}\)

var server = app.listen\(8081, function \(\) {

var host = '62.193.13.86'

var port = server.address\(\).port

console.log\("Example app listening at [http://%s:%s](http://%s:%s)", host, port\)

}\)

