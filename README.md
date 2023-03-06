# AudienceM Web SDK v2

## Quick start
Insert between your page's `<head></head>` tags
```html
<script
  async="async" type="text/javascript"
  src="//sdk.audiencem.co.kr/datarius.min.js"
  crossorigin="anonymous"></script>
```

## Supported functions

### Identify
```js
analytics.identify('userId', {
  name: '홍길동',
  email: 'gildong@fles.co.kr'
});
```

The Identify method follows the format below:

`analytics.identify([userId], [traits], [options], [callback]);`

The Identify call has the following fields:
| Field    |          | Type     | Description                                                                                                                                                                             |
|----------|----------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| userId   | optional | String   | The database ID for the user. If you don’t know who the user is yet, you can omit the userId and just record traits. You can read more about identities in the identify reference.      |
| traits   | optional | Object   | A dictionary of traits you know about the user, like email or name. You can read more about traits in the identify reference.                                                           |
| options  | optional | Object   | A dictionary of options. For example, enable or disable specific destinations for the call. Note: If you do not pass a traits object, pass an empty object (as an ‘{}’) before options. |
| callback | optional | Function | A function executed after a timeout of 300 ms, giving the browser time to make outbound requests first.                                                                                 |


### Track
```js
analytics.track('구독신청', {
  plan: '1년'
});

analytics.track('관심하기', {
  title: '오늘의 운세',
  // ... 자유로운 데이터 주차 가능
  // ... You can add other data you need here
});
```

The Track method lets you record actions your users perform. You can see a track example in the Quickstart guide or find details on the track method payload.

The Track method follows the format below:

`analytics.track(event, [properties], [options], [callback]);`

The track call has the following fields:

| Field    |          | Type     | Description                                                                                                                                                                             |
|----------|----------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| userId   | optional | String   | The database ID for the user. If you don’t know who the user is yet, you can omit the userId and just record traits. You can read more about identities in the identify reference.      |
| properties   | optional | Object   |Optional. A dictionary of properties for the event. If the event was 'Added to Cart', it might have properties like `price` and `productType`.                                                           |
| options  | optional | Object   | A dictionary of options. For example, enable or disable specific destinations for the call. Note: If you do not pass a traits object, pass an empty object (as an `{}`) before options. |
| callback | optional | Function | A function executed after a timeout of 300 ms, giving the browser time to make outbound requests first.                                                                                 |

### TrackForm

```js
var form = document.getElementById('signup-form');

analytics.trackForm(form, 'Signed Up', {
  plan: 'Premium',
  revenue: 99.00
});
```

trackForm is a helper method that binds a track call to a form submission. The trackForm method inserts a timeout of 300 ms to give the track call more time to complete. This is useful to prevent a page from redirecting before the track method could complete all requests.

The trackForm method follows the format below.

`analytics.trackForm(form, event, [properties])`

### Page

```js
analytics.page('Pricing', {
  title: 'My Overridden Title',
  url: 'https://borra.today/pricing',
  path: '/pricing/view',
  referrer: 'https://borra.today/warehouses'
});
```

The Page method lets you record page views on your website, along with optional extra information about the page viewed by the user.

You can call it more than once if needed, for example, on virtual page changes in a single page app.

We included a Page call by default.

The page method follows the format below.

`analytics.page([category], [name], [properties], [options], [callback]);`

| Field      | Type     | Description |                                                                                                                                                                                                                                |
|------------|----------|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| category   | optional | String      | The category of the page. Useful for cases like ecommerce where many pages might live under a single category. Note: if you pass only one string to page it is assumed to be name. You must include a name to send a category. |
| name       | optional | String      | The name of the page.                                                                                                                                                                                                          |
| properties | optional | Object      | A dictionary of properties of the page. Note: Analytics.js collects url, title, referrer and path are automatically. This defaults to a canonical url, if available, and falls back to document.location.href.                 |
| options    | optional | Object      | A dictionary of options. For example, enable or disable specific destinations for the call. Note: If you do not pass a properties object, pass an empty object (like ‘{}’) before options.                                     |
| callback   | optional | Function    | A function that runs after a timeout of 300 ms, giving the browser time to make outbound requests first.                                                                                                                       |

### Group

The Group method associates an identified user with a company, organization, project, workspace, team, tribe, platoon, assemblage, cluster, troop, gang, party, society or any other collective noun you come up with for the same concept.

This is useful for tools like Intercom, Preact, and Totango, as it ties the user to a group of other users.

The Group method follows the format below.

`analytics.group(groupId, [traits], [options], [callback]);`

| Field    | Type     | Description                                      |                                                                                                                                                                                            |
|----------|----------|--------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| groupId  | String   | The Group ID to associate with the current user. |                                                                                                                                                                                            |
| traits   | optional | Object                                           | A dictionary of traits for the group. Example traits for a group include address, website, and employees.                                                                                  |
| options  | optional | Object                                           | A dictionary of options. For example, enable or disable specific destinations for the call. Note: If you do not pass a properties object, pass an empty object (like ‘{}’) before options. |
| callback | optional | Function                                         | A function that runs after a timeout of 300 ms, giving the browser time to make outbound requests first.                                                                                   |

### Alias

The Alias method combines two unassociated user identities. Not often used. Use only when `identify()` fails to combine two different identities in your result.

The Alias method follows the format below:

`analytics.alias(userId, [previousId], [options], [callback]);`

| Field      | Type     | Description                                          |                                                                                                                 |
|------------|----------|------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| userId     | String   | The new user ID you want to associate with the user. |                                                                                                                 |
| previousId | optional | String                                               | The previous ID that the user was recognized by. This defaults to the currently identified user’s ID.           |
| options    | optional | Object                                               | A dictionary of options. For example, enable or disable specific destinations for the call.                     |
| callback   | optional | Function                                             | A function that is executed after a timeout of 300 ms, giving the browser time to make outbound requests first. |
