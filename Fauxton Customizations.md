# Fauxton customizations
## REPOSITORY NOTES:
- In `couchdb` repository, base is `./src/fauxton/app/`
- In `couchdb-fauxton` repository, base is `./app/`

## CODE MODIFICATIONS
- ***`./constants.js`***
  > **This will show more databases (at the all_dbs screen) and documents.**
  >
  > **Change `DEFAULT_PAGE_SIZE: 20` to `DEFAULT_PAGE_SIZE: 500` and `DOCUMENT_LIMIT: 20` to `DOCUMENT_LIMIT: 500`**
  >
  ```js
  MISC: {
    TRAY_TOGGLE_SPEED: 250,
    DEFAULT_PAGE_SIZE: 500
  },

  DATABASES: {
    DOCUMENT_LIMIT: 500
  },
  ```

- ***`./addons/documents/index-results/components/pagination/PerPageSelector.js`***
  > This will allow you to choose more than 100 documents to be displayed at once, and will enable the previous change (setting documents to default at 500)
  >
  > **In `PerPageSelector.defaultProps`, change `options: [5, 10, 20, 30, 50, 100]` to `options: [5, 10, 20, 30, 50, 100, 200, 500, 1000]`**
  ```js
  PerPageSelector.defaultProps = {
    label: 'Documents per page: ',
    options: [5, 10, 20, 30, 50, 100, 200, 500, 1000]
  };
  ```

- ***`./addons/fauxton/notifications/notifications.js`***
  or
  ***`./addons/fauxton/notifications/components/Notification.js`***
  > **This will vastly speed up the notification message timeout**
  >
  > **In `static defaultProps`, change `visibleTime: 8000` to `visibleTime: 1537`**
  ```js
  static defaultProps = {
    type: 'info',
    visibleTime: 1537,
    escape: true
  };
  ```

