Tooling
=======

Lando provides a way to easily define nice `lando MYCOMMAND` commands so that users can take advantage of development tools that are installed inside of containers. Setting up some common routes for things like `composer` or `npm` allows the user to get a "native" experience but perhaps more importantly allows project specific development dependencies to be isolated and run in containers instead of on the users host machine. Never worry about which version of `php` or `grunt` you need for each project.

> #### Warning::Make sure to install your dependencies
>
> You will want to make sure you install the tools you need inside of the services your app is running. If you are not clear on how to do this check out either [build steps](./../config/services.md#build-extras) or our [`ssh`](./../cli/ssh.md) command.

### Example

{% codesnippet "./../examples/trivial-tooling/.lando.yml" %}{% endcodesnippet %}

Directory Mapping
-----------------

Lando will try to map your host directory to the analogous directory inside the service. This should **MAKE IT SEEM** as though you are running the command locally.

Tool Discovery
--------------

If you are not sure about what tools live inside your container you can use `lando ssh` to drop into a shell on a specific service to both investigate and install any needed dependencies.

```bash
# SSH into the appserver
lando ssh appserver

# Explore whether grunt is installed
which grunt
  # not installed

# Add grunt
npm install -g grunt-cli

# Exit the appserver container
exit

# Add grunt to the tooling in your .lando.yml
```

While you can do the above it's generally recommended to install any additional dependencies as part of the build process either using specific dependency management built into the service you are using or with Lando's more generic [build step proces](./../config/services.md#build-extras).