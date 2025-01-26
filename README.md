# Redis

This is a simple Redis client. I used to copy this file to every project so I could use the same client across projects. So this helps me have it one place.

This is not designed to be run as a server, only to be imported and used in your code.

# Installation

```bash
go get github.com/boolow5/redis
```

# Usage

```go
import "github.com/boolow5/redis"

func main() {
    redisDb, err = db.NewRedisDB("", "", 0)
    if err != nil {
        panic(err)
    }

    // to test that it works
    ping, err := redisDb.Ping() // pings the redis server
    if err != nil {
        panic(err)
    }

    ctx := context.Background() // create a context

    redisDb.Set(ctx, "foo", "bar") // sets key: foo to value:bar
    redisDb.SetEx(ctx, "foo", "bar", 100) // sets key: foo to value:bar with an expiration of 100 seconds
    redisDb.Get(ctx, "foo") // gets the value of key: foo
    redisDb.Del(ctx, "foo") // deletes key: foo
    redisDb.Keys(ctx, "*") // gets all keys
    redisDb.Exists(ctx, "foo") // checks if key: foo exists
    redisDb.Expire(ctx, "foo", 100) // sets key: foo to expire in 100 seconds
    redisDb.Incr(ctx, "foo") // increments key: foo by 1
    redisDb.IncrBy(ctx, "foo", 10) // increments key: foo by 10
    redisDb.Decr(ctx, "foo") // decrements key: foo by 1
    redisDb.DecrBy(ctx, "foo", 10) // decrements key: foo by 10
    redisDb.HGet(ctx, "foo")  // gets the value of a hash field
    redisDb.HSet(ctx, "foo", "bar")  // sets the value of a hash field
    redisDb.HDel(ctx, "foo", "bar")  // deletes a hash field
    redisDb.HExists(ctx, "foo", "bar")  // checks if a hash field exists
    redisDb.HGetAll(ctx, "foo")  // gets all hash fields
    redisDb.HIncr(ctx, "foo", "bar")  // increments a hash field by 1
    redisDb.HIncrBy(ctx, "foo", "bar", 10)  // increments a hash field by 10
    redisDb.HDecr(ctx, "foo", "bar")  // decrements a hash field by 1
    redisDb.HDecrBy(ctx, "foo", "bar", 10)  // decrements a hash field by 10
    redisDb.LPush(ctx, "foo", "bar")  // adds an item to the head of a list
    redisDb.LPop(ctx, "foo")  // removes an item from the head of a list
    redisDb.LLen(ctx, "foo")  // gets the length of a list
    redisDb.LRange(ctx, "foo", 0, 10)  // gets a range of items from a list
    redisDb.RPush(ctx, "foo", "bar")  // adds an item to the tail of a list
    redisDb.RPop(ctx, "foo")  // removes an item from the tail of a list
    redisDb.SAdd(ctx, "foo", "bar")  // adds an item to a set
    redisDb.SRem(ctx, "foo", "bar")  // removes an item from a set
    redisDb.IsMemberOfSet(ctx, "foo", "bar")  // checks if an item is in a set

    redisDb.GetKeys("*") // gets all keys
}

```

# Prefix the keys
This is for separating or differentiating keys between different projects. If you have a project called `foo` and another project called `bar`, you can have the keys prefixed with `foo_` and `bar_` so that they don't conflict.

In order to add prefix for your project, set the environment variable APP_NAME to your project name.

```bash
export APP_NAME=foo
```

Then all your keys will in redis will be `foo:*` instead of just `*`.

# Expected environment variables:
All environment variables are optional. If you set any of them make sure you load them in your main function using `github.com/joho/godotenv` or any other package you prefer.

Example:
```go
func main() {
	err := godotenv.Load()
	if err != nil {
		log.Fatal("Error loading .env file")
	}

	log.Printf("Starting %s server...\n", os.Getenv("APP_NAME"))

    // ... your code
}
```

List all the environment variables:
```bash
APP_NAME            # Default ""            | This is the project name and will prefix for all keys
REDIS_HOST          # Default "localhost"   | This is the host of the redis server
REDIS_PORT          # Default 6379          | This is the port of the redis server
REDIS_PASSWORD      # Default ""            | This is the password of the redis server
REDIS_DEFAULT_DB    # Default 0             | This is the default database
```

# License

MIT License

# Author
[boolow5](https://github.com/boolow5)

# Contributing

Please fork this repo and create a pull request.

# Acknowledgements

- [Redis](https://redis.io/)
- [GoRedis](https://github.com/go-redis/redis)
