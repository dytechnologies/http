# Migration Guide

This guide will help you to migrate from [Axios Module](https://github.com/nuxt-community/axios-module).

:::tip Note
The nuxt-community axios module is still supported and maintained. The HTTP module uses newer web technologies like fetch which might be beneficial
:::

## Differences
- There is no scope for [`setHeader`](/api/#setheader), [`setToken`](/api/#settoken)<br/>
_When calling these methods they apply to the global scope and are used for all future requests_
- The axios hooks `onRequestError` and `onResponseError` are unified<br/>
_Use the [`onError`](/api/#onerror) hook instead_
- The http module does not have a `debug` option like the axios module<br/>
_You can setup a basic logger using the [`onRequest`](/api/#onrequest) hook_
- Progress bar integration is not supported (for the moment)<br/>
_This option may be added again once [`PR #34: Add 'onProgress' option`](https://github.com/sindresorhus/ky/pull/34) for ky is merged_

## Response body parsing

Axios automatically transforms response bodies to JSON, if you wish to keep that behaviour you will 

- either need to switch to using the `$` prefixed methods 

```diff
-- const resJson = await this.$axios.get('/url')
++ const resJson = await this.$http.$get('/url')
```

- or explicitly call [`json`](https://developer.mozilla.org/en-US/docs/Web/API/Body/json) on the Response:

```diff
-- const resJson = await this.$axios.get('/url')
++ const resJson = await this.$http.get('/url').json()
```

If you are already using `$` prefixed shortcuts for making requests that return JSON, you can keep using them.

```diff
-- const resJson = await this.$axios.$get('/url')
++ const resJson = await this.$http.$get('/url')
```