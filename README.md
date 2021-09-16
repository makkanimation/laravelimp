# laravelimp

#To Run Sql query

  $query = str_replace(array('?'), array('\'%s\''), $base->toSql());
  
  $query = vsprintf($query, $base->getBindings());
  
  dump($query);
