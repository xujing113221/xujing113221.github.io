Create My Blog Using Hexo
======

Deploy my new blog
----

### Set information to use Git

<https://github.com/hexojs/hexo-deployer-git>

```bash
$ npm install hexo-deployer-git --save
```

### Create a new post file

```bash
$ hexo new my-first-blog
INFO  Created: ~/***/yt8yt.github.io/source/_posts/my-first-blog.md
```

### Deploy your new blog

```bash
$ hexo generate # or hexo g
$ hexo clean    
$ hexo deply    # or hexo d
```

遇到的问题
----
### 问题一: 创建博客时候遇到安全漏洞

```bash
$ hexo init myblog

INFO:
....
Thank you for installing EJS: built with the Jake JavaScript build tool (https://jakejs.com/)

npm notice created a lockfile as package-lock.json. You should commit this file.
added 253 packages from 452 contributors and audited 253 packages in 9.225s

5 packages are looking for funding
  run `npm fund` for details

found 1 low severity vulnerability
  run `npm audit fix` to fix them, or `npm audit` for details
```
####解决方案：

* 错误方案

```bash 
$ npm audit fix

INFO:
npm ERR! code EAUDITNOPJSON
npm ERR! audit No package.json found: Cannot audit a project without a package.json

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/xujing/.npm/_logs/2020-07-08T22_39_25_571Z-debug.log
```
* 正确方案

```bash
$ npm init -yes
INFO: Wrote to /Users/xujing/Desktop/xujing113221.github.io/package.json:
...

$ npm audit fix
INFO: npm ERR! code EAUDITNOLOCK
npm ERR! audit Neither npm-shrinkwrap.json nor package-lock.json found: Cannot audit a project without a lockfile
npm ERR! audit Try creating one first with: npm i --package-lock-only

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/xujing/.npm/_logs/2020-07-08T22_45_59_745Z-debug.log

$ npm i --package-lock-only
INFO: npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN xujing113221.github.io@1.0.0 No description

up to date in 0.59s
found 0 vulnerabilities
```
