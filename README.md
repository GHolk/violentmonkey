# Purplemonkey
Just like [Violentmonkey], but with more unsafe API.

[Violentmonkey]: https://violentmonkey.github.io/api/gm/

## Purplemonkey API
only the additional api from violent monkey is listed.
other api are same to the violent monkey in the same version.

### GM_messageExtension(id, payload)
send message to other extension's `browser.runtime.onMessageExternal` handler.

* id: the id of the destination extension.
* payload: the data to send. must be structure clonable.
* return: a promise resolve to the response or reject to error.

to use this api, you have to add `@connect web-extension://id`
in the userscript's meta field.
where id is the extension that you want to send message with.
the special `web-extension://*` allow to connect to all the other extensions.

### GM_webextEval(code, args)
eval string or function in violent monkey background script.

* String(code): the code is call as
  `(function (...args) {return eval(code)})(...args)`,
  so the last statement is return.

* Function(code): code is stringify and reconstructed as function in background.
  stringify so any closure will not work.

  if this is a method, you should make sure that it could be stringify 
  and reconstruct correctly.
  
  async could work.

* args: an argument array that structure clonable.

* return: a promise resolve to result or reject to error.
