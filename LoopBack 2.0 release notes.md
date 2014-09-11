## Yeoman generators

For LoopBack 2.0, the Command-line tool, `[slc loopback](http://docs.strongloop.com/pages/viewpage.action?pageId=3836281)`, now uses Yeoman generators to create and scaffold applications.  The `slc lb` and `slc example` commands are now deprecated.

## ExpressJS 4.x

LoopBack 2.0 uses ExpressJS v4.x, which introduces some major backwards-incompatible changes. For more information, see [ExpressJS 4.0: New Features and Upgrading from 3.0](http://scotch.io/bar-talk/expressjs-4-0-new-features-and-upgrading-from-3-0).  For instructions on migrating your existing app to LoopBack 2.0, see [Migrating existing apps to version 2.0](/display/LB/Migrating+existing+apps+to+version+2.0).

## New project structure

LoopBack 2.0 has a [new canonical project structure](/display/LB/Project+layout+reference).  Although you're not required to use this structure, when you create an app with [slc loopback](/display/SLC/slc+loopback), it will have the new structure.  And if your app does have the new structure, you can use the Yeoman generators to add new models, properties, data sources, and access control settings.

### Support for external configuration

Applications now have greater flexibility in managing application configuration for multiple environments (for example: development, staging, and production).  For example, you can have a `config.json` with development settings, `config.staging.json` with settings for the staging environment, and `config.production.json` with settings for production.

## New object `PersistedModel`

The base `Model` class is now specifically for defining data structures. `PersistedModel` is the default class for models defined with `app.model(name, ...);` and `models.json`.

Note: loopback 1.x comes with `DataModel`, which is a predecessor of `PersistedModel`. The `DataModel` is no longer available in loopback 2.0.

## Bootstrapper was moved to its own module

The implementation of `app.boot` was moved to the module `loopback-boot`. The 1.x versions are backwards compatible with `app.boot`, the current 2.x versions are using the new project layout.

## Email connector uses nodemailer 1.x

See [http://www.nodemailer.com/](http://www.nodemailer.com/) for details.

## The method `loopback.getModel` throws for unknown model names

In loopback 1.x, `loopback.getModel('unknown-name')` returns `undefined`. In loopback 2.x, the method throws an error instead. Use `loopback.findModel` if you need the old semantics.

## Remote methods

The function `loopback.remoteMethod()` is deprecated along with attaching remote configuration directly to model objects. Instead you should use the actual `SharedMethod` object.

Now, define a remote method by calling the `remoteMethod()` method on the model, for example, as follows:

```js
MyModel.greet = function(msg, cb) {
  cb(null, &#39;greetings... &#39; + msg);
}

MyModel.remoteMethod(
  &#39;greet&#39;,
  {
    accepts: [{arg: &#39;msg&#39;, type: &#39;string&#39;}],
    returns: {arg: &#39;greeting&#39;, type: &#39;string&#39;}
  }
);
```

NOTE: Remote instance method support is also now deprecated. Use static methods instead. If you absolutely need it, you can set `options.isStatic = false`.
Remote instance methods will likely not be supported at all in future releases.</span>


## New loopback-component modules

Several modules used by LoopBack have been renamed.
<table class="confluenceTable"><tbody><tr><th class="confluenceTh">Version 1</th><th class="confluenceTh">Version 2</th></tr><tr><td class="confluenceTd">loopback-passport</td><td class="confluenceTd">loopback-component-passport</td></tr><tr><td class="confluenceTd">loopback-storage-service</td><td class="confluenceTd">loopback-component-storage</td></tr><tr><td class="confluenceTd">loopback-push-notification</td><td class="confluenceTd">loopback-component-push</td></tr></tbody></table></div>
