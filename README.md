nudus-php
=========

If you only want MVC and you mean ONLY that, this is the _(not-really-a-)_framework for you.

## Getting started

Installation is the same steps as upgrading:

- git clone https://github.com/CodeReaper/nudus-php.git
- cd nudus-php
- cp -r .htaccess nudus &lt;path to your project root&gt;

## Mapping

If you access the root of your project, Nudus will route to the defaultController and use the defaultAction and display the default view. Assuming you have the following code in a file named 'controller/defaultController.php':

    class defaultController {
        function defaultAction() {
            view('default');
        }
    }

To map a URL like '/php/echo/key1/value1/key2/value2', you could create a php controller by creating a file at named "controller/phpController.php" with contents:

    class phpController {
        function echoAction($data) {
            // $data contains the keys key1 and key2
            // and their values value1 and value2
            view('default', $data);
        }
    }

### Things to note

- Controller class names are suffixed with 'Controller'.
- Controller class file names must match the class names.
- Callable methods on controller classes are suffixed with 'Action'.
- Implementing a 404 response requires you to need a Http404Controller class with a defaultAction().

## Views

Nudus provides two global functions to aid you in creating your views, view and asset.

### view($name, $data)

Extracts the key-value data from the $data parameter and loads the the file /view/{$name}.php.

### asset($name)

Print the path to /public/{$name} asset.
