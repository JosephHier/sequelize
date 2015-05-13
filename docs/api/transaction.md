<a name="transaction"></a>
# Class Transaction
[View code](https://github.com/sequelize/sequelize/blob/a3155ec82d64a76ada2aaaadcb09d4161912819d/lib/transaction.js#L11)
The transaction object is used to identify a running transaction. It is created by calling `Sequelize.transaction()`.

To run a query under a transaction, you should pass the transaction in the options object.

***

<a name="solation_level"></a>
## `SOLATION_LEVEL`
[View code](https://github.com/sequelize/sequelize/blob/a3155ec82d64a76ada2aaaadcb09d4161912819d/lib/transaction.js#L46)
The possible isolations levels to use when starting a transaction.
Can be set per-transaction by passing `options.isolationLevel` to `sequelize.transaction`.
Default to `REPEATABLE_READ` but you can override the default isolation level by passing `options.isolationLevel` in `new Sequelize`.

```js
{
  READ_UNCOMMITTED: "READ UNCOMMITTED",
  READ_COMMITTED: "READ COMMITTED",
  REPEATABLE_READ: "REPEATABLE READ",
  SERIALIZABLE: "SERIALIZABLE"
}
```


***

<a name="oc"></a>
## `OC`
[View code](https://github.com/sequelize/sequelize/blob/a3155ec82d64a76ada2aaaadcb09d4161912819d/lib/transaction.js#L70)
Possible options for row locking. Used in conjuction with `find` calls:

```js
t1 // is a transaction
Model.findAll({
  where: ...
}, {
  transaction: t1,
  lock: t1.LOCK.UPDATE,
  lock: t1.LOCK.SHARE,
  lock: t1.LOCK.KEY_SHARE, // Postgres 9.3+ only
  lock: t1.LOCK.NO_KEY_UPDATE // Postgres 9.3+ only
})
```

***

<a name="commit"></a>
## `commit()` -> `this`
[View code](https://github.com/sequelize/sequelize/blob/a3155ec82d64a76ada2aaaadcb09d4161912819d/lib/transaction.js#L82)
Commit the transaction


***

<a name="rollback"></a>
## `rollback()` -> `this`
[View code](https://github.com/sequelize/sequelize/blob/a3155ec82d64a76ada2aaaadcb09d4161912819d/lib/transaction.js#L103)
Rollback (abort) the transaction


***

_This document is automatically generated based on source code comments. Please do not edit it directly, as your changes will be ignored. Please write on <a href="irc://irc.freenode.net/#sequelizejs">IRC</a>, open an issue or a create a pull request if you feel something can be improved. For help on how to write source code documentation see [JSDoc](http://usejsdoc.org) and [dox](https://github.com/tj/dox)_