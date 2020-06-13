#### Redux Integration in React JS
- First of all add 'Action Type' (Just type of operation you are going to perform for eg. in e-commercial website we have to add the product price so we will make unique name for this  *action type* i.e PRODUCT_ADD).
- In second step we have to create 'Action' (basically it describe that what is going to happen inside this process).**From component we generally call Action method to process the functionality beacuse it is responsible to run the reduce function. Generally we use the below code to call the functionality from the repective component.***
```javascript
   dispatch(addProduct)
``` 
- In the End we have to make the 'Reducer'  file where we actually write the logic to perform the operation.


######  Lets  discuss the implementation of the reducer in react js with example:-

We are making the redux for shop to make the count of the cake after each sell.


1.  Create the  'Action Type' as discussed.
```javascript
//cakeType.js
export const BUY_CAKE = 'BUY_CAKE'
```

2. Now Create the 'Action'  for the above 'Action Type'.
```javascript
//cakeActions.js
import { BUY_CAKE } from './cakeTypes';
export const buyCake = (number = 1) => {
  return {
    type: BUY_CAKE,
    payload: number
       }
  }
```

3. Now create the 'Reducer' the main logic.

```javascript
//cakeReducer.js
import { BUY_CAKE } from './cakeTypes';

const initialState = {
  numOfCakes: 10
}

const cakeReducer = (state = initialState, action) => {
  switch (action.type) {
    case BUY_CAKE: return {
      ...state,
      numOfCakes: state.numOfCakes - action.payload
    }

    default: return state
  }
}

export default cakeReducer
```

#### Now how we can make make use inside component.
1. If we have to take the data from the Redux state the we have to use:-
```javascript
mapStateToProps
```
2. When call the methods of the reducer then we have to use:-
```javascript
mapDispatchToProps
```
3. For the communication among component, mapStateToProps and mapDispatchToProps. We have to use the *connect*  from below import : -
```javascript
import { connect } from 'react-redux'
```

Now lets complete the above example from the working of the component that will use the aboue as the redux methods.
```javascript
import React from 'react';
import { connect } from 'react-redux';
import { buyCake } from '../redux';    // 'Action' function

function CakeContainer (props) {
  return (
    <div>
      <h2>Number of cakes - {props.numOfCakes} </h2>
      <button onClick={props.buyCake}>Buy Cake</button>
    </div>
  )
}

const mapStateToProps = state => {
  return {
    numOfCakes: state.cake.numOfCakes
  }
}

const mapDispatchToProps = dispatch => {
  return {
    buyCake: () => dispatch(buyCake())
  }
}

export default connect(mapStateToProps,mapDispatchToProps)(CakeContainer)
```

##  At the end two most important part of the redux:-

1. We have to create the rootReducer.js file where we can combine all the reducer file to make them availlable.:-

```javascript
//rootReducer.js
import { combineReducers } from 'redux'
import cakeReducer from './cake/cakeReducer' ;   // reducer file 1
import iceCreamReducer from './iceCream/iceCreamReducer';    // reducer file 2
import userReducer from './user/userReducer';    // reducer file 3

const rootReducer = combineReducers({
  cake: cakeReducer,
  iceCream: iceCreamReducer,
  user: userReducer
})
export default rootReducer
```

2. In the Second we have to provide this inside store.

```javascript
//store.js
import { createStore, applyMiddleware } from 'redux'
import { composeWithDevTools } from 'redux-devtools-extension'
import logger from 'redux-logger'
import thunk from 'redux-thunk'

import rootReducer from './rootReducer'  // Created above.

const store = createStore(rootReducer,composeWithDevTools(applyMiddleware(logger, thunk)))

export default store

```

3.  At the end wrapped the component inside **Provider** tag and pass the store as above we have created.

```javascript
import React from 'react'
import { Provider } from 'react-redux'
import './App.css'
import store from './redux/store'    //As we have create above.
import CakeContainer from './components/CakeContainer'   //component 1
import HooksCakeContainer from './components/HooksCakeContainer'  //component 2

function App() {
  return (
    <Provider store={store}>
      <div className='App'>
        <CakeContainer />
        <HooksCakeContainer />
      </div>
    </Provider>
  )
}

export default App
```

### Install the following npm package.
```shell
npm install redux --save
npm install --save  react-redux
npm i redux-devtools-extension
npm i redux-logger
npm i redux-thunk
```





