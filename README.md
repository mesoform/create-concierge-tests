# Role to create tests for a Concierge managed application 

## Using this role

Generally this role should be wrapped by a [top level playbook for generating application 
config](https://github.com/mesoform/concierge-app-playbook) to be built into the image. However, if ran manually, there is a 
`concierge-tests.yml` file which can be passed to `ansible-playbook` but many of the required variables and files will need to be passed at runtime.

Primarily the role simply pulls all of your application variables and scripts together into a set Ansible tasks used for performing system and integration tests on a running container which includes your application. 

CURRENTLY, there are no required variables to run this as a stand alone playbook but as we develop more tests there may be some which are. These will be able to be set using `ansible-playbook --extra-vars some_key=some_value`.

## Testing
Add a test tag to the tasks you want to test and run `ansible-playbook -vv concierge-tests.yml -t test`

However, because it's generally unlikely this role will be used on its own much, and because it is so easy, we recommend
 [testing whilst integrated as a submodule](https://github.com/mesoform/concierge-app-playbook/blob/master/README.md#submodules)

`-----------------------------------------------------------------------------------------------------------------`
Template by [Mesoform Limited](http://www.mesoform.com)