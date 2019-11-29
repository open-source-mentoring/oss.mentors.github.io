

# Just push it

Often times, developers get blocked by long builds, test, etc. In an ideal world, you'd figure out why this is taking so long and work out better caching. In reality, that's not so easy.

The pain here goes away with good CICD infrastructure and TDD practices. In this world, you can easily parallelize builds and tests such that you don't need to sit around waiting for things to finish.

## Test Driven Development

The concept is simple. Write your tests first.

In practice, this is not always super easy, at least for me. I stuggle with front-end tdd, but I find that front-end has other strategies that work well for me. In backend, I get a huge leg up from TDD. The thing is, that everyone always, **always** checks if the code they wrote works. Sometimes though, they do that without writing a real test.

I catch myself testing code by,
* Running it in commandline
* Copy paste into an interpreter
* Print statements

Each of these should just become a test. Honestly the only thing that blocks me, and others I work with, is just setting up the test infrastructure. But just do it, and be done.

## Unit test watcher

If your tests run really quickly, or you separate integ and unit tests (<-- good idea too), then you can have something continuously execute your tests. I often run commands like this,

```
watch -n1 pytest tests
```

which will continuously run your tests, even as you switch branches or make changes. This way you can interactively develop. The CICD pipeline become powerful for longer running builds and/or tests.

## Cost of CICD

Once you have tests, you need a CICD server. For any serious work, pricing is nothing. For example, [AWS CodeBuild Pricing](https://aws.amazon.com/codebuild/pricing/) is,

> Build minutes = 100 builds * 5 minutes = 500 build minutes
> Build minutes – Free tier build minutes = Monthly billable build minutes = 500 – 100 = 400 build minutes
> Monthly build charges = 400 build minutes * $0.005 = $2

Plus the setup time. Let's say 2hrs (which is exagerrated)
> $2 + $30/hrs * 2 = $62

Or, you pay your developer to sit there at stare at the build and tests,

> Build minutes = 100 builds * 5 minutes = 500 build minutes
> Monthly build charges = 500 build minutes * $30/hrs = $250

And I hope your dev is paid more than $30/hrs.

## Push, switch branch, push

Once you have a CI/CD server, you can off load your builds to that machine. My workflow is typically,

```
git checkout -b feature-set-A
... add all the tests I want to ultimately pass ...
git checkout -b feature-A-a
... implement ...
git push origin feature-A-a
git checkout -b feature-A-b
... implement ...
git push origin feature-A-b
git checkout -b feature-A-c
... implement ...
git push origin feature-A-c
```

At this time, some of your branches will be done building in CI/CD, so you check the results and rotate branches again.

## Summary

I use CICD pipelines regularly for development. I find them a powerful way to offload work and time on my part.