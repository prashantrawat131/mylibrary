Step 1: Provide the implementation of the library inside the app build.gradle file:

implementation 'surelogin:mylibrary:1.0.2'


Note: 
Target and compile SDK are 33 for the libray.
Do not forget to take internet permission.


Step 2: Create a file at the root of your project. Name it as 'surepass.properties' and insert following lines into the file

usr = COMPANY_USER_NAME
key = AUTH_TOKEN


Step 3: Put this code inside your settings.gradle file outside and above of the dependencyResolutionManagement section:

def surePassProperties = new Properties()
def surePassPropertiesFile = new File('./surepass.properties')
if (surePassPropertiesFile.exists()) {
    surePassPropertiesFile.withReader('UTF-8') { reader ->
        surePassProperties.load(reader)
    }
}
def libName="myLibrary"


Step 4: Put this code inside settings.gradle inside dependencyResolutionManagement section:

   repositories {
        maven {
            name = "GitHubPackages"
            url = uri("https://maven.pkg.github.com/${surePassProperties.get('usr')}/$libName")

            credentials {
                username = surePassProperties.get("usr")
                password = surePassProperties.get("key")
            }
        }
    }



