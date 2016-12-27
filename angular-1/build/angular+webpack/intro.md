Webpack
=======

webpack is a module bundler. This means webpack takes modules with dependencies
and emits static assets representing those modules.

Instalacja
==========

Instalowany za pomocą: npm install webpack

Usage
=====

Can be used as a CLI - webpack and instructions
Can be used by a webpack.conf.js - configuration file

Configuration
=============

A webpack configuration file is a CommonJS-style module. So you can run any kind of code here, as long as a configuration object is exported out of this module:

module.exports = {...}


running configuration
---------------------
Terminal:

cd /projekt
webpack

Server
