发布自己的package

## 1. 注册一个自己的[npm账号](https://www.npmjs.com/signup)

## 2. 建一个[github仓库](git@github.com:ys558/my-npm-module-test.git)

## 3. 项目结构

```
|__/package/
|__/test-folder/
```

`/package` 文件夹用于存放我们写的包   
`/test-folder` 文件夹用于引用并测试 `/package` 里的包

编写包 `my-package-publish-test`

在 `/package` 里初始化项目 `npm init` 并写一些关于该 package 的名字，如`my-package-publish-test` 和描述等东西    
像写普通文件一样，新建`/package/index.js` 并写下一些简单功能，如

```js
const isTest = string => string === 'test'
module.exports = isTest
```

## 4. 创建 node_modules 软链接

在当前目录 `./package/` 下运行创建软链接
```bash
npm link
```

返回 `./test-folder/` 下运行软链接，软链接后的名必须对应 `package/package.json` 的 `"name"`

```bash
cd ../test-folder/
npm link my-package-publish-test
```

## 5. 登录并发布
返回 `./package/` 并执行登录，运行
```bash
cd ../package/
npm login
```

输入一些 `npmjs.org`的用户名密码等，登录npm账号
```bash
$ npm login
Username: ys558
Password:
Email: (this IS public)
Email: (this IS public) yuyi.gz@163.com
Logged in as ys558 on https://registry.npmjs.org/.
```

如出现以下报错需要登录自己的邮箱是否通过 npmjs.org 的验证邮件

```bash
npm ERR! code E403
npm ERR! 403 403 Forbidden - PUT http://registry.npmjs.org/my-package-publish-test - Forbidden
npm ERR! 403 In most cases, you or one of your dependencies are requesting
npm ERR! 403 a package version that is forbidden by your security policy.

npm ERR! A complete log of this run can be found in:
npm ERR!     C:\Users\yuyi\AppData\Roaming\npm-cache\_logs\2021-07-04T12_02_21_879Z-debug.log
```

最后运行以下命令，即可发布成功属于自己的npm package
```bash
npm publish
```

发布成功：
```bash
$ npm publish
npm notice 
npm notice package: my-package-publish-test@1.0.0
npm notice === Tarball Contents ===
npm notice 85B  index.js
npm notice 564B package.json
npm notice 21B  README.md
npm notice === Tarball Details ===
npm notice name:          my-package-publish-test
npm notice version:       1.0.0
npm notice package size:  509 B
npm notice unpacked size: 670 B
npm notice shasum:        98b90c3ab222a573f0379802cc3d59d43ffcb402
npm notice integrity:     sha512-Fz/SDMr5vgoAe[...]UD5J4OP0rFtFA==
npm notice total files:   3
npm notice
+ my-package-publish-test@1.0.0
```