# WIP

# swagger-grails
Generate and view Swagger documentation for your Grails app.

## Built With
* Grails 3.1.5
* Swagger Core 1.5.15
* Swagger UI 3.0.18

## Installation
Add this line to the `dependencies` block in your `build.gradle` file:
    
    compile "org.grails.plugins:swagger-grails:0.1"
    
## Usage
Given the following UrlMappings.groovy ...
```groovy
class UrlMappings {
    static mappings = {
        "/$controller/$action?/$id?(.$format)?" {
            constraints {
                // apply constraints here
            }
        }
        
        "/authors"(resources: 'author')
    }
}
```

... and the following AuthorController.groovy ...
```groovy
class AuthorController {
    def index() {/*...*/ }

    def save(AuthorCommand authorCommand) {/*...*/ }

    def show(String id) {/*...*/ }

    def delete(String id) {/*...*/ }

    def update(String id) {/*...*/ }

    def patch(String id) {/*...*/ }

    def custom(String name, int age) {/*...*/ }
}

class AuthorCommand implements Validateable {
    String name
}
```

... will generate Swagger documentation like this :

![Example Swagger Doc](src/test/resources/author-controller.png?raw=true)

Also any Swagger annotations that are manually added to actions in  controllers
will be used when generating the Swagger documentation. So you could let the
plugin do what it does by default and then enhance the actions with responses,
authorizations, etc...

## Configuration
The plugin also exposes the ability to customize the Swagger instance that is used.

The following resources.groovy ...
```groovy
    swagger(Swagger) {
        securityDefinitions = ["apiKey": new ApiKeyAuthDefinition("apiKey", In.HEADER)]
        security = [new SecurityRequirement().requirement("apiKey")]
    }
```
... will create the default swagger instance that the plugin will use.  It also sets the
 security definition and security block.  Together these two allow a header "apiKey"
 to be attached to all calls from the front end.
 
 Any of the fields on the Swagger object can be configured this way as well.  For some more
 info on what can be configured the [OpenAPI-Specification](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md#schema) describes what the Swagger
 object can contain.

## Running the plugin locally
The plugin source contains more examples of what types of configuration you
can apply to controllers and actions :

##### Prerequisites
* Java 8
* Grails 3.1.5

##### Running
* Clone or download the repo
* Run `grails run-app`
* Navigate to `http://localhost:8080/swagger`

