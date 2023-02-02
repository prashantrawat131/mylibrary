# Steps to implement myLibrary


**Step 1:** Provide the implementation of the library inside the app build.gradle file:

        implementation 'surelogin:mylibrary:1.0.2'


>Note:
>Target and compile SDK are 33 for the library.
>Do not forget to take internet permission.


**Step 2:** Open the file 'local.properties' (at the root of your app) and insert the following lines into the file

        usr = prashantrawat131
        key = READ_GITHUB_PACKAGE_TOKEN
        
>Note: This READ_GITHUB_PACKAGE_TOKEN is generated inside the github developer settings. Please generate this token in order to use the library.


**Step 3:** Put this code inside your *settings.gradle* file outside and above of the dependencyResolutionManagement section:

        
        def githubProperties = new Properties()
        def githubPropertiesFile = new File('./local.properties')
        if (githubPropertiesFile.exists()) {
            githubPropertiesFile.withReader('UTF-8') { reader ->
                githubProperties.load(reader)
            }
        }
        def libName="myLibrary"


**Step 4:** Put this code inside settings.gradle inside dependencyResolutionManagement section:

        repositories {
                maven {
                        name = "GitHubPackages"
                        url = uri("https://maven.pkg.github.com/${githubProperties.get('github_usr')}/$libName")

                credentials {
                        username = githubProperties.get("github_usr")
                        password = githubProperties.get("github_key")
                        }
                }
        }

------------------------------------------------------------------------------------------------

# How to use the library

Inside your activity simply put this line inside the onCreate method or inside some button click listener:

        startActivity(Intent(this, ImageActivity::class.java))


