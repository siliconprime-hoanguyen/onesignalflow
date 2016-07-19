# OneSignal flow
API routes to be used
  1.  'https://onesignal.com/api/v1/players' // to register a device
  2.  'https://onesignal.com/api/v1/notifications' //to send push notification

Steps
  
  1. User sends device token to our API server.
  2. Server register user device by calling API 1 with body
  
  ```javascript
    {
      device_type: 0, //0 for ios, 1 for android
      identifier: 'deviceAddress',
      app_id: appId,
      tags: {
        userId: 'ourdesireuserid'
      },
      test_type: 1 //BEWARE, non-production environment is 1, production environment is 2
    }
  ```
  Doc: https://documentation.onesignal.com/docs/players-add-a-device
  
  
  3. Calling sending push notification when needed using API 2 with body
  
  ```javascript
  {
    contents: {
      en: 'message from dropin' //title
    },
    data: {data1: 'abc'},  //data to send
    //include_player_ids: [id], //Use this only if sending to specfic users, in this case, we use tag 
    tags:[{ //this is our registed tags in the API register above
      "key": "userId", 
      "relation": "=",
      "value": "ourdesireuserid" 
    }]
    app_id: appId,
    headings: {
      en: 'test headings'
    }
  }
  ```
  
  Doc: https://documentation.onesignal.com/docs/notifications-create-notification
  

