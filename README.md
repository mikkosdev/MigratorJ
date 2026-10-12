# MigratorJ

![Java](https://img.shields.io/badge/Java-25+-blue?logo=openjdk&logoColor=white)
![Maven](https://img.shields.io/badge/build-Maven-red)
![License](https://img.shields.io/badge/License-AGPLv3-purple.svg)

WORK IN PROGRESS - NOT YET RELEASED.

## How is this different from other tools?

- GPL3 license
- Very simple and small library
- Abstract, meaning it only provides the concept of a migration and a migration runner, but not the concrete implementations for different databases
- Each migration is responsible for its own implementation
- You can mix and match different databases as you will
- The migration classes are just Java classes that can have any code in them
- The only thing required is to set up the bookkeeping database that saves the migrations that have been run to avoid running the migrations multiple times

## How it works

The idea is that the MigratorJ runs all the migration classes it finds in a package, and saves each run migration in a database table so that they won't be run again the next time.

- You set up the MigrationJ database configuration.
  - This is needed for the bookkeeping of run migrations.
- You create a migration classes that extend the `AbstractMigration` superclass.
- You add the MigrationJ `runMigrations()` method to your application initialization.
- Each migration class will have `up()` and ´down()` methods.
  - The `up()` method is what adds/creates what you need in the database.
  - The `down()` method removes what the `up()` added.
- You can set the last migration to be run and migrations beyond that will have their `down()` called.

## Best practices

- Name migration classes with prefix 'M001_' where:
  - 'M' is needed for it to be a valid Java class name
  - The '001' part is what keeps them sorted alphabetically
  - The underscores can make the names more readable, but are not required.
- In the migration classes, utilize the same persistence code as elsewhere in the code.
- Make sure you have model classes for the data that you'll modify with the migrations.
- Use _Repository Pattern_ for the different models.

# Tips

- Look at the www.github.com/mikkosdev/MegalomaniaK example app to see a simple project that uses this library.
