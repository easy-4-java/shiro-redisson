# shiro-redisson

![Java CI with Gradle](https://github.com/streamone/shiro-redisson/workflows/Java%20CI%20with%20Gradle/badge.svg)

[![Travis](https://img.shields.io/travis/streamone/shiro-redisson.svg)](https://travis-ci.org/streamone/shiro-redisson)
[![Coverage Status](https://coveralls.io/repos/github/streamone/shiro-redisson/badge.svg?branch=master)](https://coveralls.io/github/streamone/shiro-redisson?branch=master)
[![license](https://img.shields.io/badge/license-MIT%20License-blue.svg)](https://github.com/streamone/shiro-redisson/blob/master/LICENSE)

### Redis based implementations of Apache Shiro's Cache and Session, using [redisson](https://github.com/redisson/redisson) as rich redis client.

### Shiro 3 build

This branch targets Java 17 or later, Apache Shiro 3.0.2, Jakarta Servlet 6.1, and Redisson 3.52.0.
Its Maven coordinate is `io.github.easy4j:shiro-redisson:3.0.x.20261119-SNAPSHOT`.

Run the test suite against a dedicated Redis instance. The tests create and clear cache regions.
Use `mvn verify -Dredis.url=redis://127.0.0.1:6379` to select the instance.
Use `mvn install` with the same property to make the SNAPSHOT available to other local Maven builds.

The default JSON codec preserves the Shiro 3 salt bytes and the principals grouped by realm.
Existing authentication entries written with Shiro 1 class names require a fresh cache namespace during migration.

### Features
* Shiro Cache implementation
  * support cache config according to Spring Cache specification

* Shiro Session implementation
  * serialize attributes of session individually as minimum unit
  * package redis commands in lua script for high performance (reduce round-trip time)  and supporting transaction

* Others
  * support several serialization solutions: JDK Serialization, JSON, Smile, MsgPack, FST and so on
  * support common redis servers mode,  including single server, master-salve replication, sentinel, cluster  