# Why
There are different tools out there which gives you different perspectives of your Maven dependencies, but sometimes you don't need all the fancy stuff and just want a simple and quick way to get part of this information.
This repository contains 6 scripts that leverage the [maven dependency plugin](https://maven.apache.org/plugins/maven-dependency-plugin/) and displays different project dependencies information in a friendly CSV manner.

# Display all dependencies (including transitive dependencies)
Running the `check_all_dependencies` script will output a `dependencies_all.csv` file with all project dependencies and their corresponding version.

# Check dependencies age
Running the `check_age` script will iterate through all your projects dependencies and checks how old is your version compared to the latest available (in months). It will output a `dependencies_age.csv` that you can browse/sort/etc.

# Check for duplicates
Running the `check_duplicates` will check for duplicate dependencies in `<dependencies>` and `<dependenciesManagement>`. It will output a `dependencies_duplicates.csv` file with all duplicated dependencies.

# Check for dependencies being used with different versions inside a multi-module maven project
Running the `check_multiple_versions` script will output a `dependencies_mixed_version.txt` file with all dependencies that appear with mixed versions across the project modules. By running `mvn dependency:tree -Dincludes=DEPENDENCY"` for each identified dependency you will get exact information for the exact components that are mixing the versions.

# Check for dependencies used but not declared or unused but declared
Running the `check_used_unused` script will output a `dependencies_used_unused.csv` file with all dependencies that should be reviewed for removal/addition. When reviewing these dependencies, you might consider the following:
- Dependencies marked as *Used undeclared* must be explicitly declared inside the `pom.xml` files. This will prevent future unintentional version upgrades that might broke your integration.
- Dependencies marked as *Unused declared* must be reviewed for removal. Some might be spring autoconfiguration dependencies which you will want to keep, but others might indeed be residual and must be removed.
- Ignore it as not relevant (you might rely on `spring-boot-starters` for example or similar concepts)


