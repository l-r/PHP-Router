# PHP Router class

A simple Rails inspired PHP router class.

* Usage of different HTTP Methods
* REST / Resourceful routing
* Reversed routing using named routes
* Dynamic URL's: use URL segments as parameters.

## Usage

    <?php
    require 'Router.php';

    $r = new Router();

    // maps / to controller 'users' and method 'index'.
    $r->match('/','users#index');

    // maps /user/5 to controller 'users', method 'show' with parameter 'id' => 5
    $r->match('/user/:id','users#show');

    // maps POST request to /users/ to controller 'users' and method 'create'
    $r->match('/users','users#create',array('via' => 'post'));

    // maps GET /users/5/edit to controller 'users', method 'edit' with parameters 'id' => 5 and saves route as a named route.
    $r->match('/users/:id/edit','users#edit',array('via' => 'get', 'as' => 'user_edit_page'));

    // echoes /users/5/edit
    echo $r->reverse('user_edit_page',array('id' => '5'));

    // maps multiple routes
    // GET /users will map to users#index
    // GET /users/5 will map to users#show
    $r->resources('users',array('only' => 'index,show'));


    if($r->hasRoute()) {
        // extract controller, action and parameters.
        extract($r->getRoute());

        ?>
        <h1>Route found!</h1>
        <p><b>Controller: </b><?php echo $controller; ?></p>
        <p><b>Action: </b><?php echo $action; ?></p>
        <p><b>Params: </b><?php var_dump($params); ?></p>
        <?php

    } else {
        ?><h1>No route found.</h1><?php
    }
    
    ?>   


## More information
Have a look at the example file or read trough the class' documentation for a better understanding on how to use this class.