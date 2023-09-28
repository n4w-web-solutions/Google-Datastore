# GCP Datastore

GCP Datastore is a library for querying Google Datastore, naturally (default) or through GQL (Google Query Language) or even with GQL Aggregation

## Installation

Use the package manager [npm](https://docs.npmjs.com/about-npm) to install GCP Datastore.

```bash
npm i @N4W-Web-Solutions/gcp-datastore@1.0.0
```

## Usage dafault Query

```javascript

const gcpDatastore = require("@N4W-Web-Solutions/gcp-datastore")
const gcpDS = new gcpDatastore({projectId: '[PROJECT_ID]', keyFilename: '[/PATH/TO/KEYFILE.json]'})

async function run () {
    const res = await gcpDS.query('[KIND_NAME]', null, null, null, null, 1)
    console.log(res)
}

run()

```

Results in ``res[0]``
Pagination information in ``res[1]``

## Usage GQL Query

```javascript

const gcpDatastore = require("@N4W-Web-Solutions/gcp-datastore")
const gcpDS = new gcpDatastore({projectId: '[PROJECT_ID]', keyFilename: '[/PATH/TO/KEYFILE.json]'})

async function run () {
    const entities = await ds.gqlQuery("SELECT * FROM `[KIND_NAME]` LIMIT @limit", {
        limit: {
            value: {
                integerValue: 1
            }
        }
    })
    console.log(entities)
}

run()

```

Results in ``entities.batch.entityResults``

## Usage GQL AGGREGATION Query

```javascript

const gcpDatastore = require("@N4W-Web-Solutions/gcp-datastore")
const gcpDS = new gcpDatastore({projectId: '[PROJECT_ID]', keyFilename: '[/PATH/TO/KEYFILE.json]'})

async function run () {
    const entities = await ds.gqlQuery("AGGREGATE COUNT(*) AS total OVER (SELECT * FROM `[KIND_NAME]` WHERE param1 = @param1 AND param2 = @param2 LIMIT @limit OFFSET @offset)", {
        param1: {
            value: {
                stringValue: "test"
            }
        },
        param2: {
            value: {
                integerValue: 5
            }
        },
        offset: {
            value: {
                integerValue: 10
            }
        },
        limit: {
            value: {
                integerValue: 1
            }
        }
    })
    console.log(entities)
}

run()

```

Results in ``entities.batch.aggregationResults``


## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)