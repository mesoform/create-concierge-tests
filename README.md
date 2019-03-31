# Role to create tests for a Concierge managed application 

## Using this role

Generally this role should be wrapped by a [top level playbook for generating application 
config](https://github.com/mesoform/concierge-app-playbook) to be built into the image. However, if ran manually, there is a 
`concierge-tests.yml` file which can be passed to `ansible-playbook` but many of the required variables and files will need to be passed at runtime.

Primarily the role simply pulls all of your application variables and scripts together into a set Ansible tasks used for performing system and integration tests on a running container which includes your application. 

CURRENTLY, there are no required variables to run this as a stand alone playbook but as we develop more tests there may be some which are. These will be able to be set using `ansible-playbook --extra-vars some_key=some_value`.

## Docker Compose files
This playbook makes use of the [multiple compose files principle](https://docs.docker.com/compose/extends/#extending-services)
 as well as the `extends` keyword for extending services.  It will autogenerate a `docker-compose-override.yml`
 file which will automatically be read by `docker-compose up` and can be used for integration tests. 
 It will also create a `docker-compose-units.yml` file which can be passed in with `-f docker-compose-units.yml` 
 and used for running unit tests of your application and ran without the containerpilot `entrypoint`.
 The general idea behind these tests is you will have another file where you define your specific test
 requirements defined in a `service` named the same as your application service and makes use of the
 `extends` keyword for defining specific commands (e.g scripts) for your tests  

## Testing the playbook
Add a test tag to the tasks you want to test and run `ansible-playbook -vv concierge-tests.yml -t test`

However, because it's generally unlikely this role will be used on its own much, and because it is so easy, we recommend
 [testing whilst integrated as a submodule](https://github.com/mesoform/concierge-app-playbook/blob/master/README.md#submodules)

`-----------------------------------------------------------------------------------------------------------------`
Template by [Mesoform Limited](http://www.mesoform.com)