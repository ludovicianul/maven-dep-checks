These scripts leverage the maven dependency plugin and displays different project dependencies information a friendly CSV manner.

# Display all dependencies (including transitive dependencies)
Running the `check_all_dependencies` script will output a `dependencies_all.csv` file with all project dependencies and their corresponding version.

# Check for duplicates
Running the `check_duplicates` script will output a `dependencies_duplicates.csv` file with all duplicated dependencies. All dependencies must appear only once in `<dependencies/>` or `<dependenciesManagement/>`, so this is an opportunity to remove anything appearing in this file.

# Check for dependencies being used with different versions inside a multi-module maven project
Running the `check_multiple_versions` script will output a `dependencies_mixed_version.txt` file with all dependencies that appear with mixed versions across the project modules. By running `mvn dependency:tree -Dincludes=DEPENDENCY"` for each identified dependency you will get exact information for the exact components that are mixing the versions.

# Check for dependencies used but not declared or unused but declared
Running the `check_used_unused` script will output a `dependencies_used_unused.csv` file with all dependencies that should be reviewed for removal/addition. The decisions should be as follows:

- Dependencies marked as *Used undeclared* must be explicetly declared inside the pom.xml files. This will prevent future unintentional version upgrades that might broke your integration
- Dependencies marked as *Unused declared* must be reviewed for removal. Some might be spring autoconfiguration dependencies which you will want to keep, but others might indeed be residual and must be removed


