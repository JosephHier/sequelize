<a name="querychainer"></a>
# Class QueryChainer
[View code](https://github.com/sequelize/sequelize/blob/a3155ec82d64a76ada2aaaadcb09d4161912819d/lib/query-chainer.js#L18)
The sequelize query chainer allows you to run several queries, either in parallel or serially, and attach a callback that is called when all queries are done.

**Deprecated** The query chainer is deprecated, and due for removal soon. Please use [promises](API-Reference-Promise) instead!

***

<a name="add"></a>
## `add(emitterOrKlass, [method], [params], [options])` -> `hi`
[View code](https://github.com/sequelize/sequelize/blob/a3155ec82d64a76ada2aaaadcb09d4161912819d/lib/query-chainer.js#L81)
Add an query to the chainer. This can be done in two ways - either by invoking the method like you would normally, and then adding the returned emitter to the chainer, or by passing the
class that you want to call a method on, the name of the method, and its parameters to the chainer. The second form might sound a bit cumbersome, but it is used when you want to run
queries in serial.

*Method 1:*
```js
chainer.add(User.findAll({
  where: {
    admin: true
  },
  limit: 3
}))
chainer.add(Project.findAll())
chainer.run().done(function (err, users, project) {

})
```

*Method 2:*
```js
chainer.add(User, 'findAll', {
  where: {
    admin: true
  },
  limit: 3
})
chainer.add(Project, 'findAll')
chainer.runSerially().done(function (err, users, project) {

})
```

**Params:**

| Name | Type | Description |
| ---- | ---- | ----------- |
| emitterOrKlass | EventEmitter &#124; Any |  |
| [method] | String |  |
| [params] | Object |  |
| [options] | Object |  |


***

<a name="run"></a>
## `run()` -> `EventEmitter`
[View code](https://github.com/sequelize/sequelize/blob/a3155ec82d64a76ada2aaaadcb09d4161912819d/lib/query-chainer.js#L96)
Run the query chainer. In reality, this means, wait for all the added emtiters to finish, since the queries began executing as soon as you invoked their methods.

***

<a name="runserially"></a>
## `runSerially([options])` -> `EventEmitter`
[View code](https://github.com/sequelize/sequelize/blob/a3155ec82d64a76ada2aaaadcb09d4161912819d/lib/query-chainer.js#L111)
Run the chainer serially, so that each query waits for the previous one to finish before it starts.

**Params:**

| Name | Type | Description |
| ---- | ---- | ----------- |
| [options] | Object |  |
| [options.skipOnError=false] | Object | If set to true, all pending emitters will be skipped if a previous emitter failed |


***

_This document is automatically generated based on source code comments. Please do not edit it directly, as your changes will be ignored. Please write on <a href="irc://irc.freenode.net/#sequelizejs">IRC</a>, open an issue or a create a pull request if you feel something can be improved. For help on how to write source code documentation see [JSDoc](http://usejsdoc.org) and [dox](https://github.com/tj/dox)_