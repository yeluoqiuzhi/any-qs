[![Build Status](https://travis-ci.org/yeluoqiuzhi/any-qs.svg?branch=master)](https://travis-ci.org/yeluoqiuzhi/any-qs)
[![Coverage Status](https://coveralls.io/repos/github/yeluoqiuzhi/any-qs/badge.svg?branch=master)](https://coveralls.io/github/yeluoqiuzhi/any-qs?branch=master)

# any-qs

parse anything look like key=value, different key=value pairs can separate with '&', '#', '?', '\\', ',', or ';'

## install

```shell
npm i -S any-qs
```

## use to parse anything look like key=value

```js
let rawStr = 'nick=yeluoqiuzhi,email=test@email.com; url=http://github.com';
    /**
     * @type {string} string encoded with encodedURI
     */
    let encodedStr = 'nick=yeluoqiuzhi,email=test@email.com;%20url=http://github.com';
anyQs(rawStr);
anyQs(encodedStr);
/*
// two results are the same:

{
  nick: 'yeluoqiuzhi',
  email: 'test@email.com',
  url: 'http://github.com'
}
*/
```
## use to parse url

### decodeURI

```js
const url = 'https://www.baidu.com/?cid=id_34&product=%E5%A4%9A%E5%A4%9A%E6%96%87%E5%AD%97#?value=32&key=key110&system=多多测试';
const params = anyQs(url);
console.log(params);
/*
{
  cid: 'id_34',
  product: '多多文字',
  value: 32,
  key: 'key110',
  system: '多多测试'
}
*/
```

### replace + with one space

```js
const url = 'https://www.google.co.jp/?gfe_rd=cr&ei=2DVeWYrjGo3XqAH_24qQCA#newwindow=1&q=just+a+test+suit';
const params = anyQs(url);
console.log(params);
/*
{
  gfe_rd: 'cr',
  ei: '2DVeWYrjGo3XqAH_24qQCA',
  newwindow: 1,
  q: 'just a test suit'
})
*/
```

### parse number value or not

```js
const url = 'http://www.baidu.com?name=yeluoqiuzhi&born=1994&age=@24&height=174.5';
let params = anyQs(url);
console.log(typeof params.born); // number
console.log(typeof params.height) // number
console.log(params.height) // 174.5

params = anyQs.stringOnly(url);
console.log(typeof params.born); // string
console.log(typeof params.height) // string
console.log(params.height) // 174.5
```

### return empty object when match nothing

```js
const url = 'https://www.google.com';
const params = anyQs(url);
console.log(params);
/*
{}
*/