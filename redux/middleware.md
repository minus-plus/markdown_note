react middlewares
https://github.com/JoV5/blog/issues/1

Compose functions
=================
redux >> src >> utils > compose.js 
```
function compose(...funcs) {
	if (funcs.length === 0) {
		// return a function that do nothing to the arguments
		return arg => arg
	}

	if (funcs.length === 1) {
		return funcs[0]
	}

	const last = funcs[funcs.length - 1]
	const rest = funcs.slice(0, -1)
	// most inner function is last and should be the initial value of composed function
	return (...args) => rest.reduceRight(function(composed, f) => f(composed), last(...args))
}

NOTE:
Array.prototype.reduceRight()
The reduceRight() method applies a function against an accumulator and each value of the array (from right-to-left) to reduce it to a single value.
var flattened = [[0, 1], [2, 3], [4, 5]].reduceRight(function(a, b) {
    return a.concat(b);
}, []);

// flattened is [4, 5, 2, 3, 0, 1]

applyMiddleware
===============
applyMiddleware()是比createStore更高阶的函数，传入middlewares list作为参数，并会在applyMiddleware()内执行createStore()??【存疑】
```
function applyMiddleware(...middlewares) {
	return (createStore) => (reducer, preloadedState, enhancer) => {
		var store = createStore(reducer, preloadedState, enhancer)
	}
}
```


```


const logger = store => next => action => {
	console.log('dispatching', action);
	let result = next(action);
	console.log('next state', store.getState());
	return result;
};


// composing functions with parameters (store, next, action)
const logger = function(store) {
	return function(next) {
		return function(action) {
			console.log('dispatching', action);
			let result = next(action);
			console.log('next state', store.getState());
			return result;
		}
	}
}


======

{(!this.state.readMore && this.props.description !== null && this.props.description.length > 50) ?
                                ((this.state.readMore) ? "... show less" : "... read more") :
                                ("")
                            }


 {
 	(this.props.description !== null && this.props.description.length > 50) ? 
 		(!state.readMore ? "... read more" : '... show less') :
 		("")

 }


If staring down JavaScript leaves you unsteady, take heart. Mat Marquis is at your side, offering a detailed yet approachable tour around this essential language. Make your way through plenty of practical examples, as you pick up syntax rules, the fundamentals of scripting, and how to handle data types and loops. You’ll emerge clear-eyed and confident—and ready to get to work.


假如 createStore 不作为参数传给enhancer，而是被enhancer调用，行不行？ 好像也可以



function applyMiddleware(...middlewares) {
  return (reducer, preloadedState, enhancer) => {
    var store = createStore(reducer, preloadedState, enhancer)
    var dispatch = store.dispatch
    var chain = []

    var middlewareAPI = {
      getState: store.getState,
      dispatch: (action) => store.dispatch(action)
    }

    // all middles will process the same middlewareAPI, that is {getState, dispatch(action)}
    // transform function to other function
    chain = middlewares.map(middleware => middleware(middlewareAPI))
    dispatch = compose(...chain)(store.dispatch)

    return {
      ...store,
      dispatch
    }
  }
