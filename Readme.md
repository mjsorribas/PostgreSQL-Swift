Connect to your PostgreSQL database. Run queries. All natively in Swift.

### Usage

#### Connection

```swift
let parameters = ConnectionParameters(
  host: "123.123.123.123",
  port: "9000",
  databaseName: "banana_pantry",
  login: "mehungry",
  password: "reallyhungrygotnopatience"
)
let connection = try Database.connect(parameters: parameters)
```

#### Environment variables

Your database configuration should not be in your application's source. Connecting to the database becomes as easy as:

```swift
let connection = try Database.connect()
```

Configuration is automatically loaded from default PostgreSQL environment variables.

```shell
export PGHOST 123.123.123.123
export PGPORT 9000
export PGDATABASE banana_pantry
export PGUSER mehungry
export PGPASSWORD reallyhungrygotnopatience
```

#### Queries and results

```swift
let result = try connection.execute("SELECT color, is_tasty, length FROM bananas")
for row in result.rows {
  let color = row["color"] as! String
  let isTasty = row["is_tasty"] as! Bool
  let length = row["length"] as! Int
  let banana = Banana(color: color, isTasty: isTasty, length: length)
}
```

### Development

#### Setup
1. Install dependencies
  1. Xcode 7+
  1. `brew cask install dockertoolbox`
1. initialize postgres docker container
  1. `make development.setup`
1. Run tests
  1. `make test`

### Roadmap

[We are tracking our roadmap with a GitHub issue](https://github.com/stepanhruda/Elephant/issues/5)
