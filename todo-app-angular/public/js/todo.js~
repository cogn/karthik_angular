var todoApp = angular.module('todoApp', []);

todoApp.controller('TodoController', function($scope, $http) {

  $scope.todos = [];

//http://localhost/todo-app-angular/resources/todos/result.json
//http://localhost:3000/managetodo.json

  // Get all todos
  $http.get('http://localhost/todo-app-angular/resources/todos/result.json')
    .success(function(todos) {
	  alert(todos);	
      $scope.loaded = true;
      $scope.todos = todos;
    }).error(function(err) {
      alert(err);
    });

  $scope.addTodo = function(title) {
    $http.post('/todos', {
      title: title
    }).success(function(todo) {
      $scope.newTodoTitle = '';
      $scope.todos.push(todo);
    }).error(function(err) {
      // Alert if there's an error
      return alert(err.message || "an error occurred");
    });
  };

  $scope.changeCompleted = function(todo) {
    // Update the todo
    $http.put('/todos/' + todo.id, {
      completed: todo.completed
    }).error(function(err) {
      return alert(err.message || (err.errors && err.errors.completed) || "an error occurred");
    });
  };

  $scope.removeCompletedItems = function() {
    $http.get('/todos', {
      params: {
        completed: true
      }
    }).success(function(todos) {
      todos.forEach(function(t) { deleteTodo(t); });
    });
  };

  function deleteTodo(todo) {
    $http.delete('/todos/' + todo.id, {
      params: {
        completed: true
      }
    }).success(function() {
      // Find the index of an object with a matching id
      var index = $scope.todos.indexOf(
          $scope.todos.filter(function(t) {
            return t.id === todo.id;
          })[0]);

      if (index !== -1) {
        $scope.todos.splice(index, 1);
      }
    }).error(function(err) {
      alert(err.message || "an error occurred");
    });
  }

});
