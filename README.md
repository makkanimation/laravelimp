# laravelimp

#To Run Sql query

  $query = str_replace(array('?'), array('\'%s\''), $base->toSql());
  
  $query = vsprintf($query, $base->getBindings());
  
  dump($query);


# Change Public folder to public_html
## https://stackoverflow.com/questions/67328616/how-to-change-public-folder-to-public-html-in-laravel-8
then go to your public_html/index.php and add, just after the line where $app is created:

$app->bind('path.public', function() { return __DIR__; });
this will bind the document root to he current file path, where index.php exists

also, to fix the path for scripts used in CLI mode or Artisan script, you should add the code below to the file /bootstrap/app.php

$app->bind('path.public', function() { return base_path().'/public_html'; });
this will bind Laravel document root with the correct one, in this case we are linking it to public_html folder, you can also put the full path to your document root instead of the dynamic approach.

You have to follow 2 steps to change your application's public folder to public_html then your can deploy it or anything you can do :)
Edit \App\Providers\AppServiceProvider register() method & add this code .

 // set the public path to this directory
 $this->app->bind('path.public', function() {
     return base_path().'/public_html';
 });
Open server.php you can see this code

if ($uri !== '/' && file_exists(__DIR__.'/public'.$uri)) {
   return false;
}

require_once __DIR__.'/public/index.php';
Just Replace it with :

  if ($uri !== '/' && file_exists(__DIR__.'/public_html'.$uri)) {
   return false;
  }

  require_once __DIR__.'/public_html/index.php';
Then serve your application with php artisan serve, you also can deploy it on your Cpanel shared hosting where primary document root public_html
