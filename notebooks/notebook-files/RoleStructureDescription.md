#### Description
---
##### defaults
- `main.yml` will contain all values for variables that don't have a definition elsewhere in the role/run. Defaults have the lowest precedence </br> of any type of variable assignment in Ansible. That is, if the variable is assigned a value anywhere else, it will override the default value.

##### library
- Will include any non-Ansible code that is used elsewhere in the role. At Chevron, this consists of custom Ansible Modules but may also </br> include other Python, Bash or PowerShell scripts. The library folder is not required.

##### meta
- `main.yml` will include all of the role's external dependencies. These dependencies will be other roles. For example, at Chevron almost all </br> roles will have `ansible-role-get-manifest` included as a dependency. As such it will be listed in `main.yml`. Any time the role is </br> run, each listed dependency will be run first.

##### tasks
- Will include any and all Ansible (.yml) files that comprise the role. These tasks will be run when the role is run. It is important to note that </br> the entry point for all runs of the role will be `main.yml`.

##### templates
- Will include any and all ARM templates (or otherwise) that are used by the role. At Chevron, ARM templates are the principal method of </br> deploying resources in Azure.

##### tests
- Will include a test playbook that will run and unit-test (or end-to-end test depending on how it is written) the role.

##### vars
- `main.yml` will include all the names and values of variables who's values should not change or should not be overridden. Variables </br> whose values are comprised of other variables are also defined here.

##### .vsts-ci.yml
- This is the Continuous Integration (CI) or pipeline file. The name will start with `.` so that the file is hidden. This is where you will include any </br> and all runtime variables, extra vars (which have the highest precedence) or other runtime configuration info such as verbosity. This CI file </br> will be read and used by the build pipeline each time a build for the role is kicked off.

##### README.md
- Will include a detailed description of what the role is able to do, example playbooks, info and descriptions of notable vars or defaults and </br> any important information that is pertinent to future updates or use of the role. Will also list any dependencies.