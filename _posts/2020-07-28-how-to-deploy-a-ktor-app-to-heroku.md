---
layout: post
title: "How to deploy a Ktor app to Heroku ?"
date: 2020-07-28 14:05:32 +0700
categories: Programming
---

`Heroku` is a great cloud platform that allow you to deploy your own pet projects quickly. When I started with a Ktor project, I really want to deploy my project to the Internet to use it for my Android projects as a simple mocking API. However, there isn't any good tutorial for this work. So I referenced some tutorial for java project with Gradle to deploy my project to Heroku. And finally I success. So this is my brief.



## 1. Initialize Ktor project

First of all, install IntelliJ then install `Ktor` plug-in. Set up a new project with Ktor as normal (you can reference [this link](https://ktor.io/quickstart/index.html)).

Please confirm that your `Application.kt` file contains following code:

```kotlin
@Suppress("unused") // Referenced in application.conf
fun Application.module() {

    routing {
        get("/") {
            call.respondText("HELLO WORLD!", contentType = ContentType.Text.Plain)
        }
    }
}
```

We want to show the text "HELLO WORLD!" when visit the website.

Run project to confirm this works fine.



## 2. Config Gradle for Heroku

We use **Shadow** plug-in to build project to a .jar file. So please add below code to your `build.gradle` file:

```groovy
buildscript {
    repositories {
        maven {
            url "https://plugins.gradle.org/m2/"
        }
    }
    
    dependencies {
        classpath "com.github.jengelman.gradle.plugins:shadow:5.2.0"
    }
}

apply plugin: "com.github.johnrengelman.shadow"

shadowJar {
    manifest {
        attributes 'Main-Class': mainClassName
    }
}
```

The `shadowJar` block provide a gradle task with same name. So when we run `./gradlew shadowJar`, a .jar file contain your project name will be created. Suppose you create project with name `example`, if you run `./gradlew shadowJar`, the file created has name `example-0.0.1.jar`, it was contained in `build/libs/` directory.



## 3. Config Heroku Process file

Create a file with name `Procfile` in your root project contains below content:

```
web: java -jar build/libs/example-0.0.1-all.jar
```

Heroku will run the command after `web:` to start the web. By adding this line, Heroku runs the .jar file was built.

Everything is nearly done, now run below command to commit project source code:

```bash
git init
git add .
git commit -m "Init project"
```



## 4. Install HerokuCLI

- Install [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli). For Ubuntu 16+, run below command in terminal:

```bash
sudo snap install --classic heroku
```

- Navigate to your project in the root folder, run `heroku login` and follow the steps.
- Run `heroku create` to initialize your backend application.
- **Important**: Run following command to let Heroku use Gradle Task `shadowJar` to build .jar file.

```bash
 heroku config:set GRADLE_TASK="shadowJar"
```

- Use `git push heroku master` to push your application on server.
- Start your Procfile command launching `heroku ps:scale web=1`. Your backend is now online and ready for use.
- To open heroku remote site, run `heroku open`, you can also use `heroku local web` to run the web on local.



That's all, hope this help. You can see my site here: [https://peaceful-depths-96000.herokuapp.com/](https://peaceful-depths-96000.herokuapp.com/)
